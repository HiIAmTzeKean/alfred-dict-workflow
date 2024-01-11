# Alfred Translation

## Installation

Tested on Alfred 5 MacOS Sonoma 14.2

Requirements:
- lxml
- python 2.7.18
 
```bash
pip install lxml
brew install pyenv
pyenv install 2.7.18
pyenv global 2.7.18

```

Reference to install python2 on mac can be found below
- https://stackoverflow.com/questions/60298514/how-to-reinstall-python2-from-homebrew 

## Changes made
```bash
PATH=$PATH:$(pyenv root)/shims
```
Has been added into the script to force the terminal to use python2 as the default python.
Refer to the plist file.

## Post notes from Developer

* 支持的词典：
    * 系统词典，支持朗道、牛津词典
    * 有道在线词典
    * 爱词霸在线词典
    * <del>百度在线词典</del>
    * 必应在线词典
    * 海词在线词典
* 支持英汉、汉英互查
* 支持音标，默认显示美式音标
* 使用系统 TTS 引擎发音
* 可快速复制释义
* 可使用快捷键进行词典切换
* 缓存查询结果，方便下次查询
* 支持快捷键取词
* 支持自定义配置

## 截图

![screenshot](http://ww1.sinaimg.cn/large/ded9da26gy1fuchcybxkbg20i70fqnpe.gif)

## 查词

查词：

    cc {word} @ {dict}

词典代号：

词典                          | 代号        
--------------------------- | ----------- 
系统内置牛津词典（需要 lxml）   | nj, oxford
朗道本地词典（需下载）         | ld, landau 
有道在线词典                  | yd, youdao  
爱词霸在线词典                 | cb, iciba    
<del>百度在线词典</del>       | <del>bd, baidu</del>   
必应在线词典                  | by, bing    
海词在线词典                  | hc, dictcn

注：

* 关键词默认为 cc（即查词），可通过配置文件修改。
* 每个词典有长短两个代号，短的代号为拼音缩写，便于记忆，长的代号为全称。
* 可以为每个词典启用一个切换快捷键，`⌘`/`⌥`/`⌃`/`⇧`/`fn` + `↩`，可通过配置文件修改。
* 朗道词典非系统内置，请先[下载](http://pan.baidu.com/s/1qWx4mV6)，然后复制到 `~/Library/Dictionaries/` 目录。
* 由于必应、海词没有提供 API，只能通过解析 HTML 得到，因此速度可能稍慢（已优化）。

## 内部命令

查看内部命令：

    cc :

命令     | 功能
------- | ---------------------------------
clean   | 清除所有缓存
config  | 编辑配置文件（json 格式）
update  | 修改配置文件的某些项后需要更新才能生效

建议每次修改配置文件后，执行一次 update，确保生效。

## 配置文件

配置文件为 json 格式，目前有以下选项：

* "keyword": 关键字，默认为 "cc"。
* "default": 默认词典，即省略 `@ {dict}` 时使用的词典，默认为"nj"。
* "keymap": 键绑定，修改切换词典快捷键，支持以下修饰键：
    * "none": 直接回车时的行为，可取 "open" 或 "say"：
        - "open"：打开详细解释页面（浏览器或系统词典）。
        - "say"：发音，目前只支持系统 tts 引擎。
    * "ctrl/alt/shift/cmd/fn": 词典代号，长短皆可。
* "options": 词典相关的选项，一般不用修改。
    * "dictcn": 海词词典选项：
        * "wap_page": 是否使用 wap 页面查词，wap 页面信息较少，默认为 "false"。
* "cache": 缓存相关的设置。
    * "enable": 打开或关闭缓存，默认为 "true"。
    * "expire": 缓存失效时间，以小时为单位，默认为 "24"。

注：

* 配置文件里同样有较详细英文注释，请修改之前务必了解每个选项的作用。
* "keyword" 和 "keymap" 这两个选项修改完之后执行 update 才能生效。
* 没有特殊需求，无需修改配置文件，保持默认即可。

## LICENSE

GPL

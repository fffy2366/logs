# [安装Sublime Text 3插件的方法](http://www.cnblogs.com/Rising/p/3741116.html)

直接安装
安装Sublime text 2插件很方便，可以直接下载安装包解压缩到Packages目录（菜单->preferences->packages）。

使用Package Control组件安装
也可以安装package control组件，然后直接在线安装：

按Ctrl+`调出console（注：安装有QQ输入法的这个快捷键会有冲突的，输入法属性设置-输入法管理-取消热键切换至QQ拼音）
粘贴以下代码到底部命令行并回车：
```
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```
重启Sublime Text 3。
如果在Perferences->package settings中看到package control这一项，则安装成功。
顺便贴下Sublime Text2 的代码

```
import urllib2,os; pf='Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler( ))); open( os.path.join( ipp, pf), 'wb' ).write( urllib2.urlopen( 'http://sublime.wbond.net/' +pf.replace( ' ','%20' )).read()); print( 'Please restart Sublime Text to finish installation')
```
如果这种方法不能安装成功，可以到这里下载文件手动安装。

用Package Control安装插件的方法：

按下Ctrl+Shift+P调出命令面板
输入install 调出 Install Package 选项并回车，然后在列表中选中要安装的插件。
不爽的是，有的网络环境可能会不允许访问陌生的网络环境从而设置一道防火墙，而Sublime Text 2貌似无法设置代理，可能就获取不到安装包列表了。
好，方法介绍完了，下面是本文正题，一些有用的Sublime Text 2插件：

GBK Encoding Support
对应gb2312来说，Sublime Text 2 本生不支持的，我们可以通过Ctrl+Shift+P调出命令面板或Perferences->Package Contro,输入install 调出 Install Package 选项并回车，在输入“GBK Encoding Support”选择开始安装，左下角状态栏有提示安装成功。这时打开gbk编码的文件就不会出现乱码了，如果有需要转成utf-8的可以在File-GBK to UTF8-选择Save with UTF8就偶看了。

Zen Coding
这个，不解释了，还不知道ZenCoding的同学强烈推荐去看一下：《Zen Coding: 一种快速编写HTML/CSS代码的方法》。

Sublime Text 3 常用插件以及安装方法 --PHP 第1张
emmet

PS:Zen Coding for Sublime Text 2插件的开发者已经停止了在Github上共享了，现在只有通过Package Control来安装。

jQuery Package for sublime Text
如果你离不开jQuery的话，这个必备～～

Sublime Prefixr
Prefixr，CSS3 私有前缀自动补全插件，显然也很有用哇

Sublime Text 3 常用插件以及安装方法 --PHP 第2张
Sublime Prefixr

JS Format
一个JS代码格式化插件。

SublimeLinter
一个支持lint语法的插件，可以高亮linter认为有错误的代码行，也支持高亮一些特别的注释，比如“TODO”，这样就可以被快速定位。（IntelliJ IDEA的TODO功能很赞，这个插件虽然比不上，但是也够用了吧）

Sublime Text 3 常用插件以及安装方法 --PHP 第3张
SublimeLinter

Placeholders
故名思意，占位用，包括一些占位文字和HTML代码片段，实用。

Sublime Alignment
用于代码格式的自动对齐。传说最新版Sublime 已经集成。

Sublime Text 3 常用插件以及安装方法 --PHP 第4张

Clipboard History
粘贴板历史记录，方便使用复制/剪切的内容。

DetectSyntax
这是一个代码检测插件。

Nettuts Fetch
如果你在用一些公用的或者开源的框架，比如 Normalize.css或者modernizr.js，但是，过了一段时间后，可能该开源库已经更新了，而你没有发现，这个时候可能已经不太适合你的项目了，那么你就要重新折腾一遍或者继续用陈旧的文件。Nettuts Fetch可以让你设置一些需要同步的文件列表，然后保存更新。

Sublime Text 3 常用插件以及安装方法 --PHP 第5张

JsMinifier
该插件基于Google Closure compiler，自动压缩js文件。

Sublime CodeIntel
代码自动提示

Bracket Highlighter
类似于代码匹配，可以匹配括号，引号等符号内的范围。

Sublime Text 3 常用插件以及安装方法 --PHP 第6张

Hex to HSL
自动转换颜色值，从16进制到HSL格式，快捷键 Ctrl+Shift+U

Sublime Text 3 常用插件以及安装方法 --PHP 第7张

GBK to UTF8
将文件编码从GBK转黄成UTF8，快捷键Ctrl+Shift+C

Git
Sublime Text 3 常用插件以及安装方法 --PHP 第8张

该插件基本上实现了git的所有功能。

Shell Turtlestein
命令行工具，参考：
http://stackoverflow.com/questions/12103028/sublime-text-2-open-cmd-prompt-at-current-or-project-directory-windows

[Sublime Text3配置Node.js开发环境](http://my.oschina.net/ximidao/blog/413101)
摘要
习惯了用 Sublime Text开发神器写代码，目前在使用Node.js，正好github上有一个 Sublime Text的Node.js的插件，于是就尝试着配置了一下
1、下载Nodejs插件，下载地址为：
https://github.com/tanepiper/SublimeText-Nodejs

下载zip压缩包后解压，文件名改为Nodejs


2、打开Sublime Text3，点击菜单“Perferences” =>“Browse Packages”打开“Packages”文件夹，并将第1部的Nodejs文件夹剪切进来


3、打开文件“Nodejs.sublime-build”，将代码 "encoding": "cp1252" 改为 "encoding": "utf8" ，将代码 "cmd": ["taskkill /F /IM node.exe & node", "$file"] 改为 "cmd": ["node", "$file"] ，保存文件



4、打开文件“Nodejs.sublime-settings”，将代码 "node_command": false改为 "node_command": "D:\\Program Files\\nodejs\\node.exe" ，将代码 "npm_command": false 改为 "npm_command": "D:\\Program Files\\nodejs\\npm.cmd" ，保存文件



5、编写一个测试文件test.js，按“ctrl+B"运行代码，运行结果如下图所示：


至此，环境配置成功！



## 在线安装
* ctrl+shift+p->install->nodejs
* Preferences->Browse Packages
* 文件：\AppData\Roaming\Sublime Text 3\Installed Packages\Nodejs.sublime-package
这种方法不知道哪里配置编码

* Preferences->Browse Packages
* mkdir nodejs
* git clone https://github.com/tanepiper/SublimeText-Nodejs nodejs
* 输入github用户名密码
* 进入nodejs目录，编辑文件Nodejs.sublime-build
将"encoding": "cp1252" 改为 "encoding": "utf8" 
将"cmd": ["taskkill /F /IM node.exe & node", "$file"]替换为
"cmd": ["node", "$file"]
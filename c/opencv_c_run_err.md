##解决Win10 64bit + VS2012 使用opencv时出现提“应用程序无法正常启动（0xc000007b）”错误

这个错误出现的原因应该是64位与32位的兼容问题。

一开始opencv库都调用x64，不行。

全都换成x86，也不行。

后来是因为环境变量中必须同时加上x86和x64的bin文件目录，解决。

参考：
http://www.cnblogs.com/fawkes/p/3303536.html
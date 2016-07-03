 Linux终端使用wget下载百度云资源

 很多时候为了方便将大文件放到百度云盘中作为共享资源。

在windows下和Linux桌面系统中，使用浏览器很容易下载百度云盘里的共享资源，但当我们使用Linux字符界面的时候，就会变的很麻烦。

一直在找解决的方法，有人使用百度云应用，通过百度云Linux客户端来解决文件上传与下载问题。

百度云盘Linux下的Python客户端：https://github.com/houtianze/bypy

但在Linux终端需要配置参数以及配置应用数据等比较复杂，故想找一种wget就能下载共享文件的简单可行的办法。


于是发现了文章：http://www.centoscn.com/CentOS/2014/0928/3876.html


自己实践如下：

1.在百度云盘中共享一个文件



2.在浏览器中下载此文件（真正用意是找到它的下载地址），在浏览器下载界面找到下载文件，并复制文件的下载地址：



3.保存此下载地址，在Linux终端使用wget下载：

wget -c --referer=http://pan.baidu.com/s/1hq04k1e -O testfile.PNG "http://nb.baidupcs.com/file/6a0a41574d8603ff04786b046da3e361?...........testfile.PNG"

注：此处-c 为断点续传，--referer为百度云分享地址，-O为指定输出文件，后面接浏览器下载文件的下载地址。


终于可以使用wget轻松下载百度云盘共享的资源了。


来自：http://blog.csdn.net/boycy/article/details/41210981

wget -c --referer=http://pan.baidu.com/s/1czDXuQ -O test_del.rar "https://bjbgp01.baidupcs.com/file/141a102523e0bb2d697246ee1b98e459?bkt=p3-000064b63b78796a5e2d44bdae6899f81d70&fid=3859138035-250528-876587492163975&time=1466579796&sign=FDTAXGERLBH-DCb740ccc5511e5e8fedcff06b081203-pIcTeUq5AHLEbVW5dLTBapF6JuU%3D&to=hbjbgp&fm=Yan,B,G,bs&sta_dx=878&sta_cs=0&sta_ft=rar&sta_ct=0&fm2=Yangquan,B,G,bs&newver=1&newfm=1&secfm=1&flow_ver=3&pkey=000064b63b78796a5e2d44bdae6899f81d70&sl=70910030&expires=8h&rt=sh&r=238094813&mlogid=4027121410811269534&vuk=3859138035&vbdid=1331887625&fin=%E5%88%A0%E9%99%A4_%E6%B5%8B%E8%AF%95.rar&fn=%E5%88%A0%E9%99%A4_%E6%B5%8B%E8%AF%95.rar&slt=pm&uta=0&rtype=1&iv=0&isw=0&dp-logid=4027121410811269534&dp-callid=0.1.1"



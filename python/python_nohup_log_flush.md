# python nohup & 没有日志
最近在用nohup执行python脚本，发现nohup.out 里日志不实时写入，后来发现stdout是启用了缓冲区。
```
nohup python xxx.py &
```

解决办法就是用python -u ,如下：

```
nohup python -u xxx.py &
```

现在就可以查看实时日志了
```
tail -f nohup.out
```

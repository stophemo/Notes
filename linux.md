

# linux命令

## 网络通讯

### telnet

![image-20220729150453569](linux.assets/image-20220729150453569.png)

Linux telnet命令用于远端登入。

执行telnet指令开启终端机阶段作业，并登入远端主机。

![image-20220729150515532](linux.assets/image-20220729150515532.png)



```
 telnet localhost 8888
```



### netstat



```
netstat -ano
// 显示所有连接中的socket（显示PID）
```



### tasklist

```
tasklist|findstr "1360"
// idea64.exe                    1360 Console                   19  1,132,320 K
```


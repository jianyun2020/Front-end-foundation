
# 查看文件安装目录

```shell
ps -ef|grep nginx
```

# 查看端口

```shell
netstat -apn|grep 443
```

# 查看端口使用情况

```shell
netstat -lntp
```

# 开启443端口

Linux 开启443端口
在Linux终端输入指令：

iptables -I INPUT -p tcp --dport 443 -j ACCEPT

 
2
回车之后继续输入指令，输入保存防火墙配置指令：

service iptables save

 
3
确认之火，返回防火墙配置保存成功的提示信息

 
4
输入重启防火墙服务指令：

service iptables restart

 
5
回车执行指令，返回防火墙服务重启成功的提示信息，

至此，成功开启了443端口


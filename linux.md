使用free命令可以查看内存

使用lsof -i:<端口号>，可以查看端口占用情况。

疑问命令

```
lsblk
```

<++>

### manjaro的防火墙

默认防火墙为iptables和ip6tables。

```
sudo systemctl start iptable //开启防火墙
sudo systemctl stop iptable  //关闭防火墙
sudo systemctl restart iptable //重启防火墙
sudo systemctl enable iptable //防火墙开机自启
sudo systemctl disable iptable //关闭防火墙开机自启
```


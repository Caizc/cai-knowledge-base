# CentOS 7.2 iptables 配置命令

```shell
iptables --list
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
service iptables save
systemctl restart iptables.service
```

---

change log: 

	- 创建（2019-05-15）

---



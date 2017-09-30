> 1、yum提示Another app is currently holding the yum lock; waiting for it to exit...

在使用yum install 失败之后，再一次使用yum install后出现的错误。只需要使用ps aux \| grep yum 然后kill 掉该id即可。

[http://blog.csdn.net/testcs\_dn/article/details/48711805](http://blog.csdn.net/testcs_dn/article/details/48711805)

---

> 2、CentOS使用yum安装软件时出现Could not retrieve mirrorlist...

在我使用yum安装docker的时候出现的，多半是网络问题，网上说配置eth0网卡dns为8.8.8.8 然后 service network restart 即可，但当我使用ifconfig查看的时候，发现我centos7 并没有eth0，而是有一个eth0sop（具体名字忘记了，应该是随机的）。那我首先要添加一个eth0吧。根据以下教程的说法，我重命名了该网卡为eth0，并且经历一系列我自己都不知道有什么用的操作。然后重启reboot即可正常使用Yum install docker。都不需要我去配置dns.

[http://www.cnblogs.com/feixiangtk/p/6819118.html](http://www.cnblogs.com/feixiangtk/p/6819118.html)

---




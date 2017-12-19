### 搭建 nginx 镜像

今天我们利用之前最早的镜像centos，创建一个临时容器。

```
$ docker run -it --privileged --name tmp centos /usr/sbin/init
```

界面会卡死，但无所谓。我们新开一个xshell窗口。

然后使用exec进行操作。利用交互式方式进入后再安装。

> $ docker exec -it tmp /bin/bash

---

### 安装 Nginx

```
$ rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
$ yum install nginx -y
$ systemctl enable nginx
$ systemctl start nginx
```

测试是否安装成功

```
$  curl http://localhost:80 
```

![](/assets/L@KWO]3_JC~N%28]ENUNWU_%28S.png)

---




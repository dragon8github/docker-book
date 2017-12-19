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

测试是否安装成功（Nginx默认安装是80端口，且没有其他端口占据，所以这里应该是正常的）

```
$  curl http://localhost:80
```

![](/assets/L@KWO]3_JC~N%28]ENUNWU_%28S.png)

---

### 保存容器 / 提交镜像

[https://docs.docker.com/engine/reference/commandline/commit/\#description](https://docs.docker.com/engine/reference/commandline/commit/#description)

用到命令：`$ docker commit`

我们还需要 -c 参数，该参数使用的内容是之前的章节 Dockerfile 使用的配置。但现在我们也可以通过 Commit 的方式来创建。

* CMD：默认启动容器使用的命令
* EXPOSE: 暴漏的端口

```
$ docker commit -c 'CMD ["/usr/sbin/init"] ' -c "EXPOSE 80" tmp centos:nginx
```




### 搭建 nginx 镜像

今天我们利用之前最早的镜像centos，创建一个临时容器。

```
$ docker run -it --privileged --name tmp centos /usr/sbin/init
```

界面会卡死，但无所谓。我们新开一个xshell窗口。

然后使用exec进行操作。利用交互式方式进入后再安装。

> $ docker exec -it tmp /bin/bash

---

### 手工进入容器安装 Nginx

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

### 保存镜像 / 提交镜像

[https://docs.docker.com/engine/reference/commandline/commit/\#description](https://docs.docker.com/engine/reference/commandline/commit/#description)

用到命令：`$ docker commit`

另外我们需要使用一个重要的参数 -c ，该参数使用的内容，和之前的章节 Dockerfile 使用的配置一样。

但现在我们也可以通过 Commit -c 的方式来配置创建了。

* CMD：默认启动容器使用的命令
* EXPOSE: 暴漏的端口

```bash
$ docker commit -c 'CMD ["/usr/sbin/init"] ' -c "EXPOSE 80" tmp centos:nginx
```

![](/assets/123123123123123123123import.png)

---

### 将容器中的文件拷贝到主机 / 将主机中的文件拷贝到容器

https://docs.docker.com/engine/reference/commandline/cp/

> $ docker cp

1、将容器中的文件拷贝到主机

```bash
 $ mkdir /root/nginx && /root/nginx/conf
 $ docker cp tmp:/etc/nginx/nginx.conf /root/nginx/conf/
 $ cat /root/nginx/conf/nginx.conf
```




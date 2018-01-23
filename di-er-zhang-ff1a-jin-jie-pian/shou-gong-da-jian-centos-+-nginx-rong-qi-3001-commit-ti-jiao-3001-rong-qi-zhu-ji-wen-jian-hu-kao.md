### 搭建 nginx 镜像

今天我们利用之前最早的镜像centos，创建一个临时容器。

```
$ docker run -it --privileged --name tmp centos /usr/sbin/init
```

![](/assets/axczxaddgfgimport.png)

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

### 保存镜像 / 提交镜像 / 制作镜像

[https://docs.docker.com/engine/reference/commandline/commit/\#description](https://docs.docker.com/engine/reference/commandline/commit/#description)

用到命令：`$ docker commit`

另外我们需要使用一个重要的参数 -c ，该参数使用的内容，和之前的章节 Dockerfile 使用的配置一样。

但现在我们也可以通过 Commit -c 的方式来配置创建了。

* CMD：默认启动容器使用的命令
* EXPOSE: 暴漏的端口

```bash
$ docker commit -c 'CMD ["/usr/sbin/init"] ' -c "EXPOSE 80" tmp centos:nginx
```

制作完成![](/assets/azxvxcvcsadsdfimport.png)

---

### 将容器中的文件拷贝到主机

[https://docs.docker.com/engine/reference/commandline/cp/](https://docs.docker.com/engine/reference/commandline/cp/)

> $ docker cp

将容器中的文件拷贝到主机

```bash
 $ mkdir /root/nginx && /root/nginx/conf
 $ docker cp tmp:/etc/nginx/nginx.conf /root/nginx/conf/
 $ cat /root/nginx/conf/nginx.conf
```

---

### 启动 nginx 镜像，将主机中的文件映射到容器中

我们可以删除临时的容器tmp了。因为之前我们已经保存好镜像了。

```
$ docker stop tmp && docker rm tmp
```

启动 nginx 镜像，将主机中的nginx/conf/nginx.conf文件映射到容器中。这也是之前章节的知识点了

```
$ docker run --name mynginx --privileged -p 9090:80 -v /root/nginx/conf/nginx.conf:/etc/nginx/nginx.conf -d centos:nginx
```

![](/assets/1649534524import.png)

测试配置是否正常

```
$ curl http://localhost:9090
```

![](/assets/146457568768import.png)

如果服务器部署在阿里云. 需要先配置一下阿里云的安全组。添加9090端口对外，然后就可以在外部访问了

![](/assets/121363575678import.png)

![](/assets/312312213231123import.png)


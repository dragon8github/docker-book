github地址：

> [https://github.com/portainer/portainer](https://github.com/portainer/portainer)

官网地址：

> [https://portainer.readthedocs.io/en/latest/deployment.html](https://portainer.readthedocs.io/en/latest/deployment.html)

---

### 1、拉取镜像

> $ docker pull portainer/portainer

### 

### 2、设置9000端口放行

> $ iptables -I INPUT -p tcp --dport 9000 -j ACCEPT

顺便设置一下阿里云安全组配置

![](/assets/12312312123import.png)

### 3、运行容器

> $ docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v /opt/portainer:/data --name mydocker portainer/portainer

![](/assets/11616import.png)

### 4、访问![](/assets/114123import.png)

首次登陆会让你创建一个账号，密码必须是8位即可。

譬如我设置账号为admin

密码为12345678

---

5、设置关联我们的Docker![](/assets/1351412312import.png)

Name 可以随意设置一个用户名，譬如我设置 Lee

Endpoint URL 必须设置上节课开通的TCP链接和端口，如：119.23.111.13:2375

尝试前，请确保上一节课能正常跑通。

然后点击Connect即可。

---

连接成功之后就进入我们的后台了![](/assets/23123123123123import.png)

---

### 使用管理工具下载mysql

选择左侧的“App Template”。选择mysql

![](/assets/23123123import.png)

Name随意设置。譬如就叫mysql。然后点击“Show advanced options”

这里可以设置端口和映射端口，mysql的端口默认是3306，我们设置为3307吧。

之后点击"Deploy the container"即可

![](/assets/135134import.png)

等待一段时间。然后跳转到Container界面，我们发现多了一个mysql 的容器。并且默认帮我们启动了

![](/assets/123123123123123151import.png)

---

但是，默认的启动方式有点问题。我们需要先删除掉这个容器，重新启动，并且按照mysql官方推荐的做法来启动。

![](/assets/12312415345import.png)

[https://hub.docker.com/\_/mysql/](https://hub.docker.com/_/mysql/)

> $ docker stop mysql && docker rm mysql

![](/assets/15123123123import.png)

然后再运行这段代码，并且可以设置密码

```
$ docker run --name mysql -p 3307:3306 -e MYSQL_ROOT_PASSWORD=123 -d mysql
```

之后就可以正常连接了。（如果是阿里云，请务必去设置好安全组，添加开放3307端口）

![](/assets/爱上112312312312import.png)


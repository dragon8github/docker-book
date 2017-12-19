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


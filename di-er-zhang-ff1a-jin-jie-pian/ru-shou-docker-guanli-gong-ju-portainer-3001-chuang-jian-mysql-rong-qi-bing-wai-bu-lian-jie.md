github地址：

> [https://github.com/portainer/portainer](https://github.com/portainer/portainer)

官网地址：

> [https://portainer.readthedocs.io/en/latest/deployment.html](https://portainer.readthedocs.io/en/latest/deployment.html)

---

### 1、拉取镜像

> $ docker pull portainer/portainer

### 2、设置9000端口放行

> $ iptables -I INPUT -p tcp --dport 9000 -j ACCEPT

随便设置一下阿里云安全组配置

![](/assets/12312312123import.png)

### 3、运行容器

> $ docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v /opt/portainer:/data --name mydocker portainer/portainer

![](/assets/11616import.png)

4、访问![](/assets/114123import.png)

该界面是让你创建一个账号，密码必须是8位即可


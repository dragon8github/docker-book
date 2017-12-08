github地址：

> https://github.com/portainer/portainer

官网地址：

> https://portainer.readthedocs.io/en/latest/deployment.html



---

### 1、拉取镜像

> $ docker pull portainer/portainer

### 

### 2、运行容器

> $ docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v /opt/portainer:/data --name mydocker portainer/portainer




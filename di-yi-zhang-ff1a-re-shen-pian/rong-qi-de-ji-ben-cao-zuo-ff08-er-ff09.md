我们pull了一个纯净镜像，如果想要安装一些软件的话， 怎么办？

1、硬来

利用attach进入，各种yum，各种安装 \(你会发现好多权限问题\)

2、Dockerfile

今天我们来看一下如何利用Dockerfile创建一个镜像

Dockerfile是由一系列命令和参数构成的脚本，这些命令应用于基础镜像并最终创建一个新的镜像。

官方文档：[https://docs.docker.com/engine/reference/builder/\#usage](https://docs.docker.com/engine/reference/builder/#usage)

---

### ⏰ Dockerfile

新建 Dockerfile

* FROM ： 基于现有的镜像来创建（也就是基于`$ docker images`列表中的镜像来创建）；
* RUN ： 在容器中运行的语句；
* EXPOSE：容器对外暴露的端口，可以设置多个。

```js
FROM centos:latest
RUN yum -y install httpd
RUN  systemctl enable httpd.service
EXPOSE 80
```

![](/assets/659659569import.png)

### 🏠 docker build 命令

用于读取 Dockerfile 创建镜像

```
$ docker build -t centos:httpd .
```

** （注意，最后有一个点，很重要。代表当前文件夹中找Dockerfile**）

build完成之后，通过 `$ docker images` 可以看到一个标签（TAG）为 httpd 的 centos 新镜像。

> 顺带一提，这个TAG只是一个标注、注释。并不一定说明该centos镜像就一定是最新的。

![](/assets/213123123import.png)

---

### 🌼 启动容器

我们尝试之前学到的启动容器方式如

```
$ docker run  -d -p 8080:80 --name myhttpd centos:httpd
```

这时你会发现根本启动不了，它就是一直处于停止状态  \(╬￣皿￣\)凸。

这时我们以交互式方式进入。发现是可以进入的（先删除之前的容器）

```
$ docker stop myhttpd && docker rm myhttpd
$ docker run -i -t  -p 8080:80 --name myhttpd centos:httpd
```

![](/assets/54545544545import.png)我们在容器内部查看一下httpd的状态 `$ systemclt status httpd`，却发现是没有权限的。

![](/assets/56565import.png)

docker 对容器的权限有一定的限制规则。那么怎么给容器加特权呢？

---

### 🍁 使用 --privileged 给容器加特权

给容器加特权,否则交互式方式进入容器无法操作一些譬如修改内核、修改系统参数、甚至启动服务等

```
$ docker run --privileged -d -p 8080:80 --name myhttpd centos:httpd /usr/sbin/init
```

此时我们发现已经启动成功了。![](/assets/1312331123import.png)

我们使用浏览器访问一下 ip + 8080端口

![](/assets/6656766import.png)


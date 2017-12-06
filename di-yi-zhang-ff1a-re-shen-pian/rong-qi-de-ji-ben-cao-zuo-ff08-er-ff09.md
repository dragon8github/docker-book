我们pull了一个纯净镜像，如果要部署网站、安装一些软件的话， 有啥办法？

1、硬来

利用attach进入，各种yum，各种安装 \(你会发现好多权限问题\)

2、Dockerfile

今天我们来看一下如何利用Dockerfile创建一个镜像

Dockerfile是由一系列命令和参数构成的脚本，这些命令应用于基础镜像并最终创建一个新的镜像。

官方文档：[https://docs.docker.com/engine/reference/builder/\#usage](https://docs.docker.com/engine/reference/builder/#usage)

---

### Dockerfile

譬如我们是PHP开发人员，可能要用到apache\(httpd\)，我们希望直接构建出一个环境容器。

接下来我们创建一个空文件夹，CD进入。然后创建一个文件叫做 Dockerfile \(注意大小写\)，插入内容如下：

* FROM ： 基于现有的镜像来创建（也就是基于`$ docker images`列表中的镜像来创建）
* RUN ： 在容器中运行的语句。下面我们将在容器中下载Apche（httpd），并且设置为服务启动项

> FROM centos:latest   
>
> RUN yum -y install httpd
>
> RUN  systemctl enable httpd.service
>
> EXPOSE 80

![](/assets/659659569import.png)

### docker build 命令

用于读取 Dockerfile 创建镜像

> $ docker build -t centos:httpd .

** （注意，最后有一个点，很重要。代表当前文件夹**）

当然也可以指定Dockerfile

> $ docker build -f /path/to/a/Dockerfile .

下载完成之后，通过 `$ docker images` 可以看到出现了一个新镜像叫做centos 只不过标签变成了 httpd

![](/assets/213123123import.png)

---

### 启动httpd以及排坑

docker 对容器的权限有一定的限制规则

总而言之，如果我们尝试之前学到的启动容器方式如

> $ docker run  -d -p 8080:80 --name myhttpd centos:httpd

![](/assets/67342import.png)

这时你会发现根本启动不了。它就是一直处于停止状态。这时我们以交互式方式进入。发现是可以进入的（需要先删除刚刚的容器）

> $ docker run -i -t  -p 8080:80 --name myhttpd centos:httpd

![](/assets/54545544545import.png)我们在容器（centos7）内部查看一下httpd的状态，却发现是没有权限的

![](/assets/56565import.png)

就如我们开头所说，docker 对容器的权限有一定的限制规则。那么怎么给容器加特权呢？

---

### 给容器加特权

给容器加特权,否则交互式方式进入容器无法操作一些譬如修改内核、修改系统参数、甚至启动服务等

> $ docker run --privileged -d -p 8080:80 --name myhttpd centos:httpd /usr/sbin/init

（在启动容器时，执行命令 `/usr/sbin/init`）

![](/assets/1312331123import.png)此时我们发现已经启动成功了。

我们仍然使用浏览器访问一下 ip + 8080端口

![](/assets/6656766import.png)


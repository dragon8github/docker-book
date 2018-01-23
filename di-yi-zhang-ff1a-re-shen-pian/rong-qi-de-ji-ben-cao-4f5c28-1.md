正式环境下，我们很少直接使用第三方提供的镜像。因为这可能是不安全的，不全面的，又或者是过于冗余的。

所以通常都是自己基于官方的镜像来搭建的一个镜像，从这节课开始我们将基于Centos镜像学习搭建一个自己的镜像。

---

### 容器的概念

> container是images运行时的的状态。docker对于运行过的image都保留一个状态（container），可以使用命令docker ps来查看正在运行的container，对于已经退出的container，则可以使用docker ps -a来查看。 如果你退出了一个container而忘记保存其中的数据，你可以使用docker ps -a来找到对应的运行过的container使用docker commit命令将其保存为image然后运行。

**1、查看所有运行中的容器**

> $ docker ps

![](/assets/2312312321import.png)

**2、停止容器**

> $ docker stop &lt;CONTAINER ID&gt;

![](/assets/676776import.png)

**3、查看所有容器**

再次使用 `$ docker ps` 发现镜像列表已经空空如也了。难道是镜像被删除了吗？

当然不是。只是停止运行了。我们需要加入 -a 来查看所有的镜像

> $ docker ps -a

![](/assets/32525import.png)

**4、删除指定的容器**

> $ docker rm &lt;CONTAINER ID&gt;

![](/assets/100import.png)

5**、启动容器，当停止的容器需要重新启动时**

> $ docker start &lt;containerID&gt;



### 镜像的概念

1**、查看所有的镜像源**

> $ $ docker images

2、**删除镜像，只有当所有基于该镜像的容器被删除之后，才可以删除该镜像**

> $ docker rmi &lt;IMAGE ID&gt;



---

### 下载官方的镜像源

先从阿里云docker仓库中搜索Centos，并且找到官方认证的源![](/assets/65223import.png)默认下载的是我们最新的版本

> $ docker pull centos

由于我们删除了上节课的apache-php，所以只有最新下载的centos镜像了

![](/assets/562342import.png)

---

### 和容器进行交互

`$ docker run`命令的几个参数（可以运行 docker run --help 查看更多详细说明）

* -i： 打开stdin，用于和容器进行交互，通常与 -t 同时使用；
* -t：为容器创建虚拟终端，我们就可以登录终端了通常与 -i 同时使用；
* --name：  譬如 --name xxxooo: 为容器指定一个名称。

输入以下命令我们就可以进入容器内部了。

> $ docker run -i -t --name fuck centos

![](/assets/342342import.png)**按下 CTRL + D 或 输入 “exit” 可以退出容器。**

当我们退出容器后，我们使用 `$ docker ps` 发现容器没有在运行列表中。难道他被消灭了吗？NO！只是停止了![](/assets/wq5215123import.png)

我们可以使用 `$ docker ps -a` 查看全部容器，并且用 `$ docker start fuck` 重新启动它。![](/assets/64556import.png)

---

### exec： 直接从容器中运行命令

注意，该命令只能对已启动的容器使用。所以我们优先启动容器。

![](/assets/123123123123import.png)

上图中，我们先启动了容器fuck，然后输出本机的pwd，是在/root下，再从容器中输入命令pwd，输出了/

---

### 与容器交互并且退出，而不停止容器

我们发现docker列表中有一个COMMAND字段，值为"/bin/bash"。它是什么意思呢？

事实上，它表示如果我们不使用任何参数，那么它容器默认执行 "/bin/bash"命令，从而我们可以进入终端命令行。

既它是一个默认的命令。那么我们可以根据这个特性，和exec命令结合，使得在不关闭容器的情况下和容器交互。

（注意，这里必须加入 -i -t 参数）

> $ docker exec -i  -t fuck /bin/bash

![](/assets/12312351import.png)

我们发现，退出之后容器仍然在运行。


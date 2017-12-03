正式环境下，我们很少直接使用第三方提供的镜像。因为这可能是不安全的，不全面的，又或者是过于冗余的。

所以通常都是自己基于官方的镜像来搭建的一个镜像，从这节课开始我们将基于Centos镜像学习搭建一个自己的镜像。

---

先删除上节课我们创建的镜像。

> container是images运行时的的状态。docker对于运行过的image都保留一个状态（container），可以使用命令docker ps来查看正在运行的container，对于已经退出的container，则可以使用docker ps -a来查看。 如果你退出了一个container而忘记保存其中的数据，你可以使用docker ps -a来找到对应的运行过的container使用docker commit命令将其保存为image然后运行。

**1、查看所有运行中的镜像**

> $ docker ps

![](/assets/2312312321import.png)

**2、停止镜像**

> $ docker stop &lt;CONTAINER ID&gt;

![](/assets/676776import.png)

**3、查看所有镜像**

再次使用 `$ docker ps` 发现镜像列表已经空空如也了。难道是镜像被删除了吗？

当然不是。只是停止运行了。我们需要加入 -a 来查看所有的镜像

> $ docker ps -a

![](/assets/32525import.png)

---

先从阿里云docker仓库中搜索Centos，并且找到官方认证的源![](/assets/65223import.png)

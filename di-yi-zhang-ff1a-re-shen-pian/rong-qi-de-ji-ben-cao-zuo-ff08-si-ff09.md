这节课我们将下载到宿主机的JDK，拷贝到容器中去。

本节课我们将创造的镜像，是基于上节课 centos:httpd 镜像（该镜像也是基于 centos 官方镜像搭建）

在真实开发时，我们搭建流程中也是这样的，先有一个纯净（centos），再做一些基本工作（添加httpd、jdk、redis之类）。

然后再一次叠加叠层。实战的镜像就是这样一步一步的搭建起来的。这样我们既拥有一些高级的镜像，也拥有一些底层的镜像。

![](/assets/34345345import.png)

---

### 1、下载jdk（Java SE Development Kit）

前往java官方下载地址

[http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

![](/assets/65555import.png)![](/assets/zasdijijaisdj2183import.png)

注意，你必须按照此步骤来下载，否则无法正常解压：

1. 点击Accept License Agreement；
2. 点击 linux-tar-gz 版本，等待下载；
3. 从下载列表中复制下载链接，然后取消下载。

拿到下载链接，我们就可以使用wget命令下载了。

```
$ wget <下载地址>
```

### ![](/assets/123123123.png)

下载完成后，使用tar命令解压

```
$ tar zxvf <目标文件>
```

![](/assets/1212123123import.png)

将jdk-9.0.1放置在/usr/local下（UNIX规范），然后我们将jdk配置到环境变量中去。

```
$ mv jdk-9.0.1 /usr/local
$ vim /etc/profile
```

修改 /etc/profile ，加入以下内容

**请注意，笔者的文件夹名为jdk-9.0.1，根据不同版本，名字可能会不同，请根据实际情况配置。**

```
export JAVA_HOME=/usr/local/jdk-9.0.1
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
```

让 /etc/profile 立即生效（注意 . 和 /etc/profile 之间有空格）

```
$  . /etc/profile
```

### 2、创建 Dockerfile

新建 build-jdk 文件夹和 Dockerfile 文件，并且把 /usr/local/jdk-9.0.1 复制一份放进去

```
$ mkdir build-jdk && cd build-jdk
$ cp -r /usr/local/jdk-9.0.1 /root/build-jdk
$ vim Dockerfile
```

* COPY：将本地的内容拷贝进镜像指定文件夹中；
* ENV：设置容器的环境变量；
* CMD：容器启动时默认执行的语句。

```js
FROM centos:httpd 
COPY ./jdk-9.0.1 /usr/local/jdk-9.0.1
ENV JAVA_HOME=/usr/local/jdk-9.0.1
ENV PATH $JAVA_HOME/bin:$PATH
ENV CLASSPATH .:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
CMD /usr/sbin/init
```

**请注意，这里的jdk-9.0.1 必须是和 Dockerfile 文件同目录**

![](/assets/45346import.png)

### 3、开始构建镜像

```
$ docker build -t centos:jdk .
```

![](/assets/141142123import.png)

### 3、运行容器

为了方便演示，已经将上节课所有的容器都删除了，当然你可以不删除，但需要映射其他端口。否则会一样使用8080端口是不行的

```
$ docker run --privileged -d -p 8080:80 --name  myjdk -v /root/myweb:/var/www/html centos:jdk
```

![](/assets/231234342234342import.png)

启动成功之后，我们依然访问一下浏览器，确保 Apache 还是正常运行的。

![](/assets/23123123123import.png)

然后再来看看 jdk 的情况，我们进入容器内部，查看jdk版本（我们刚刚已经通过Dockerfile将jdk设置到容器的环境变量中了）

```bash
$ docker exec -it myjdk /bin/bash
$ java -version
java version "9.0.1"
Java(TM) SE Runtime Environment (build 9.0.1+11)
Java HotSpot(TM) 64-Bit Server VM (build 9.0.1+11, mixed mode)
```

![](/assets/16735468import.png)

---

### 排坑

1、解压.tar.gz出错

> gzip: stdin: not in gzip format tar: /
>
> Child returned status 1
>
> tar: Error is not recoverable: exiting now

注意，你必须按照此步骤来下载，否则无法正常解压：

1. 点击Accept License Agreement；
2. 点击 linux-tar-gz 版本，等待下载；
3. 在下载列表中复制下载链接，然后取消下载。

拿到下载链接，我们就可以使用wget命令下载了。

```
$ wget <下载地址>
```




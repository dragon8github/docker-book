这节课我们将下载到本地的JDK，拷贝到容器中去。

### 1、下载jdk（Java SE Development Kit）

前往java官方下载地址

[http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

![](/assets/65555import.png)![](/assets/3333import.png)

你需要点击Accept，然后点击linux-tar-gz版本。等待下载，再从资源中复制下载链接

接下来就可以使用wget命令下载了

> $ wget [http://download.oracle.com/otn-pub/java/jdk/9.0.1+11/jdk-9.0.1\_linux-x64\_bin.tar.gz?AuthParam=1512527311\_ae7d1cf8bc60fd3f29f0baea498cb2a3](http://download.oracle.com/otn-pub/java/jdk/9.0.1+11/jdk-9.0.1_linux-x64_bin.tar.gz?AuthParam=1512527311_ae7d1cf8bc60fd3f29f0baea498cb2a3)

### ![](/assets/123123123.png)

下载完成后，使用tar命令解压

> $ tar zxvf &lt;.tar.gz压缩文件&gt;

![](/assets/1212123123import.png)

将jdk-9.0.1放置在/usr/local下（规范），然后我们将jdk配置到环境变量中去。

> $ mv jdk-9.0.1 /usr/local
>
> $ vim /etc/profile

修改 /etc/profile ，加入以下内容

> export JAVA\_HOME=/usr/local/jdk-9.0.1
>
> export PATH=$JAVA\_HOME/bin:$PATH
>
> export CLASSPATH=.:$JAVA\_HOME/lib/dt.jar:$JAVA\_HOME/lib/tools.jar

让 /etc/profile 立即生效

> $ . /etc/profile

### 2、创建 Dockerfile

本节课我们将创造的镜像，是基于上节课centos:httpd镜像（该镜像也是基于 centos 官方镜像搭建）

在真实开发时，我们搭建流程中也是这样的，先有一个纯净（centos），再做一些基本工作（添加httpd、jdk、redis之类）。

然后再一次叠加叠层。实战的镜像就是这样一步一步的搭建起来的。

![](/assets/34345345import.png)

新建Dockerfile

> FROM centos:httpd  COPY jdk-9.0.1 /usr/local/jdk-9.0.1
>
> ENV JAVA\_HOME=/usr/local/jdk-9.0.1
>
> ENV PATH $JAVA\_HOME/bin:$PATH
>
> ENV CLASSPATH .:$JAVA\_HOME/lib/dt.jar:$JAVA\_HOME/lib/tools.jar
>
> CMD /usr/sbin/init

---

### 排坑

> 1、解压.tar.gz出错gzip: stdin: not in gzip format tar: /Child returned status 1 tar: Error is not recoverable: exiting now

可能是资源为html导致的，也就是说你下载错了~


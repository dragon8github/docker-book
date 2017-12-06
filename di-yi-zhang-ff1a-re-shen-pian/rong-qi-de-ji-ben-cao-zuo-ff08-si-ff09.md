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

---

### 排坑

> 1、解压.tar.gz出错gzip: stdin: not in gzip format tar: /Child returned status 1 tar: Error is not recoverable: exiting now

可能是资源为html导致的，也就是说你下载错了~


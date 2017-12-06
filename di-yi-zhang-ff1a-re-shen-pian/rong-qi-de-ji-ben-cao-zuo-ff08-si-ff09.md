这节课我们将下载到本地的JDK，拷贝到容器中去。

### 1、下载jdk（Java SE Development Kit）

前往java官方下载地址

[http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

![](/assets/65555import.png)![](/assets/3333import.png)

你需要点击Accept，然后点击linux-tar-gz版本。等待下载，再从资源中复制下载链接

接下来就可以使用wget命令下载了

> $ wget [http://download.oracle.com/otn-pub/java/jdk/9.0.1+11/jdk-9.0.1\_linux-x64\_bin.tar.gz?AuthParam=1512527311\_ae7d1cf8bc60fd3f29f0baea498cb2a3](http://download.oracle.com/otn-pub/java/jdk/9.0.1+11/jdk-9.0.1_linux-x64_bin.tar.gz?AuthParam=1512527311_ae7d1cf8bc60fd3f29f0baea498cb2a3)

### ![](/assets/123123123.png)

### 2、创建 Dockerfile



---

### 排坑

> 1、解压.tar.gz出错gzip: stdin: not in gzip format tar: /Child returned status 1 tar: Error is not recoverable: exiting now

可能是资源为html导致的，也就是说你下载错了~


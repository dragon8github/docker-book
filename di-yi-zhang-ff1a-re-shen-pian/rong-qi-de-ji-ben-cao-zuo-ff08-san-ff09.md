### 怎么把我们写好的网站文件塞入容器（以php + apache为例）？

apache的配置文件存放目录默认在：/etc/httpd/conf/httpd.conf

我们先进入容器内部，然后打开该配置文件夹。

> $ docker exiec -i -t myhttpd /bin/bash
>
> $ cat /etc/httpd/conf/httpd.conf

然后找到 DocumentRoot 关键字，发现站点目录在 /var/www/html 下

![](/assets/353import.png)

在apache站点目录下新建一个index.html，然后在外部浏览器中访问看看情况

> $ cd /var/www/html
>
> $ ls
>
> $ echo 123 &gt; index.html

![](/assets/5412import.png)

---

### 通过挂载实现容器和主机间的数据共享

you need stop and remove the container

> $ docker stop myhttpd
>
> $ docker rm myhttpd




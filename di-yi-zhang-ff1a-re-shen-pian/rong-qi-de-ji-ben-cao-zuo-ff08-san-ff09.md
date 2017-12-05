### 怎么把我们写好的网站文件塞入容器（以php + apache为例）？

apache的配置文件存放目录默认在：/etc/httpd/conf/httpd.conf

我们先进入容器内部，然后打开该配置文件夹。

> $ docker exiec -i -t myhttpd /bin/bash
>
> $ cat /etc/httpd/conf/httpd.conf

然后找到 DocumentRoot 关键字，发现站点目录在/var/www/html下

![](/assets/353import.png)


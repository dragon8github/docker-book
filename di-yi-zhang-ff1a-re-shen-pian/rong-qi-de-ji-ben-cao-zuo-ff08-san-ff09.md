### 手动在进入容器，在apache中新建一个测试页面

我们先进入容器内部，然后打开apache配置文件。

apache的配置文件存放目录默认在：/etc/httpd/conf/httpd.conf

> $ docker exec -i -t myhttpd /bin/bash
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

### （以php + apache为例）怎么把我们写好的网站文件塞入容器中？

**答案是通过挂载将主机的数据（文件夹/文件）映射到容器中去，实现数据共享。    
**

> **请注意，映射等于同步。当映射完成之后，容器中被映射的内容也被替换掉。所以应该先对容器中映射的文件夹做好备份。**
>
> 同步的效果就是：当主机修改时，容器也会跟着修改，当容器修改时，主机也会跟着修改。
>
> 但目前发现文件夹可以同步，而文件不能同步。只在首次启动时会同步。不知为何需要进一步研究。

you need to stop and remove the container at first

> $ docker stop myhttpd
>
> $ docker rm myhttpd

create a folder and named it \_myweb ，\_then create html file, what every entry something word in that. just like that:

> $ pwd
>
> /root
>
> $ mkdir myweb
>
> $ cd myweb
>
> $ echo fuck &gt; index.html

so，we still  run the container just like before time，but this time ,we add some para in the order.

* **-v**：the left part is our servers path（/root/myweb），the right part is in the docker container centos servers path（/var/www/html）。

> $ docker run --privileged -d -p 8080:80 --name  myhttpd -v /root/myweb:/var/www/html centos:httpd /usr/sbin/init

review the web again， just like that！！！

![](/assets/656456465import.png)


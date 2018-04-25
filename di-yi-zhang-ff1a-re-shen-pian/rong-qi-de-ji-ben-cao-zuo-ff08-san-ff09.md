### 📦 手动在进入容器，在Apache中新建一个测试页面

我们先进入容器内部，然后打开 Apache 配置文件。

Apache 的配置文件存放目录默认在：/etc/httpd/conf/httpd.conf

```
$ docker exec -i -t myhttpd /bin/bash
$ cat /etc/httpd/conf/httpd.conf
```

然后找到 DocumentRoot 关键字，发现站点目录在 /var/www/html 下![](/assets/353import.png)在apache站点目录下新建一个index.html

```
$ echo 123 > /var/www/html/index.html
```

在浏览器中访问看看情况

![](/assets/5412import.png)

---

### 🍁 怎么把我们写好的网站文件塞入容器中？（以 Apache 为例）

答案是将宿主机的文件夹/文件映射到容器中去，实现数据共享。

🔔 请注意，映射等于同步。当宿主机修改时，容器也会跟着修改，当容器修改时，主机也会跟着修改。

当容器启动时，容器中被映射的内容也被替换掉。所以应该先对容器中映射的文件夹做好备份。

宿主机文件复制到容器中：**$ docker cp &lt;宿主机文件路径&gt; &lt;容器id/容器name&gt;:&lt;容器路径&gt;，**示例如下：

```
$ docker cp /root/php/www/index.html ca798fee7920:/var/www/
```

将容器中的文件复制到宿主机中：**$ docker cp &lt;容器id/容器name&gt;:&lt;文件路径&gt; &lt;宿主机路径&gt;，**示例如下：

```
$ docker cp ca798fee7920:/var/www/ /root/php/
```

目前发现文件夹可以一直保持这种同步，而文件却仅在初次启动容器时同步，而后修改就不同步了。需要进一步研究。

1、让我们先删除刚刚的容器

```
$ docker stop myhttpd && docker rm myhttpd
```

2、创建一个文件夹 myweb，用来保存网站内容，并新建 index.html 用来演示

```
$ mkdir myweb
$ echo fuck > myweb/index.html
```

3、启动容器

* -v：冒号左边是我们的宿主机资源路径（/root/myweb），冒号右边是容器资源路径（/var/www/html）。请注意当启动完成之后，容器路径中的资源将会被宿主机的资源替换掉。所以最好先做好备份，如果需要映射多个资源路径，执行多次-v即可；
* -d：后台运行容器，否则会卡死当前会话；
* --privileged：给容器加特权，否则什么事都做不了；
* -p：和本机映射的端口，冒号左边是宿主机的端口，冒号右边是容器暴露出来的端口；
* --name：容器的别名。
* /usr/sbin/init：启动容器后，容器第一句执行的命令。但作用不明，可能是初始化吧。

```
$ docker run --privileged -d -p 8080:80 --name  myhttpd -v /root/myweb:/var/www/html centos:httpd /usr/sbin/init
```

4、浏览网页

![](/assets/656456465import.png)


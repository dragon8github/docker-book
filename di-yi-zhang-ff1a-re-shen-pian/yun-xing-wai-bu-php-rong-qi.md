docker安装时默认创建了docker用户组，将普通用户加入 docker 用户组就可以不使用sudo来操作docker

> $ sudo usermod -aG docker root

\( 这里root成你自己的用户名\)

注意：光加入还不行，要么重i新登录，要么执行下面命令改变当前用户的有效群组。

> $ newgrp - docker

---

### 内置镜像

你可以理解为很多贴心的老外或国人帮你制作好的环境。你可以直接使用

[https://hub.docker.com/](https://hub.docker.com/)

然而由于国情，你根本下载不了。于是我们要配置国内镜像，我们可以用阿里云

### 使用阿里云的容器镜像服务

[https://dev.aliyun.com/search.html](https://dev.aliyun.com/search.html)

### 使用阿里云的镜像加速器

点击右上角的管理中心。假设你已经注册并登录阿里云的镜像中心。我们就可以使用阿里云的镜像加速器

![](/assets/12import.png)

阿里云的镜像加速器传送门：[https://cr.console.aliyun.com/\#/accelerator](https://cr.console.aliyun.com/#/accelerator)

![](/assets/8import.png)

请注意，每个人的加速器地址都不一样，所以需要根据自己的加速器地址来进行配置。

```py
sudo mkdir -p /etc/docker     #创建一个文件夹 叫做docker
sudo tee /etc/docker/daemon.json <<-'EOF'   #利用tee 命令把下面的配置写入 daemon.json
{
  "registry-mirrors": ["https://xxxx.mirror.aliyuncs.com"]  #这里要改成你们自己的 地址
}
EOF

sudo systemctl daemon-reload  # 重载所有修改过的配置文件,扫描新的或有变动的单元
sudo systemctl restart docker  # 重启docker
```

### 开始下载一个镜像

回到阿里云的镜像仓库：[https://dev.aliyun.com/search.html](https://dev.aliyun.com/search.html)

进行搜索 ，譬如输入关键字：PHP

我们选取一个下载次数还算多的镜像作为学习测试：[https://dev.aliyun.com/detail.html?repoId=1666](https://dev.aliyun.com/detail.html?repoId=1666)

根据提示执行命令：

> $ docker pull registry.cn-hangzhou.aliyuncs.com/lxepoo/apache-php5

![](/assets/21import.png)下载完成之后，使用以下命令命令查看镜像

> $ docker images

### ![](/assets/2312import.png)

---

### 镜像已经有了，接下来怎么办？

想想虚拟机的话，肯定要启动我们的虚拟机嘛~~~

> $ docker run -d -p 8080:80 &lt;名称或ID&gt;

run 把我们的镜像放入容器中（只在第一次运行\)

* -d 启动容器后台运行，并返回ID；
* -p 把容器的80端口映射到宿主机的8080；

> $ docker run -d -p 8080:80 e121d5f99e1e

为什么我们知道容器中启动的端口是80？没有为什么，因为作者就是这样设置的。并且可以通过该镜像的文档看出来。

![](/assets/123123import.png)

---

### 查看所有运行中容器

> $ docker ps

![](/assets/21331import.png)

---

一切准备就绪，开始访问我们的站点服务器。但在这之前需要跨过几个坑先。

**1、【IPv4forwarding is disabled.Networkingwill not work.】**

解决办法：\(Linux内核参数配置文件，可在运行时修改某些内核参数，使之永久生效\)

> $ sudovi/etc/sysctl.conf

加入内容 `net.ipv4.ip_forward=1`

保存并退出后 执行

> $ systemctlrestart network

**2、阿里云的安全组配置**

请查看[《第零章：阿里云上购买并配置Centos7》](https://dragon8github.gitbooks.io/docker/content/a-li-yun-shang-gou-mai-he-pei-zhi-centos7.html)

**3、防火墙放行8080端口示例**

> $ iptables -I INPUT -p tcp --dport 8080 -j ACCEPT

现在，正常在浏览器上访问我们的 ip + 8080端口，如果可以看到php信息页面，就说明成功了。具体如下

![](/assets/123123123import.png)


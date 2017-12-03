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

[https://dev.aliyun.com/search.html](https://dev.aliyun.com/search.html)

然后点击右上角的管理中心。假设你已经注册并登录阿里云的镜像中心。我们就可以使用阿里云的镜像加速器

![](/assets/12import.png)

[https://cr.console.aliyun.com/\#/accelerator](https://cr.console.aliyun.com/#/accelerator)

![](/assets/8import.png)

请注意，每个人的加速器地址都不一样，所以需要根据自己的加速器地址来进行配置。

```bash
sudo mkdir -p /etc/docker     #创建一个文件夹 叫做docker
sudo tee /etc/docker/daemon.json <<-'EOF'   #利用tee 命令把下面的配置写入 daemon.json
{
  "registry-mirrors": ["https://xxxx.mirror.aliyuncs.com"]  #这里要改成你们自己的 地址
}
EOF

sudo systemctl daemon-reload  # 重载所有修改过的配置文件,扫描新的或有变动的单元
sudo systemctl restart docker  # 重启docker
```




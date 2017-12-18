# 1、修改 Docker service 的配置

```bash
$ cd /usr/lib/systemd/syste
$  vim docker.service
```

![](/assets/2131231import.png)

---

把原本是 ExecStart=/usr/bin/dockerd  这一行 注释掉 改成

> \# ExecStart=/usr/bin/dockerd

ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:2375 -H unix://var/run/docker.sock

![](/assets/15134123import.png)

---

### 重启 Docker Service 使配置生效

第一步是让守护进程重新装载。第二步是重启服务

```bash
$ systemctl daemon-reload
$ systemctl restart docker
```

---

### 查看是否正常配置并且正常开启

```bash
$ ps -ef | grep docker
```

![](/assets/231231251323import.png)

这样一来，我们就可以使用TCP的方式对Docker进行操作和连接了。

---

### python 连接 Docker 尝试

官网推荐了pthon版本和Go版本、HTTP方式的。我们使用python，比较简单。

> [https://docs.docker.com/develop/sdk/\#python-sdk](https://docs.docker.com/develop/sdk/#python-sdk)
>
> [https://docs.docker.com/develop/sdk/examples/](https://docs.docker.com/develop/sdk/examples/)

1、使用 pip 安装 python使用 docker 必备的插件，当然首先要确定你安装了pip.

第一命令是检查你的python是否自带pip（python某个版本开始，已经自带pip了。如果没有请自己扩展下载）

第二命令是从阿里云镜像库中下载我们的 python docker 模块

```bash
$ python -m pip help
$ python -m pip install --upgrade pip
$ python -m pip install docker -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
```

测试一下是否能正常引入docker，没有报错就是成功。

![](/assets/123135134134import.png)

---

2、如果docker是部署在阿里云服务器中，那么添加阿里云安全组配置。添加2375端口访问权。

![](/assets/1243263467import.png)

---

3、防火墙开启2375端口访问

```bash
$ iptables -I INPUT -p tcp --dport 2375 -j ACCEPT
```

---

4、python代码编写

```py
import docker

# iptables -I INPUT -p tcp --dport 2375 -j ACCEPT  确保防火墙放行2375端口 
# 如果docker是部署在阿里云服务器中，切记必须将安全组规则开启2375端口的访问
client = docker.DockerClient(base_url='tcp://119.23.111.13:2375')
images=client.images.list()
print(images)
```

成功打印出我们docker所有的容器内容！！

![](/assets/123124637467import.png)


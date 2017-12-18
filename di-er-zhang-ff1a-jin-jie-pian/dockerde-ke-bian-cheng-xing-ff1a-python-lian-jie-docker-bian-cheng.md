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

使用 pip 安装 python使用 docker 必备的插件，当然首先要确定你安装了pip.

```bash
$ python -m pip help
$ python -m pip install --upgrade pip
$ python -m pip install docker -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
```




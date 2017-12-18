# 1、修改 Docker service 的配置

> $ cd /usr/lib/systemd/syste
>
> $  vim docker.service

![](/assets/2131231import.png)

---

把原本是 ExecStart=/usr/bin/dockerd  这一行 注释掉 改成

> \#ExecStart=/usr/bin/dockerd

ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:2375 -H unix://var/run/docker.sock

![](/assets/15134123import.png)

---

### 重启 Docker Service 使配置生效

第一步是让守护进程重新装载。第二步是重启服务

> $ systemctl daemon-reload
>
> $ systemctl restart docker

---

### 查看是否正常配置并且正常开启

> ps -ef \| grep docker

![](/assets/231231251323import.png)

这样一来，我们就可以使用TCP的方式连接Docker了。


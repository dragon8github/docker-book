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

> $ systemctl daemon-reload

---




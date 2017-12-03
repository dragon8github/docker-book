### 传送门

官方文档：[https://docs.docker.com/](https://docs.docker.com/)

官方Centos版本安装教程：[https://docs.docker.com/engine/installation/linux/docker-ce/centos/](https://docs.docker.com/engine/installation/linux/docker-ce/centos/)

下载地址：[https://docs.docker.com/engine/installation/](https://docs.docker.com/engine/installation/)

阿里云推荐的源信息，譬如centos7的yum源和ubuntu下的apt-get源设置：

[https://yq.aliyun.com/articles/110806?spm=a2c1q.8351553.0.0.11b720beQRyGTx](https://yq.aliyun.com/articles/110806?spm=a2c1q.8351553.0.0.11b720beQRyGTx)

---

CE和EE的区别：前者是社区版，免费试用；后者是企业版。需要购买版权。

我们选择最新的版本：17.09社区版![](/assets/6import.png)

进入之后，我们选择CE社区版

![](/assets/import.png)

就可以看到官方推荐的安装教程了。下面我们来实践一下

---

### 安装一些基本依赖软件

注意：默认是 普通用户,不要用root

为了演示方便，下面的命令 前面一律要加sudo

> $ yum install -y yum-utilsdevice-mapper-persistent-data lvm2

为了使用 yum-config-manager 需要先安装一下这个

> $ yum -y install yum-utils

这一步设置即将安装的是稳定版仓库

> $ yum-config-manager --add-repo [https://download.docker.com/linux/centos/docker-ce.repo](https://download.docker.com/linux/centos/docker-ce.repo)

这一步是可选的,我们不加（edge月更新仓库, Edge gives you new features every month）

> $ yum-config-manager --enable docker-ce-edge




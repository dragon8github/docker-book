我们pull了一个纯净镜像，如果要部署网站、安装一些软件的话， 有啥办法？

1、硬来 

利用attach进入，各种yum，各种安装 \(你会发现好多权限问题\)

2、Dockerfile  

今天我们来看一下如何利用Dockerfile创建一个镜像

Dockerfile是由一系列命令和参数构成的脚本，这些命令应用于基础镜像并最终创建一个新的镜像。

官方文档：https://docs.docker.com/engine/reference/builder/\#usage

---

### 来个案例

譬如我们是PHP开发人员，可能要用到apache\(httpd\).我们希望直接构建出一个环境容器

接下来我们创建一个空文件夹，CD进入。然后创建一个文件叫做Dockerfile\(注意大小写\)，插入内容如下：

> FROM centos:latest
>
> RUN yum -y install httpd  
>
> RUN  systemctl enable httpd.service 
>
> EXPOSE 80




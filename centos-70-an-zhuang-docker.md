对于使用Centos 7 的用户，直接运行如下命令，就可安装最新版本的Docker

```
sudo yum install docker -y
```

安装成功！

![](/assets/21312312312312.png)

### 启动docker服务，并把docker服务注册为开机启动。

```
sudo service docker start
sudo chkconfig docker on
```

![](/assets/12312312asadsasdasd.png)

### 运行Docker镜像

执行以下命令将直接从DockerHub上启动“hello world"Web服务器示例。

```
$ docker run -p 8080:8080 cloudnativego/book-hello
[negroni]  listening  on  :8080
[negroni]  Started  GET  I
[negroni]  Completed  200  OK  in  71 . 688µs
```

![](/assets/3415651515sdfsd.png)

如果是第一次执行，那么将看到许多进度报告，表明正在下载Docker镜像。

命令将Docker镜像内部的8080端口映射到外部的8080端口上。

如上所述，Docker提供了网络隔离，所以除非明确定义了来自外部的流量在容器内的路由规则，否则隔离本质上将是一个防火墙。

由于我们已经定义了内部和外部的端口映射关系，因此可以通过Docker机器的IP地址加上8080端口进行访问。


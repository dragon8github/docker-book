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

```
$ docker run -p 8080:8080 cloudnativego/book-hello
[negroni]  listening  on  :8080
[negroni]  Started  GET  I
[negroni]  Completed  200  OK  in  71 . 688µs
```

![](/assets/3415651515sdfsd.png)


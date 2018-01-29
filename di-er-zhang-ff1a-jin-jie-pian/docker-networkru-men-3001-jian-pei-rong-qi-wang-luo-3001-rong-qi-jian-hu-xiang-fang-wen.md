### Network

📘 文档地址：[https://docs.docker.com/engine/reference/commandline/network/\#usage](https://docs.docker.com/engine/reference/commandline/network/#usage)

首先使用`$ docker network ls`看一下，

默认会创建桥接模式 bridge（当我们启动容器时，默认会加入bridge这个网络）。

其中 \*\_default 是我们使用 Docker Compose 创建时默认添加的。

![](/assets/阿萨德import.png)

我们可以通过`$ docker network inspect cc_default`来查看该里面到底有什么内容

![](/assets/az123asdasimport.png)

我们发现，通过docker-compose启动的两个java容器，他们默认是同一网关的，

也就是说，这两个容器之间可以通过ip的方式进行互通。

🔎 举个例子，我们随便进入其中一个java容器中`$ docker exec -it web1 /bin/bash`

然后使用 `$ cat /etc/hosts`来查看网络配置。再通过ping、curl等命令测试。发现他们的确实是处于同一网关的。

反过来说，如果容器与容器之间不在统一网关，他们就无法互相访问。

🍒  那么，在非 Docker Compose 来创建的容器 与 容器之间，如何建立统一网关呢？

这就是我们本节课将要学到的内容。

---






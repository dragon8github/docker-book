> Docker 容器编排的工具， 可以配置并启动多个容器，适合复杂业务场景

文档地址

> [https://docs.docker.com/compose/overview/](https://docs.docker.com/compose/overview/)

安装 \(一切根据官方文档来 ）

> $ sudo curl -L [https://github.com/docker/compose/releases/download/1.18.0/docker-compose-\`uname](https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname) -s\`-\`uname -m\` -o /usr/local/bin/docker-compose

下载完成之后，要为docker-compose 赋予可执行权限

> $ sudo chmod +x /usr/local/bin/docker-compose

然后测试一下安装是否成功

> $  docker-compose -v
>
> docker-compose version 1.18.0, build 8dd22a9






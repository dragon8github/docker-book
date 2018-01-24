> Docker 容器编排的工具， 可以配置并启动多个容器，适合复杂业务场景

### 📘 文档地址

> [https://docs.docker.com/compose/overview/](https://docs.docker.com/compose/overview/)

### 🏊 安装 

> $ sudo curl -L [https://github.com/docker/compose/releases/download/1.18.0/docker-compose-\`uname](https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname) -s\`-\`uname -m\` -o /usr/local/bin/docker-compose

### 🔔 赋予权限

> $ sudo chmod +x /usr/local/bin/docker-compose

### 👆 测试

> $  docker-compose -v
>
> docker-compose version 1.18.0, build 8dd22a9

---

### 📀 docker-compose.yml

引导教程

> [https://docs.docker.com/compose/gettingstarted/\#step-1-setup](https://docs.docker.com/compose/gettingstarted/#step-1-setup)

支持的相关参数列表 ，要多查阅多试

> [https://docs.docker.com/compose/compose-file/\#build](https://docs.docker.com/compose/compose-file/#build)

相关yaml检查的在线工具

> [http://www.yamllint.com/](http://www.yamllint.com/)

### 💐 Example

1、创建一个空文件夹，叫做composetest

2、创建一个docker-compose.yml 文件,拷贝如下内容

```js
ervices: 
  web1: 
    container_name: web1
    image:"centos:jdk"
    ports: 
      - "8080:80"
    privileged: true
    volumes: 
      - "/home/shenyi/nginx/web1/:/var/www/html/"
  web2: 
    container_name: web2
    image: "centos:jdk"
    ports: 
      - "8081:80"
    privileged: true
    volumes: 
      - "/home/shenyi/nginx/web2/:/var/www/html/"
version: "3"
```




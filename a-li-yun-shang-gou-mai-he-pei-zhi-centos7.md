### 配置安全组，让外部可以访问云服务器上的地址

左侧菜单 -&gt; 云服务器ECS -&gt; 左侧内部菜单 -&gt; 实例 -&gt; 右侧服务器列表 -&gt; 管理 -&gt; 左侧内部菜单 -&gt; 本实例安全组 -&gt; 配置规则

![](/assets/1import.png)譬如我想开通8080端口给外界访问。

1、点击右上角【添加安全组规则】

2、端口范围选择8080/8080，授权对象直接设置为 0.0.0.0/0 即可

##### ![](/assets/65464import.png)

##### 3、服务器防火墙放行8080端口示例

> $ iptables -I INPUT -p tcp --dport 8080 -j ACCEPT





### 修改系统盘配置，譬如我想从Centos6 升级到 Centos7

1、先停止

2、进入实例的管理界面

![](/assets/2import.png)

### xshell 远程登陆

1、首先去xshell的官网下载软件：[http://www.netsarang.com/products/xsh\_overview.html](http://www.netsarang.com/products/xsh_overview.html)

2、进入实例，查看服务器列表，找到ip地址（公）

![](/assets/3import.png)3、在xshell上新建会话，并在主机栏上填上你的ip

![](/assets/4import.png)4、设置你服务器的登录账号和密码即可（譬如root、mpP?）

![](/assets/5import.png)


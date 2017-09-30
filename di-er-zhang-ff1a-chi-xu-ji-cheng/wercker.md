> Wercker 官网：[https://app.wercker.com/](https://app.wercker.com/)
>
> Wercker-cli 官网：[http://www.wercker.com/cli/install/osx](http://www.wercker.com/cli/install/osx)

### Wercker-cli 下载

请用root管理员权限输入以下命令：

```
curl -L https://s3.amazonaws.com/downloads.wercker.com/cli/stable/linux_amd64/wercker -o /usr/local/bin/wercker
```

下载完成之后，添加权限：

```
chmod u+x /usr/local/bin/wercker
```

然后测试一下是否一切正常可用：

```
$ wercker version
```

![](/assets/123123d55dd8saassa09as9jcjxcxcx.png)



### 创建Wercker 的配置文件

wercker配置文件是一个YAML文件。AML对空格和制表符非常敏感，如果关闭了间距，有些内容将会损坏。大多数编辑器，包括Emacs和Atom，都有可以处理YAML的插件。如果无法确定YAML的格式，又想要进行语法验证，可以访问一个在线YAML验证程序，地址是h饥p://www.yamllint.corn/。这个工具己经拯救了很多人。

```
http://www.yamllint.com/
```

Wercker配置文件包含三个部分，对应可用的三个主要流水线：

* Dev  ：定义了开发流水线的步骤列表。
* Build  ：定义了在Wercker构建期间要执行的步骤和脚本的列表。
* Deploy：定义构建的部署方式和位置。




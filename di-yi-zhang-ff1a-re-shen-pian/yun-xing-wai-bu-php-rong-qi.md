docker安装时默认创建了docker用户组，将普通用户加入docker用户组就可以不使用sudo来操作

`docker sudo usermod -aG docker` \( 这里替换成你自己的用户名\) 

注意：光加入还不行，要么重i新登录，要么执行 `$ newgrp - docker `改变当前用户的有效群组。

---




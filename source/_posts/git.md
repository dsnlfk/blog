---
title: git 配置多个SSH-Key
date: 2016-06-16 14:21:18
tag: 
---
"久久配一次，mark一下"

## SSH-Key生成
生成多个SSH注意命名，如：~/.ssh/id_rsa_github
生成过程密码不要设置直接回车两三次就ok
结果生成id_rsa，id_rsa.pub两个文件，把id_rsa.pub中的全部内容添加至git站上
```bash
ssh-keygen -t rsa -C "xxxxxx@xxxxxx.com" -f ~/.ssh/id_rsa
```

## 多个SSH-Key配置
~/.ssh/目录下新建config文件，把下面的配置粘贴修改User为自己账号名即可
```bash
# 預設帳號 （個人帳號）
Host github.com
    HostName github.com
    User xxxxxx@xxxxxx.com
    IdentityFile ~/.ssh/id_rsa_github

# 工作帳號
Host http://git.ucweb.local/
   HostName http://git.ucweb.local/
   User xxxxxx@xxxxxx.com
   IdentityFile ~/.ssh/id_rsa
```
---
title: Connecting to GitHub with SSH
date: 2019-07-07 11:21:23
categories: GitHub #分类
tags: [github,ssh] 
description: 
---

使用 SSH 协议可以连接远程服务器和服务并向它们验证。 利用 SSH 密钥可以连接 GitHub，而无需在每次访问时提供用户名或密码。

> 使用的环境是windows 系统 

<!--more-->

### 配置你的用户名和邮箱

``` shell
git config --global user.email "your.email@**" 填写你的github注册邮箱
git config --global user.name "yourgithubnname" //你的github用户名，非昵称
```

### 检查存在的SSH keys

- 在Git bash 中 输入`ls -al ~/.ssh` 以查看是否存在现有 SSH 

  ```shell
  ls -al ~/.ssh
  ```

- 检查目录列表以查看是否已经有 SSH 公钥。

  > 默认情况下，公钥的文件名是以下之一：
  >
  > - *id_dsa.pub*
  > - *id_ecdsa.pub*
  > - *id_ed25519.pub*
  > - *id_rsa.pub*

### 生成一个新的SSH key

- 在Git bash 输入 下面命令，your_email@example.com替换为有的GitHub 邮箱

  ```shell
  $ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    Generating public/private rsa key pair.
    Enter file in which to save the key (C:\Users\Administrator/.ssh/id_rsa):
  ```

> 在自定义key的位置时，选择默认即可（C:\Users\Administrator/.ssh/id_rsa）
>
> 这里的没有使用[SSH key passphrases](https://help.github.com/en/articles/working-with-ssh-key-passphrases)  直接回车即可
>
> ``` shell
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
> ```
>
> 使用SSH密钥，如果有人获得对您计算机的访问权限，他们也可以访问使用该密钥的每个系统。要添加额外的安全层，可以向SSH密钥添加密码。您可以使用它`ssh-agent`来安全地保存您的密码，这样您就不必重新输入密码。[Adding your SSH key to the ssh-agent](https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent)

### 将SSH key 添加到Github 账户中

- 将SSH密钥复制到剪贴板

  ``` shell
  $ clip < ~/.ssh/id_rsa.pub # Copies the contents of the id_rsa.pub file to your clipboard
  ```

  > 如果`clip`不起作用，您可以找到隐藏`.ssh`文（C:\Users\Administrator/.ssh/id_rsa)
  >
  > 复制id_rsa.pub中的内容即可

- 在你的Github 页面的右上角，点击个人头像，然后点击 Settings
- 在用户设置中（Personal settings），点击SSH and GPG keys
- 点击 New SSH key or Add SSH key
- 在Title 字段中，为新密钥添加描述性标签，将密钥粘贴到key 字段中
- ,点击添加，如何有提示，输入你的GitHub 密码

### 测试连接

- 在Git Bash 中输入

  ``` shell
  $ ssh -T git@github.com # Attempts to ssh to GitHub
  Hi junqiangni! You've successfully authenticated, but GitHub does not provide shell access.
  ```

>如果出现警告，按照提示输入，即可
>
>如果是 permission denied 信息 [Error: Permission denied (publickey)](https://help.github.com/en/articles/error-permission-denied-publickey).

### 参考

1.https://help.github.com/en/articles/connecting-to-github-with-ssh




---
title: 部署Hexo到github
---


## 1 打开Git Base
在任意位置点击鼠标右键，选择Git Base。

## 2 安装hexo
输入命令:
``` bash
npm install hexo-cli -g
```
注意：-g是指全局安装hexo。

## 3创建Hexo文件夹
安装完成后，在你喜爱的文件夹下（如C:\Hexo），执行以下指令(在C:\Hexo内点击鼠标右键，选择Git Bash)，Hexo 即会自动在目标文件夹建立网站所需要的所有文件。
``` bash
hexo init
```

## 4安装依赖包
``` bash
npm install
```
## 5本地查看
现在我们已经搭建起本地的hexo博客了，执行以下命令(在C:\Hexo)，然后到浏览器输入localhost:4000看看。
``` bash
hexo generate
hexo server
```

## 6注册Github账号
这里不演示了。

## 7创建Repository
创建的时候注意Repository的名字。比如我的Github账号是yourname，那么我应该创建的Repository的名字是：yourname.github.io。

## 8修改配置文件
1
到你刚刚创建的Repository下，找到以下内容：

2
先点击HTTPS，然后复制里面的地址。然后编辑_config.yml文件（在C:\Hexo下）。
``` bash
deploy:
  type: git
  repository: https://github.com/yourname/yourname.github.io.git
  branch: master
```
3
修改文件里面的deploy。其中的repository就改成你刚刚复制的地址。保存这个文件。

## 9设置SSH keys
1
在Git Bash输入以下指令（任意位置点击鼠标右键），检查是否已经存在了SSH keys。
``` bash
ls -al ~/.ssh
```
2
如果不存在就没有关系，如果存在的话，直接删除.ssh文件夹里面所有文件：

3
输入以下指令（邮箱就是你注册Github时候的邮箱）后，回车：
``` bash
ssh-keygen -t rsa -C "yourname@163.com"
```

4
然后它会提示要你输入passphrase（我没有输入直接回车，如果你输入的话，要记得，到时候会用到)。

5
然后键入以下指令：
``` bash
ssh-agent -s
```
6
继续输入指令：
``` bash
ssh-add ~/.ssh/id_rsa
```
7
输入之后，在我这里是出错了，不知道你的有没有出错。

8
如果你的也是这样子出错了的话，就输入以下指令：
``` bash
eval `ssh-agent -s`
ssh-add
```
9
到了这一步，就可以添加SSH key到你的Github账户了。键入以下指令，拷贝Key（先拷贝了，等一下可以直接粘贴）：
``` bash
clip < ~/.ssh/id_rsa.pub
```
10
然后到Github里面，点击右上角的设置图标：

11
在Settings sidebar那里，点击SSH keys：

12
点击Add SSH key：

13
输入Title，作为这个key的描述吧（你可以输入Personal MacBook Air，瞬间高大上）

14
然后这个Key就是刚刚拷贝的，你直接粘贴就好（也可以文本打开以下文件）：

15
点击Add Key：

16
输入你的Github密码即可完成SSH Key的添加。嗯，最后还是测试一下吧，键入以下命令：
``` bash
ssh -T git@github.com
```
17
你可能会看到有警告，没事，输入“yes”就好。

## 10完成部署
最后一步，快要成功了，键入指令：
hexo generate
hexo deploy
OK，我们的博客就已经完全搭建起来了，在浏览器输入（当然，是你的用户名）：
http://yourname.github.io/

注意：每次修改本地文件后，需要键入hexo generate才能保存。每次使用命令时，都要在C:\Hexo目录下。每次想要上传文件到Github时，就应该先键入hexo generate保存之后，再键入hexo deploy。大概成功之后是酱紫的：

4
对了，记住Username是你的Github账号名称，而不是邮箱；Password就是你的Github的密码。

## Tips
hexo现在支持更加简单的命令格式了，比如：
``` bash
hexo g == hexo generate
hexo d == hexo deploy
hexo s == hexo server
hexo n == hexo new
```

## 注意事项
hexo deploy命令显示ERROR Deployer not found : github

deploy的type改成git，然后运行下
``` bash
npm install hexo-deployer-git --save
```
再
``` bash
hexo g
hexo d
```

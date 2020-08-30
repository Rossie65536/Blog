---
title: Hexo+Netlify 搭建博客
date: 2020-08-30 10:58:45
tags: [nodejs,git]
categories: Blog
---

## 前言

本人是在 windows 的操作系统搭建的，以下内容都是对于 windows，文件路径最好不要是中文（因为我也不知道会不会有 bug)，如果是 Linux 或者 Mac 系统，一些地方可以自行修改。

## 开始

首先，要有 nodejs 环境，以及 git。

[nodejs](https://nodejs.org/en/) 和 [git](https://git-scm.com/) 都可以去官网去下载。

然后打开 cmd，执行以下命令，安装 hexo-cli。

```plain
$ npm install -g hexo-cli
```

下载完后找到一个目录（你的博客文件夹就放在该目录下）。接着执行以下命令：

```plain
$ hexo init <yourblog>
$ cd <yourblg>
$ npm install
```

这里的  `<yourblog>` 是你博客的文件夹名称，这样一来，我们的第一步就完成了。

## 部署

你首先要测试以下你本地的博客页面是什么样子的，在你的博客的根目录下，打开 cmd，分别输入以下命令：

```plain
$ hexo g
$ hexo s
```

其中，hexo g 表示生成静态网页，然后 hexo s 表示在本地运行，然后你就可以访问 http://localhost:4000/ 来欣赏自己的博客，如果你要关闭本地服务器的话，那就按 `Ctrl+c`。

这里我们要把本地的博客文件夹传到 [Github]([GitHub](https://github.com/)) 上，如果没有注册的同学可以去注册一下。

打开 git bash，分别输入以下命令：

```plain
$ git config --global user.name "yourname"
$ git config --global user.email "youremail"
```

其中 `yourname` 表示你的用户名（任意的），`youremail` 是你的邮箱名（任意的）。

接着通过 `git init` 命令把你的博客变成 git 可以管理的仓库。

再将所有的文件添加到你的仓库：

```plain
$ git add .
$ git commit -m "Blog"
```

当然这只是将你的博客添加到本地的仓库，你需要将它上传到你的 github 仓库。

### 第1步：创建 SSH Key

在用户主目录下，看看有没有 .ssh 目录，如果有，再看看这个目录下有没有 `id_rsa` 和 `id_rsa.pub` 这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开 git bash，创建 SSH Key：

```plain
 $ ssh-keygen -t rsa -C "youremail"
```

`youremalil` 是你的邮箱。

### 第2步，将 SSH Key 添加到你的 github 账户

登陆 github，打开 Account settings，SSH Keys 页面。

然后，点 Add SSH Key，填上任意 Title，在 Key 文本框里粘贴 `id_rsa.pub` 文件的内容，最后点 Add Key 。

### 第3步 创建一个仓库。

在右上角找到 Create a new repo 按钮，创建一个新的仓库。

在 Repository name 填入 `Blog`，其他保持默认设置，点击 Create repository 按钮，就成功地创建了一个新的 git 仓库。

### 第4步 将博客推送到 github 仓库

首先连接到你的仓库。

```plain
$ git remote add origin git@github.com:yourname/Blog.git
```

其中 `yourname` 表示你的 github 账号名称。

现在你就可以把本地库的所有内容推送到远程库上：

```plain
$ git push -u origin master
```

之后如果你要上传博客，你就可执行以下命令：

```plain
$ git push origin master
```

其实到这里就基本完成了，你只需用将你的博客部署到 Netlify 即可。

使用 Netlify 提供的网页端用户界面。前往[新建一个网站页面](https://app.netlify.com/start)，选择需要关联的 github 库，然后遵循网站提示即可。

## 最后

关于 hexo 的其他操作，这里不详细说明，这里给出 hexo 的[官方文档](https://hexo.io/zh-cn/docs/)，最后祝大家使用愉快 o(*￣▽￣*)ブ。
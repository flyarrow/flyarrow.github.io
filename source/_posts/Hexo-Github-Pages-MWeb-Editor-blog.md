---
title: Hexo(macOS)+Pages(Github)+MWeb(Editor)构建博客系统
tags: [Hexo,Github,MWeb]
categories: [hexo]
date: 2019-12-29 15:00:00
---

今天介绍下本博客系统搭建工具组合. 
1. 本地环境: Hexo , macOS Catalina 
2. 页面托管: GitHub Pages
3. 本地编辑: MWeb , Markdown Editor
<!-- more -->

## macOS 本地环境
需要在macOS本地环境安装: `Git` , `node.js`, `Hexo` 

### 安装 Git

macOS上自带了Git系统, 不需要额外安装, 当然如果需要重新安装, 也可以在[此地址下载](https://github.com/timcharper/git_osx_installer/releases)可安装的`Git.DMG`文件.

打开Mac终端工具, 输入指令查询Git版本号:
```
git --version
```
> git version 2.19.0

### 安装 node.js

直接[官网](https://nodejs.org/zh-cn/)下载, 然后下一步下一步安装完成, node.js和npm都会安装完成.

打开Mac终端工具, 分别输入指令查询`node.js`和`npm`版本

```
node -v
```
> v12.14.0
```
npm -v
```
> 6.13.4

### 安装 Hexo

在终端工具上输入命令稍等片刻完成安装

``` 
sudo npm install -g hexo
```
安装完成后, 输入以下指令查询版本号
```
hexo -v
```
> hexo-cli: 3.1.0
os: Darwin 19.2.0 darwin x64
node: 12.14.0
v8: 7.7.299.13-node.16
uv: 1.33.1
zlib: 1.2.11
brotli: 1.0.7
ares: 1.15.0
modules: 72
nghttp2: 1.39.2
napi: 5
llhttp: 1.1.4
http_parser: 2.8.0
openssl: 1.1.1d
cldr: 35.1
icu: 64.2
tz: 2019c
unicode: 12.1


### 初始化 hexo 并启动服务

在自己用户名目录下, 创建 hexo 文件夹(名字可以自己改), 并进入文件下目录, 执行指令完成初始化

``` 
mkdir hexo   ## 创建hexo文件夹
cd hexo      ## 进入hexo文件夹
hexo init    ## 初始化hexo
npm install  ## 安装相关依赖程序
hexo generate ## 生成静态页面
hexo server  ## 启动hexo服务 
```
此时Hexo服务已经在本机启动, Ctrl+C可以停止服务, 打开本地浏览器, 直接访问 [http://localhost:4000/](http://localhost:4000/), 就可以看到网站.

通过访达工具可以直接浏览 `username/hexo/` 目录, 下面是几个重要文件和文件夹构成

> **_config.yml**  ## [站点配置文件](https://hexo.io/zh-cn/docs/configuration.html), 可以调整里面参数修改站点配置
> **/public/**  ## 站点对外发布时会在此文件夹自动生成网站静态文件, 这些文件将发送给外部托管的服务器, 比如Github
> **/source/_posts/**  ## 这里存储博客文章源文件, 每篇文章对应1个.md文件, 用markdown标记编写的文件通常保存为.md文件, 所谓发布就是把md文件变成 public下的所有站点静态文件 
> **/themes/**  ## 给博客站点安装外观模板就会放在这个文件夹
> **/node_modules/** ## node.js系统文件

-----

## Github 托管环境

需要注册Github账号, 创建Github公开Repository, 在macOS上安装Git部署器, 在设置文件中将macOS-hexo和Github-pages连接起来, 进行发布.

### 创建Github Repository
创建新库的设置页面有3个注意事项
1. Repository name
    - 命名格式必须是: `username.github.io`
    - 库名中的username必须与Github账号名称一致
2. Description 可选, 可不填写
3. Public or Private, 选择 Public
4. Initialize this repository with a README, 勾选


设置完成之后, 进入Repository Setting页面, 在Github Pages 栏目 
1. 设置Source, 由None改成Master branch
2. 然后启动Github Pages, 此时会看到以下字样
> Your site is published at [https://***username***.github.io](https://username.github.io)
> 这就代表Pages已经开通
 
### 安装本地Git部署器
1. 在macOS中打开终端工具, 进入hexo文件夹, 输入以下指令
```
cd hexo
npm install hexo-deployer-git -save #安装Git部署工具
```
2. 修改站点配置文件 `/hexo/_config.yml` 末尾
```
deply: 
    type: git
    repo: https://github.com/username/username.github.io  ## 注意username替换成自己的Github用户名
  branch: master
```
3. 进行本地发布, 通常可以先清空,再生成本地文件,最后发布
```
cd hexo
hexo clean  ## 清空本地已经产生的文件
hexo generate  ## 重新生成站点文件
hexo deploy  ## 将站点文件发布到Github
```
> 部署成功之后就能直接通过 `https://username.github.io` 访问你的站点内容

4. 如果在第3步遇到无法解析Github.com的错误提示
> hexo deploy could not resolve host: github.com
通常需要修改下本地的hosts文件, 直接进行Github.com域名解析
```
sudo vim /etc/hosts
192.30.255.112  github.com ## 在hosts文件中加入这个解析
:wq ##保存并退出
hexo deploy  ## 重新执行, 通常会成功解决无法解析的问题
```
![-w300](/images/15776857569366.jpg)

### 创建新博客

```
cd hexo
hexo new "new_blog_name"
hexo new draft "new_draft_name" 
hexo publish [layout] <filename>
```
> 自动产生新博客文件, /hexo/source/_posts/new_blog_name.md 
> 自动产生新草稿文件, /hexo/source/_drafts/new_draft_name.md
> 将草稿发布成正式

### 发布新博客 

```
hexo clean
hexo generate
hexo deploy

hexo g == hexo generate  ## 一些快捷键
hexo d == hexo deploy  ## 一些快捷键
hexo s == hexo server  ## 一些快捷键
hexo n == hexo new  ## 一些快捷键
```
### 安装Next Theme
1. [在此地址来下载](https://github.com/theme-next/hexo-theme-next/releases)
2. 安装在 /hexo/themes/ 路径上
3. [详细的设置参考地址](https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/README.md)

## MWeb 编辑环境
[下载MWeb](http://zh.mweb.im/index.html), 利用MWeb的外部模式, 可以将MWeb与Hexo结合起来, 对博客高效管理
### 设置MWeb
1. 通过 文件-打开外部模式
2. 可以在偏好设置中勾选"启动时默认打开外部模式"
3. 进入外部模式后, 点击左下角+, 引入文件夹, 把 /hexo/source/ 配置进去
4. 可以在 source文件夹下创建images文件夹, 同时将source的保存拖入的图片文件夹名称, 指定为images. 
> 这样设置的好处是, 在MWeb编辑时, 把图片往文章拖拽或者粘贴, MWeb都会自动将图片保存在`images`目录, 发布时也会自动发布, 省心省事
5. 设置完成后, 可以在MWeb里面看到hexo文章, 也可以新建博客

![-w300](/images/15776846673696.jpg)
![-w300](/images/15776847228832.jpg)

###  Hexo操作
在MWeb中完成写作后, 进入hexo进行发布操作
```
hexo clean ## 删除已经生成文件
hexo g  ## 生成新的文件
hexo s  ## 启动服务预览页面localhost:4000
hexo d  ## 发布到Github

hexo g -d ## 如果不预览直接用这个命令就可以发布
```
 
> [Github支持的Markdown语法](https://help.github.com/cn/github/writing-on-github/basic-writing-and-formatting-syntax)

## 结束语
自此就完成了个人博客的所有环境配置, 开始利用Markdown轻松记录内容了.
后续还会补充一些关于Next Theme模板的修改配置, 站点修改配置之类的内容, 等有时间再做, :)

## 补充: 多设备同步编辑
因为hexo的架构环境在本地, 在Github上发布的只是public文件夹, 所以如果想要在2台以上的电脑上同时来维护同一份博客, 就需要构建多设备同步的编辑环境.
### 构建思路
1. 假设在公司和家中分别有A,B两台电脑
2. A电脑已经完成了本篇所讲述的hexo环境搭建, 并且能把public文件夹网站文件发布到github的库master主分支
3. 此时只要把A电脑hexo文件夹下网站文件, 保存到github的另外一个分支比如branch_name即可
4. 然后在B电脑将将分支branch_name的内容全部获取下来, 再更新内容时, 将重新发布public文件夹并发布到master分支
5. 核心思路: 网站文件 存在master分支, 所有源文件存在branch_name分支

### 操作步骤
#### 首先, 假设A电脑已经完成了hexo搭建和github连接, 进入根目录hexo
```
cd hexo
git init #git初始化
git remote add origin https://github.com/Github_username/Github_username.github.io.git #添加仓库地址
git checkout -b branch_name #新建分支branch_name, 名称可更换, 切换到新分支
git add . #添加所有本地文件到git
git commit -m "这里填写你本次提交的备注，内容随意" #git提交
git push origin 分支名 #文件推送到hexo分支
```
##### 然后, 在B电脑部署git环境和node.js环境, 在某个文件夹下, 比如 cd ~
```
git clone -b branch_name https://github.com/Github_username/Github_username.github.io.git  # clone分支branch_name的内容, 也就是所有源文件
```
此时会在~目录上自动创建一个文件夹 Github_username.github.io
```
cd Github_username.github.io  
sudo npm install -g hexo-cli #安装hexo,注意这里不需要hexo初始化,否则之前的hexo配置参数会重置
sudo npm install #安装依赖库
sudo npm install hexo-deployer-git #安装git部署相关配置
```
此时环境搭建完成
##### 在B电脑完成写作之后
```
hexo g -d # 重新生成public文件夹, 并发布到 master分支
git add . # 开始讲所有源文件的更新发布
git commit -m "这里填写你本次提交的备注，内容随意"
git push origin branch_name # 更新发布到 branch_name 分支上  
```
#### 回到A电脑, 用下面的指令获取更新
```
git pull https://github.com/Github_username/Github_username.github.io branch_name # 注意要<远程> <分支名称> 之间有一个空格
```
在A电脑完成更新后, 再执行发布, 
```
hexo g -d # 重新生成public文件夹, 并发布到 master分支
git add . # 开始讲所有源文件的更新发布
git commit -m "这里填写你本次提交的备注，内容随意"
git push origin branch_name # 更新发布到 branch_name 分支上  
```
接下来就周而复始了.


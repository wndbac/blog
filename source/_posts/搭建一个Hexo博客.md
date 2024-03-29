---
abbrlink: 6e838c40
categories:
- - 教程
date: '2023-01-06 15:08:25'
description: Hexo是一款基于Nodejs的，快速、简洁且高效的博客框架。具有丰富的插件和主题，具有超快的速度。支持Makedown语法，可以方便快捷的编写博客文档。同时支持node命令，可以一键部署到GitHub Pages, Heroku等其他平台。
plugins:
- indent
readmore: false
tags:
- Hexo
title: 搭建一个Hexo博客
updated: Sun, 09 Apr 2023 11:20:01 GMT
---
## 简介

Hexo是一款基于Nodejs的，快速、简洁且高效的博客框架。具有丰富的插件和主题，具有超快的速度。支持Makedown语法，可以方便快捷的编写博客文档。同时支持node命令，可以一键部署到GitHub Pages, Heroku等其他平台。

## Hexo搭建

### 1、安装

- 安装git
- 安装node

**检测是否安装成功**

```bash
node -v
npm -v
```

- 安装hexo

```bash
npm install hexo-cli -g
```

### 2、初始化博客

```bash
hexo init
```

如操作过程中出现卡住问题可执行`Ctrl + C`命令终止程序

```bash
npm install
```

### 3、配置主题

转到theme文件夹下

```bash
git clone 主题的地址
```

**修改配置文件**

打开博客根目录的`_config.yml`文件，找到`theme`这一行，修改主题名字

```YAML
theme: 主题名字
```

### 4、上传

> 请先配置Git的SSH密钥等信息

**安装上传插件**

```bash
npm install hexo-deployer-git --save
```

**上传**

```bash
hexo clean
hexo g -d
```

到这里，我们其实已经完成了搭建，但是Hexo有一个很大的缺点，就是每次部署推送都要在本地

**解决方法：使用Hexo编辑器或Codespaces对博客进行管理**

## 管理

### 1、推送

> 如果想要使用编辑器来管理博客，那么请忽略上面的上传静态文件命令

请直接把文件夹中的所有文件直接推送到GitHub仓库（推送教程不过多阐述，自行百度）

如果上传了很久依然没有上传完成，那么请在博客根目录下新建一个`.gitignore`文件

**内容：**

```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
```

新建完成后，请再次进行推送

### 2、线上写文章/改配置

1. 使用 [GitHub Codespaces](https://github.com/codespaces/)；
2. 使用 [Qexo](https://www.oplog.cn/qexo/)；
3. 使用 [HexoPlusPlus](https://hexoplusplus.js.org)；
4. 更多... ...

### 3、部署

因GitHub无法直接处理Hexo根目录下的文件

所以为使Hexo博客运行，这里推荐使用 [Vercel](https://vercel.com) 进行部署，亦或使用 [GitHub Actions](https://xaoxuu.com/blog/20221126/#GitHub-Actions-自动化部署) 自动化部署，这里选择前者

{% gallery %}
![Vercel](https://cdn.wndbac.cn/gh/wndbac/Static/blog_img/2023/1/image_4e57c9f5fc1631f3e415d4c400ccfe13.png)
{% endgallery %}

> 请先将账号与GitHub连接

1. 点击右上角`Add New`，点开 `Project`选项

{% gallery %}
![image](https://cdn.wndbac.cn/gh/wndbac/Static/blog_img/2023/1/image_41687b54331a498b75870525bd9b4bc0.png)
{% endgallery %}

2. 在弹出的仓库中选择你部署Hexo原文件的仓库，点击`Import`按键

{% gallery %}
![image](https://cdn.wndbac.cn/gh/wndbac/Static/blog_img/2023/1/image_51b10f51997779da1f01373e757bbab7.png)
{% endgallery %}

3. 到这个页面，点击`Deploy`按键，等待部署完成

{% gallery %}
![image](https://cdn.wndbac.cn/gh/wndbac/Static/blog_img/2023/1/image_69d70e631d5aa9c3038167263b1dd21f.png)
{% endgallery %}

> 部署完成后，Vercel会分配给你一个子域名，但可惜的是`*.vercel.app`域名在大陆地区被电信运营商 DNS 污染，无法直接访问。
> 解决方法：绑定域名（一个域名一年也就几十块钱，建议自己从阿里云或者腾讯云购买一个域名）

---
layout: post
title: umami + Netlify + Supabase 零成本搭建网站访问统计系统
date: 2022-11-16 19:49:16
categories: Note
keywords: umami,netlify,supabase
---
> 2023年5月22日更新：umami已经由v1升级到了v2，架构发生了较大的改变，无法在Github中Sync fork来直接更新升级到v2。会因为在数据库中有v1版本的表格而无法升级，可以参考 https://umami.is/docs/migrate-v1-v2 来进行升级或者重新部署。

umami是一个非常小巧的网站访问统计系统，对于没几个访客的小博客来说足够用了。不需要购买VPS即可零成本搭建，一开始在vercel部署了一下，当然也是完全可以使用的，但现在感觉我这里的网络访问部署在Netlify的内容要比vercel更快一些。vercel一键部署就能成功，Netlify有一点点注意事项，作为小白的我试了好几次才部署成功，网络上也没有搜索到相关教程，所以在此记录一下。

## 一.使用Supabase创建数据库
Supabase网站地址： https://supabase.com/
可以使用GitHub账号登录，免费用户一个账号可以创建两个数据库（即两个project），登录后点击New project按钮创建数据库。

![](https://ucarecdn.com/f4ebc8d2-2bdd-4b24-8573-fd6f73fb01d9/2001.webp)

输入数据库名称和密码，如果是点击生成密码按钮得到的密码，要复制一下记录下来等下要用。地区选择离自己较近的地区，最后点击Create new project按钮。等待约一两分钟后数据库创建完成。

![](https://ucarecdn.com/caca6c41-0cfc-49e0-9ee9-26737fcacd9a/2002.webp)

点击左下角齿轮（Project Settings）按钮，点击DataBase，复制Connection string中的URI字符串，将其中的[YOUR-PASSWORD]替换为创建时设置的密码，得到一串类似于如下的连接字符串。
postgresql://postgres:password @ db.rcpdseetwdeuq.supabase.co:5432/postgres

![](https://ucarecdn.com/15a5acd1-3579-4133-86fd-529ee98cabda/2003.webp)

至此得到了umami所需要的数据库空间。

## 二.在Netlify部署
参考umami官网的步骤，这里的步骤非常简略，有些细节并没有写全。我并不能通过这里的Deploy按钮来部署成功，点击后无法自动fork umami到自己的GitHub账号，若自己已经手动fork再点击又会提示项目已存在。所以就按步骤手动操作吧。

![](https://ucarecdn.com/82fc6b84-8545-4a5f-b2ca-0f257261b076/2004.webp)

### 1.克隆umami项目
umami项目地址： https://github.com/umami-software/umami
点击Fork，将umami克隆到自己的GitHub账号。

### 2.在Netlify新增站点
登录Netlify，在Sites点击Add new site选择Import an existing project，选择从GitHub导入并授权允许访问，选择自己GitHub仓库中umami。
![](https://ucarecdn.com/76509569-6f57-46ed-b014-c56d711e34b9/2005.webp)|![](https://ucarecdn.com/2de1c6cb-becc-404e-844a-93531ac38e97/2006.webp)|![](https://ucarecdn.com/ed12504b-b54c-44c2-8476-6dd972e4e9f2/2007.webp)
---|---|---

### 3.站点部署设置
在Build command输入
```
yarn install && yarn build
```
（**重要！** 参考了https://umami.is/docs/install ，一开始因为不知道输入这个install指令部署失败了几次）。
![](https://ucarecdn.com/1af6b857-e1e4-46b9-8d0d-5167f75033a8/2008.webp)

点击Show advanced,点击New variable按钮新增三个参数。
- DATABASE_URL	值为第一步中得到的数据库连接字符串
- HASH_SALT		随意输入自定义字符串
- TRACKER_SCRIPT_NAME		如果浏览器安装有屏蔽广告插件，可能会阻止umami.js，这个参数是重命名这个js文件，避免被屏蔽而无法准确统计
> 2023年5月22日更新：v2版本中默认脚本名称已变更为script.js。TRACKER_SCRIPT_NAME不再附加“.js”后缀，可能会造成找不到这个js文件而出现404错误。可以将这个参数设置为customName.js,自己添加".js"后缀。

点击Deploy按钮，等待几分钟后，显示Published即部署成功。
![](https://ucarecdn.com/c1caeddc-c682-4e85-8ede-62d03bf2d587/2009.webp)

此时在Supabase创建的数据库中也已自动生成了数据表。
![](https://ucarecdn.com/f5d219ca-531d-472e-98fa-943f41c1068a/2010.webp)

## 三.umami网站设置
可在Netlify中设置自定义域名便于访问。
默认登录账号密码为admin/umami。
![](https://ucarecdn.com/e000eb20-a858-471a-ba6e-e3d2b71f9334/2011.webp)

## 四.umami更新
在自己克隆的umami仓库中点击Sync fork即可，Netlify中部署的网站将同步更新。
![](https://ucarecdn.com/ec4a2256-88a1-4217-95fe-d4a951d30563/2013.webp)
![logo_white.png](https://raw.githubusercontent.com/HFO4/Cloudreve/master/static/img/logo_white.png)

Cloudreve - Make the cloud easy for everyone
=========================
[![Packagist](https://img.shields.io/packagist/v/HFO4/Cloudreve.svg)](https://packagist.org/packages/hfo4/cloudreve)
[![Latest Unstable Version](https://poser.pugx.org/hfo4/cloudreve/v/unstable)](https://packagist.org/packages/hfo4/cloudreve)
[![License](https://poser.pugx.org/hfo4/cloudreve/license)](https://packagist.org/packages/hfo4/cloudreve)

[主页](https://cloudreve.org) | [论坛](https://forum.cloudreve.org) | [演示站](https://drive.aoaoao.me) | [QQ群](https://jq.qq.com/?_wv=1027&k=5TX6sJY)

使用ThinkPHP + React + Redux + Material-UI构建的网盘系统，能够助您以较低成本快速搭建起公私兼备的网盘。

![HomePage](https://i.loli.net/2019/03/16/5c8caf825282a.jpg)

目前已经实现的特性：

* 快速对接多家云存储，支持七牛、又拍云、阿里云OSS、AWS S3、Onedrive、自建远程服务器，当然，还有本地存储
* 可限制单文件最大大小、MIMEType、文件后缀、用户可用容量
* 自定义主题配色
* 基于Aria2的离线下载
* 图片、音频、视频、文本、Markdown、Ofiice文档 在线预览
* 移动端全站响应式布局
* 文件、目录分享系统，可创建私有分享或公开分享链接
* 用户个人主页，可查看用户所有分享
* 多用户系统、用户组支持
* 初步完善的后台，方便管理
* 拖拽上传、分片上传、断点续传、下载限速（*实验性功能）
* 多上传策略，可为不同用户组分配不同策略
* 用户组基础权限设置、二步验证
* WebDAV协议支持


安装需求
------------
* LNMP/AMP With PHP5.6+
* curl、fileinfo、gd扩展
* Composer

简要安装说明
------------

#### 1.使用Composer安装主程序
```
#安装开发版
$ composer create-project hfo4/cloudreve:dev-master
```

```
#等待安装依赖库后，会自动执行安装脚本，按照提示输入数据库账户信息
   ___ _                 _                    
  / __\ | ___  _   _  __| |_ __ _____   _____ 
 / /  | |/ _ \| | | |/ _` | '__/ _ \ \ / / _ \
/ /___| | (_) | |_| | (_| | | |  __/\ V /  __/
\____/|_|\___/ \__,_|\__,_|_|  \___| \_/ \___| 
        
                Ver XX
================================================
#按提示输入信息
......
```

```
#出现如下提示表示安装完成
Congratulations! Cloudreve has been installed successfully.

Here's some informatioin about yor Cloudreve:
Homepage: https://pan.cloudreve.org/
Admin Panel: https://pan.cloudreve.org/Admin
Default username: admin@cloudreve.org
Default password: admin
```

#### 2.目录权限
`runtime`目录需要写入权限，如果你使用本地存储，`public` 目录也需要有写入权限

#### 3.URL重写
对于Apache服务器，项目目录下的`.htaccess`已经配置好重写规则，如有需求酌情修改.
对于Nginx服务器，以下是一个可供参考的配置：
```
location / {
   if (!-e $request_filename) {
   rewrite  ^(.*)$  /index.php?s=/$1  last;
   break;
    }
 }
```

#### 4.完成
后台地址：`http://您的域名/Admin` 初始用户名：`admin@cloudreve.org` 初始密码：`admin`
#### 后续操作
以下操作不是必须的，但仍推荐你完成这些操作：
* 修改初始账户密码
* 到 设置-基础设置 中更改站点URL，如果不更改，程序无法正常接受回调请求
* 添加Crontab定时任务 ：你的域名/Cron
* 如果你打算使用本地上传策略并且不准备开启外链功能，请将·public/uploads·目录设置为禁止外部访问
* 如需启用二步验证功能，请依次执行`composer require phpgangsta/googleauthenticator:dev-master` `composer require endroid/qr-code`安装二步验证支持库

文档
------------
* [完整安装说明](https://cloudreve.github.io/docs/#/install)
* [安装及初次使用FAQ](https://cloudreve.github.io/docs/#/faq)
* [Wiki](https://github.com/cloudreve/Cloudreve/wiki)

许可证
------------
GPLV3


kangle主机 cloudreve 搭建
------------
环境（PHP5.5-7.3）其他版本无法使用
建议 PHP7.0
#### 1.上传压缩包并解压
#### 2.重写项目根目录下的`.htaccess`伪静态规则（kangle主机/ep面板 专用 ）
```

<IfModule mod_rewrite.c>
RewriteEngine on
RewriteBase /
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^(.*)$ index.php/$1?%{QUERY_STRING} [QSA,PT,L]
</IfModule>


```
#### 3.确保http或https协议，如果强制http转https，则无法进入页面，会出现空白页
#### 4.进入`http://[你的域名]/CloudreveInstaller`配置数据库
#### 5.进入后台配置，即可使用
#### 6.建议安装完成后手动删除`CloudreveInstaller`文件夹以保证安全性
## Cloudreve V2.0
此版本已经被原开发者抛弃，不再进行维护，这个仓库仅仅是用于存档和学习使用，任何相关问题不负责

使用ThinkPHP + React + Redux + Material-UI构建的网盘系统，能够助您以较低成本快速搭建起公私兼备的网盘。

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

## kangle主机 | EP面板 Cloudreve v2.0 安装

### 环境
------------
* PHP 5.6 - 7.3（其他版本无法使用，本人一个个版本测试过去的）
* 建议 PHP 7.0

* LNMP/AMP
* curl、fileinfo、gd扩展
* Composer
------------

#### 1.上传压缩包并解压
#### 2.重写项目根目录下的`.htaccess`伪静态规则（kangle主机/ep面板 专用）
```
<IfModule mod_rewrite.c>
RewriteEngine on
RewriteBase /
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^(.*)$ index.php/$1?%{QUERY_STRING} [QSA,PT,L]
</IfModule>
```
#### 3.确保 http 或 https 协议，如果强制 http 转 https ，则无法进入页面，会出现空白页
#### 4.进入` http://[你的域名]/CloudreveInstaller `配置数据库
#### 5.进入后台配置，后台地址：` http://您的域名/Admin ` 初始用户名：` admin@cloudreve.org ` 初始密码：` admin `
#### 6.建议安装完成后手动删除` CloudreveInstaller `文件夹以保证安全性
#### 后续操作
以下操作不是必须的，但仍推荐你完成这些操作：
* 修改初始账户密码
* 到 设置-基础设置 中更改站点URL，如果不更改，程序无法正常接受回调请求
* 添加Crontab定时任务 ：你的域名/Cron
* 如果你打算使用本地上传策略并且不准备开启外链功能，请将·public/uploads·目录设置为禁止外部访问
* 如需启用二步验证功能，请依次执行`composer require phpgangsta/googleauthenticator:dev-master` `composer require endroid/qr-code`安装二步验证支持库

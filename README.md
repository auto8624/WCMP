# WCMP
WCMP是基于Windows x64平台下的Caddy2 + PHP + MySQL便携软件包。用来搭建简易的本地php开发测试环境。

![image](https://github.com/jiix/WCMP/raw/main/screenshot.jpg)

只需要[下载](https://github.com/jiix/WCMP/releases)并运行`Wcmp.exe`，你将会有一个简单易于移植的开发环境。只需要备份WCMP目录所有文件，你可以把它带到任何地方。

## 软件包版本
* Caddy v2.3.0
* PHP v8.0.1
* MariaDB v10.5.8
* SQLite v3.33.0
* Adminer v4.7.8

## 说明:

* 所有程序均来自于官方最新x64版本，你可以下载其它版本进行替换。
* 所有配置大多是默认配置。
* php fastcgi运行于9000端口。
* 使用相对路径以便于移植。
* Mysql数据库默认用户名为root，密码为空，请一定要及时更改。
* 默认网站目录是site01。你可以访问http://127.0.0.1 浏览。

### MySQL设置
登录MySQL，先打开MySQL bin运行目录(例如`cd E:\WCMP\mysql\bin`)，再运行`mysql -u root mysql`等命令。
#### 修改MySQL root密码
运行WCMP后推荐首先设置MySQL root密码。
```
mysqladmin -uroot password
```
#### 创建数据库
```
mysqladmin -u root -p create your_db_name
```

### 使用Adminer
默认访问http://127.0.0.1/adminer.php 在线管理MySQL数据库。注：需要先设置MySQL密码后才可登录。

### 使用caddy
打开Caddyfile，进行相关设置后重启caddy。
#### 创建新站点
```
www.yourdomain.com {

    root *  ..\www\yourdomain.com
    
    php_fastcgi localhost:9000
    encode zstd gzip 
    file_server
    header -Server
}
```

#### Caddyfile WebDAV演示😄
请编辑`WCMP\caddy\Caddyfile`进行设置。演示账号为`jiih`，密码为`jiih.com`，文件目录位于`www\webdav`。
```
www.yourdomain.com {
root *  ..\www\webdav

route {
 	rewrite /webdav /webdav/
	webdav /webdav/* {
		prefix /webdav
	}
	file_server
}
  basicauth /webdav/* {
	jiih JDJhJDEwJHY1SUpDYTZram9vMWhlTU1NNGZWVk9sTXlzV3hYYmdMWnA5Ry5mbkZvOVlEUzFBU2RERzUy
}
```
Caddy的配置文件不接受纯文本密码，你需要使用[caddy hash-password](https://caddyserver.com/docs/command-line#caddy-hash-password)对密码进行加密处理。
## (⊙﹏⊙)
Fork from [KKnBB](https://kknbb.com/stories/wcmp-windowscaddy2phpmysql-all-in-1-portable-package/)

# WordPress-For-Heroku

请勿滥用，Heroku每个月仅550小时（550/24=22.916667天）

wordpress简体中文网站：https://cn.wordpress.org

PostgreSQL for WordPress 下载地址：https://wordpress.org/plugins/postgresql-for-wordpress/

1msky.cn的博客教程：https://1msky.cn/herokuWP.html

# Demo

https://xl-wp.herokuapp.com

# 原作

https://github.com/chenchk/wordpress-for-heroku

版本很低，没有主题和插件。

本仓库内置一些插件和主题。

# Deploy

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://dashboard.heroku.com/new?template=https://github.com/MINGERTAI/wordpress)

# 配置

## WordPress 版本

+ WordPress 5.9.3

## 插件

+ Jetpack
+ WPJAM Basic
+ Yoast SEO
+ WP Mail SMTP by WPForms

## 主题

+ 2019
+ 2022
+ Argon Theme
+ bravada
+ kratos

## 新建分支

下载源码https://cn.wordpress.org/latest-zh_CN.zip 解压下载的源码包 wordpress-5.9.3-zh_CN.zip, 重命名解压目录为wordpress-for-heroku

打开gitbash进入cd该目录,初始化并提交仓库

heroku只有pgsql免费，wordpress是默认使用mysql，所以要装一个插件PG4WP！

下载数据库插件：https://wordpress.org/plugins/postgresql-for-wordpress/

# 修改源码

+ 解压PostgreSQL for WordPress (PG4WP)到wp-content文件夹下

+ wp-content/pg4wp文件夹里面的db.php文件复制到wp-content文件夹下

+ 复制配置文件wp-config-sample.php文件为wp-config.php

+ 修改wp-config.php文件，添加数据库账号、密码等信息(使用heroku的pg)

+ 追加SSL_LOGIN

# wp-config.php修改内容

# 删除如下

/** WordPress数据库的名称 */

define('DB_NAME', 'database_name_here');

/** MySQL数据库用户名 */

define('DB_USER', 'username_here');

/** MySQL数据库密码 */

define('DB_PASSWORD', 'password_here');

/** MySQL主机 */

define('DB_HOST', 'localhost');

# 追加

// ** MySQL settings - You can get this info from your web host ** //  注：heroku 环境变量

$db = parse_url($_ENV["DATABASE_URL"]);        

/** The name of the database for WordPress */

define('DB_NAME', trim($db["path"],'/'));

/** MySQL database username */

define('DB_USER', $db["user"]);

/** MySQL database password */

define('DB_PASSWORD', $db["pass"]);

/** MySQL hostname */

define('DB_HOST', $db["host"]);

#  追加 SSL_LOGIN

$_SERVER['HTTPS'] = 'on';

define('FORCE_SSL_LOGIN', true);

define('FORCE_SSL_ADMIN', true);

# 🚀 在 RAKsmart 服务器上快速部署 WordPress 建站指南

WordPress 作为全球最受欢迎的开源 CMS（内容管理系统），可以帮助用户快速搭建个人博客、企业官网、商城等各类网站。如果你正在使用 RAKsmart 服务器并希望搭建 WordPress 网站，本教程将提供完整的安装步骤，即使是新手也能轻松完成！

## 📌 准备工作

在开始安装 WordPress 之前，你需要准备以下内容：

- **RAKsmart 服务器**（建议选择 Linux 服务器，如 CentOS 或 Ubuntu）
- **域名**（可选，但建议绑定域名以便访问）
- **服务器环境**（LAMP 或 LEMP）
- **SSH 终端工具**（如 Xshell、Putty）或 RAKsmart 提供的 Web 控制台
- **FTP 工具**（如 FileZilla）

👉 [【点击查看】2025年最新 RAKsmart 优惠码及特价云服务器方案汇总](https://bit.ly/raksmart)

## 📌 安装服务器环境

WordPress 需要 PHP + MySQL + Web 服务器（Apache 或 Nginx）运行，因此我们需要安装 LAMP 或 LEMP 环境。

### 🔹 方法 1：安装 LAMP（Apache + MySQL + PHP）

适用于喜欢使用 Apache 服务器的用户。

**在 CentOS 服务器上安装 LAMP：**

bash
yum update -y
yum install httpd mariadb-server mariadb php php-mysqlnd php-fpm php-xml php-mbstring unzip -y
systemctl start httpd
systemctl start mariadb
systemctl enable httpd
systemctl enable mariadb

**在 Ubuntu 服务器上安装 LAMP：**

bash
apt update -y
apt install apache2 mariadb-server php php-mysql php-fpm php-xml php-mbstring unzip -y
systemctl start apache2
systemctl start mariadb
systemctl enable apache2
systemctl enable mariadb

### 🔹 方法 2：安装 LEMP（Nginx + MySQL + PHP）

适用于喜欢使用 Nginx 服务器的用户。

**安装 Nginx、MySQL、PHP**

bash
apt update -y
apt install nginx mariadb-server php-fpm php-mysql php-xml php-mbstring unzip -y
systemctl start nginx
systemctl start mariadb
systemctl enable nginx
systemctl enable mariadb

## 📌 下载并上传 WordPress

安装完服务器环境后，下载并上传 WordPress 文件：

bash
cd /var/www/html
wget https://wordpress.org/latest.zip
unzip latest.zip
mv wordpress/* .
rm -rf wordpress latest.zip
chown -R www-data:www-data /var/www/html
chmod -R 755 /var/www/html

## 📌 创建 WordPress 数据库

使用 MySQL 创建 WordPress 所需的数据库和用户：

bash
mysql -u root -p

然后输入以下 SQL 命令：

sql
CREATE DATABASE wordpress;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'yourpassword';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;

请务必替换 `yourpassword` 为一个强密码。

## 📌 配置 WordPress

修改 WordPress 配置文件，使其连接数据库：

bash
cp /var/www/html/wp-config-sample.php /var/www/html/wp-config.php
nano /var/www/html/wp-config.php

找到以下字段，并替换为你的数据库信息：

php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wpuser');
define('DB_PASSWORD', 'yourpassword');
define('DB_HOST', 'localhost');

保存并退出（按 `Ctrl + X`，然后按 `Y` 确认保存）。

## 📌 安装并访问 WordPress

现在，打开浏览器访问 `http://你的服务器IP/`，你将看到 WordPress 安装向导。

## 📌 优化 WordPress 站点（可选）

为了提高 WordPress 站点的安全性和性能，可以进行以下优化：

### ✅ 配置 HTTPS

建议为网站安装 SSL 证书，可以使用 Let's Encrypt 免费 SSL：

bash
apt install certbot python3-certbot-apache  # LAMP 用户
apt install certbot python3-certbot-nginx   # LEMP 用户
certbot --apache                             # Apache 配置
certbot --nginx                              # Nginx 配置

### ✅ 启用缓存插件

在 WordPress 插件市场安装 **WP Super Cache 或 W3 Total Cache**，提高网站访问速度。

### ✅ 安全设置

- 修改默认 `admin` 账户，使用复杂密码
- 启用 **Wordfence Security** 插件，增强 WordPress 安全性
- 定期更新 WordPress 版本、插件和主题

## 📌 总结

恭喜！你已经在 RAKsmart 服务器上成功安装了 WordPress 🎉。现在，你可以开始自定义主题、安装插件、发布内容，让自己的网站焕发光彩！

如果在安装过程中遇到问题，可以随时在 RAKsmart 官方文档或论坛寻求帮助。希望这篇指南能帮到你，祝你的 WordPress 之旅愉快！🚀
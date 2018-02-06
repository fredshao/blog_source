---
title: Ubuntu搭建SVN服务器
date: 2017-12-16 19:55:46
tags: 服务器配置
---



好了，现在就开始在Ubuntu上配置SVN服务器，这个教程是SVN+Apache2，使用http访问的svn服务器

1. **安装必要的东西**

   ```shell
   sudo apt-get update
   sudo apt-get install apache2
   sudo apt-get install subversion libapache2-mod-svn libapache2-svn libsvn-dev
   ```

2. **修改配置文件，一个Location标识一个仓库（我猜的，没试过）**

   ```shell
   # /etc/apache2/mods-enabled/dav_svn.conf 改成下面的样子

   <Location /svn>
      DAV svn
      SVNParentPath /var/lib/svn
      AuthType Basic
      AuthName "Subversion Repository"
      AuthUserFile /etc/apache2/dav_svn.passwd
      Require valid-user
   </Location>
   ```

3. 创建仓库

   ```shell
   sudo mkdir -p /var/lib/svn/
   sudo svnadmin create /var/lib/svn/myrepo
   sudo chown -R www-data:www-data /var/lib/svn
   sudo chmod -R 775 /var/lib/svn
   ```

4. 为仓库添加用户

   ```shell
   sudo htpasswd -cm /etc/apache2/dav_svn.passwd admin	# 创建一个用户
   sudo htpasswd -m /etc/apache2/dav_svn.passwd user1	# 再创建一个用户
   sudo htpasswd -m /etc/apache2/dav_svn.passwd user2	# 再创建一个用户
   ```

5. 重启服务

   ```shell
   sudo a2enmod dav
   sudo a2enmod dav_svn
   sudo service apache2 restart
   ```

   **好了，上面的操作执行完，svn就已经配置完成了**

6. 在浏览器中访问一下试试(记得把example.com换成自己IP或者域名，用户Checkout也是用下面的地址)

   http://example.com/svn/myrepo
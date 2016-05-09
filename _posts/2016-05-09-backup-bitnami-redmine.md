---
layout: post
title: "备份Bitnami Redmine"
date: 2016-04-13
comments: true
categories:
---
  
查看Redmine的MySQL数据库密码：

cat /opt/redmine-3.2.1-0/apps/redmine/htdocs/config/database.yml

如果密码不正确，又忘记了初始设置的密码，执行以下命令进行修改：

/opt/redmine-3.2.1-0/mysql/bin/mysqladmin -P3336 -p -u root password 

密码一般为安装Redmine时管理员设置的初始密码

##1.备份数据库

/opt/redmine-3.2.1-0/mysql/bin/mysqldump -uroot -p -P3336 --set-gtid-purged=OFF mysql>/data/mysql.sql

/opt/redmine-3.2.1-0/mysql/bin/mysqldump -uroot -p -P3308 --set-gtid-purged=OFF bitnami_redmine>/data/bitnami_redmine.sql

##2.备份邮件配置

cp /opt/redmine-3.2.1-0/apps/redmine/htdocs/config/configuration.yml /data

##3.备份项目文档

cp -r /opt/redmine-3.2.1-0/apps/redmine/htdocs/files/ /data

##4. 关停Redmine

/opt/redmine-3.2.1-0/ctlscript.sh stop

##5. 重装Bitnami Redmine

/data/soft/bitnami-redmine-3.2.1-0-linux-x64-installer.run

##6. 还原数据库

/opt/redmine-3.2.1-0/mysql/bin/mysql -uroot -p -P3336 mysql</data/mysql.sql

/opt/redmine-3.2.1-0/mysql/bin/mysql -uroot -p -P3336 bitnami_redmine</data/bitnami_redmine.sql

##7. 还原文档

cp -r /data/files  /opt/redmine-3.2.1-0/apps/redmine/htdocs/ (不替换delete.me)

##8. 还原邮件配置

cp -r /data/configuration.yml  /opt/redmine-3.2.1-0/apps/redmine/htdocs/config

# 重启Redmine
/opt/redmine-3.2.1-0/ctlscript.sh restart

# 注意：
备份与还原前后的mysql数据库root账号密码需要保持一致！
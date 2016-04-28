---
layout: post
title: "设置Bitnami Redmine邮件通知"
date: 2016-04-13
comments: true
categories:
---
  
bitnami-redmine的配置文件与单纯的redmine配置文件可能并不相同，在这里我们需要打开一下配置文件：

/opt/redmine-3.2.1-0/apps/redmine/htdocs/config/configuration.yml

在configuration.yml最后添加以下配置内容，需要注意的是不需要加引号，之前的参考文献当中都说需要加引号，是错误等

```
production:
  email_delivery:
    delivery_method: :smtp
    smtp_settings:
      address: "smtp.qq.com" 
      port: "465" 
      ssl: true
      enable_starttls_auto: true
      domain: "smtp.qq.com" 
      authentication: :login
      user_name: "simbest@foxmail.com" 
      password: "xxxx"
# specific configuration options for development environment
# that overrides the default ones
development:
  email_delivery:
    delivery_method: :smtp
    smtp_settings:
      address: "smtp.qq.com" 
      port: "465" 
      ssl: true
      enable_starttls_auto: true
      domain: "smtp.qq.com" 
      authentication: :login
      user_name: "simbest@foxmail.com" 
      password: "xxxx"
```

## 注意：

一个:需要后跟一个空格，两个: :无需后跟空格

在配置完毕以后重启redmine

```
$ cd /opt/bitnami
$ sudo ./ctlscript.sh restart 
```

这个ctlscript.sh脚本的用法有一些这些参数
```
usage: ./ctlscript.sh help
       ./ctlscript.sh (start|stop|restart|status)
       ./ctlscript.sh (start|stop|restart|status) mysql
       ./ctlscript.sh (start|stop|restart|status) php-fpm
       ./ctlscript.sh (start|stop|restart|status) apache
       ./ctlscript.sh (start|stop|restart|status) subversion
```

测试
配置完毕以后测试是否配置成功，然后访问redmine，以管理员的身份登录系统，点击"管理"---->"配置"---->"邮件通知"，然后点击右下角的"发送测试邮件"，就可以测试你的邮件服务配置是否成功了。

## 注意

邮件发件人地址这一栏需要修改成我们配置的邮件服务器dev@simbest.com.cn，而测试邮件会发送到我们当前登陆账户的邮箱。
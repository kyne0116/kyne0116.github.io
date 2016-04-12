---
layout: post
title: "使用JavaMelody监控Java Web应用"
date: 2016-04-12
comments: true
categories:
---
  
  在Maven的pom文件增加javamelody依赖
  
```
<dependency>
    <groupId>net.bull.javamelody</groupId>
    <artifactId>javamelody-core</artifactId>
    <version>1.59.0</version>
</dependency>
```

在应用的web.xml中增加

```
<context-param>
	<param-name>contextConfigLocation</param-name>
	<param-value>
		classpath:net/bull/javamelody/monitoring-spring-datasource.xml,
		classpath:其他applicationContext.xml		
	</param-value>
</context-param>

<listener>
    <listener-class>net.bull.javamelody.SessionListener</listener-class>
</listener>

<filter>
    <filter-name>javamelody</filter-name>
    <filter-class>net.bull.javamelody.MonitoringFilter</filter-class>
	<init-param> 
		<param-name>log</param-name> 
		<param-value>true</param-value> 
	</init-param>
</filter>

<filter-mapping>
    <filter-name>javamelody</filter-name>
    <url-pattern>/*</url-pattern>
    <dispatcher>REQUEST</dispatcher>
</filter-mapping>
```    

配置完成后，启动应用，并打开监控首页http://host:port/monitoring，例如：

http://localhost:8080/myapp/monitoring

具体参考官网[用户指南](https://github.com/javamelody/javamelody/wiki/UserGuide#introduction)

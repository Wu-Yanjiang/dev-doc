---
title: "Tomcat常用配置"
date: 2022-03-20T17:44:15+08:00
thumbnailImagePosition: right
thumbnailImage: https://tomcat.apache.org/res/images/tomcat.png
draft: false
slug: tomcat-cfg
categories:
- web开发
tags:
- tomcat
- ssl
keywords:
- tomcat
- ssl
- 阿里云
comments:       true
showMeta:       false
showActions:    true
---

本篇文章记录tomcat在Ubuntu下的常见配置，包含安装、部署web项目、部署SSL证书等。

<!--more-->

# Tomcat官网

[Tomcat官网](https://tomcat.apache.org/)

# 安装

```shell
sudo apt-get install tomcat9
```

# 启停服务

```shell
# 启动tomcat服务
service tomcat9 start

# 停止
service tomcat9 stop

# 重启
service tomcat9 restart
```

# 配置文件

```bash
>ls /etc/tomcat9
Catalina  catalina.properties   context.xml  jaspic-providers.xml  
logging.properties  policy.d  server.xml  tomcat-users.xml  web.xml
```
- Catalina目录：Web项目部署目录  
- server.xml：tomcat服务器配置文件

# 日志

```bash
>ls /var/log/tomcat9
catalina.2022-03-14.log.gz  catalina.2022-03-18.log.gz   localhost.2022-03-19.log.gz             
catalina.2022-03-15.log.gz  catalina.2022-03-19.log.gz   localhost.2022-03-20.log                
catalina.2022-03-16.log.gz  catalina.2022-03-20.log      localhost_access_log.2022-03-14.txt.gz  
catalina.2022-03-17.log.gz  localhost.2022-03-14.log.gz  localhost_access_log.2022-03-15.txt.gz 
localhost_access_log.2022-03-16.txt.gz  localhost_access_log.2022-03-20.txt
localhost_access_log.2022-03-17.txt.gz
localhost_access_log.2022-03-18.txt.gz
localhost_access_log.2022-03-19.txt.gz 

# 查看当天日志
>tail -f /var/log/tomcat9/catalina.2022-03-20.log
```

# SSL证书配置
## 白嫖云服务商SSL证书
此处以aliyun为例，其他云类似:
1. 注册阿里云账号
2. 数字证书管理服务中创建免费证书
3. 申请证书
4. tomcat安装证书

详见[Aliyun数字证书管理服务](https://help.aliyun.com/document_detail/188316.htm?spm=5176.b657008.help.dexternal.c124799dFTBL6t)

# http强制跳转https配置

```bash
>sudo vim /etc/tomcat9/server.xml

<Connector port="80" protocal="HTTP/1.1"
        connectionTimeout="20000" 
        redirectPort="443" maxHttpHeaderSize="8192"
/>


<Connector port="443" 
        protocol="org.apache.coyote.http11.Http11NioProtocol"
        SSLEnabled="true"
        scheme="https"
        secure="true"
        keystoreFile="证书路径"
        keystoreType="PKCS12"
        keystorePass="证书密码"
        clientAuth="false"
        SSLProtocol="TLSv1.1+TLSv1.2+TLSv1.3"
        ciphers="TLS_RSA_WITH_AES_128_CBC_SHA,TLS_RSA_WITH_AES_256_CBC_SHA,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA,
        TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA25TLS_RSA_WITH_AES_128_CBC_SHA256,TLS_RSA_WITH_AES_256_CBC_SHA256"
/>

>sudo vim /etc/tomcat9/web.xml

# web-app节点中加入以下节点
<security-constraint>
    <web-resource-collection >
        <web-resource-name >SSL</web-resource-name>
        <url-pattern>/*</url-pattern>
    </web-resource-collection>
    <user-data-constraint>
        <transport-guarantee>CONFIDENTIAL</transport-guarantee>
    </user-data-constraint>
</security-constraint>

# 重启一下
>service tomcat9 restart
```
# 参考资料

- [Tomcat官网](https://tomcat.apache.org/)
- [Aliyun数字证书管理服务](https://help.aliyun.com/document_detail/188316.htm?spm=5176.b657008.help.dexternal.c124799dFTBL6t)


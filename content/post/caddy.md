---
title: "Caddy快速入门"
date: 2023-03-18T18:59:09+08:00
categories:
- server
- 服务器
- web
tags:
- linux
- caddy
keywords:
- caddy
#thumbnailImage: //example.com/image.jpg
---

<!--more-->

# Caddy
Caddy is a powerful, extensible platform to serve your sites, services, and apps, written in Go. If you're new to Caddy, the way you serve the Web is about to change.

可以用来做什么？  
答：文件服务器、web服务器、反向代理服务器、网关、代理服务器...  
简而言之，多快好省，人懒不多BB直接上Caddy，性能好，各种花活都能整，还能自动免费帮你续签Let's Encrypt的Https证书。

```bash
# Debian, Ubuntu, Raspbian
# 安装
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy
```

# Caddyfile
Caddyfile就是一个caddy服务器启动配置文件，用于配置caddy对网站的配置信息。该文件是一个无后缀名的纯文本文件。

```bash
# Caddyfile
yjlearn.cn {
        # 该指令用于重定向，访问yjlearn.cn的域名都将重定向至一下域名
        redir https://www.yjlearn.cn
}

www.yjlearn.cn {
        # 启用压缩
        encode zstd gzip
        # 指定任何路径下的根目录为以下目录
        root * ~/blog/public
        # 开启文件服务器， browse参数启用目录界面 
        # file_server browse
        file_server
}

# 启动，不用sudo会因为权限不够导致无法在80和443端口启动web服务
sudo caddy run --config Caddyfile &

```


# 参考资料
- [caddy官网帮助文档](https://caddyserver.com/docs/)
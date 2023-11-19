# Nginx Proxy Manager

# 1. 配置静态文件

在这个配置中，static-server 服务是一个 Nginx 容器，它通过挂载 ./static-html 目录来提供静态文件服务。然后，在 Nginx Proxy Manager 中设置一个代理规则，将 hi.haha.ai 的流量转发到 static-server。这样，当访问 hi.haha.ai 时，Nginx Proxy Manager 会代理请求到 static-server 服务，后者提供静态内容。

确保在 Nginx Proxy Manager 的界面中正确配置反向代理，将 hi.haha.ai 的流量代理到 static-server 实例的 IP 地址和端口（在这种情况下，通常是 static-server 和 80 端口）。

# 2. 在单体服务中，配置域名路由

接下来，在 Nginx Proxy Manager 中配置域名 hi.haha.ai：

1. 登录到 Nginx Proxy Manager 的界面。
2. 创建一个新的代理主机。
3. 在 “Domain Names” 字段中，输入 hi.haha.ai。
4. 将 “Forward Hostname / IP” 设置为 static-server（即上述 Docker Compose 中定义的 Nginx 静态文件服务器的服务名称）。
5. 将 “Forward Port” 设置为 80（Nginx 默认的 HTTP 端口）。
6. 完成其他必要的配置（如 SSL）并保存。

通过这种方法，当访问 hi.haha.ai 时，NPM 会将请求代理到 Docker Compose 网络中的 Nginx 静态服务器上，而该服务器则提供 ./static-html/ 目录中的静态文件。


高级配置如下，（类似于 vite.config.ts 中的配置）

```
location /chat {
    proxy_pass http://172.26.123.198:19075;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}


location /assets {
    proxy_pass http://172.26.123.198:19075;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}


location /qr {
    proxy_pass http://172.26.123.198:19075;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}


location /auth {
    proxy_pass http://172.26.123.198:19075;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}

// 注意：默认的放到最后面。单页应用。
location / {
    proxy_pass http://static-server:80;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;

    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;

    # 重要：为前端路由添加特殊处理
    try_files $uri $uri/ /index.html;
}
```



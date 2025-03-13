# README


## Drone CI


```bash
DRONE_GITHUB_CLIENT_ID={GITHUB_CLIENT_ID}
DRONE_GITHUB_CLIENT_SECRET={GITHUB_CLIENT_SECRET}

# openssl rand -hex 16
DRONE_RPC_SECRET=58d7d98a8e29cdb8abcde7df691f1234
```


## Run

1. 在GitHub（或其他Git服务）创建OAuth应用程序并获取客户端ID和密钥
2. 生成安全的RPC密钥（使用openssl rand -hex 16命令）
3. 将这些凭据填入.env文件


使用方式：

1. DRONE_SERVER_HOST 为 Github 调用的回调接口。
2. 服务器将在http://localhost:8080上运行
3. 你可以配置Caddy将https://ci.zouying.work反向代理到这个内部端口
4. GitHub OAuth回调URL应设置为https://ci.zouying.work/login


```bash
docker compose up -d
```



# clickhouse docker-compose

Ref:

  - [clickhouse-server](https://hub.docker.com/r/yandex/clickhouse-server/)
  - [ClickHouse](https://github.com/ClickHouse/ClickHouse/blob/master/docker-compose.yml)


## run

start instance:

```bash
docker run -d --name some-clickhouse-server --ulimit nofile=262144:262144 yandex/clickhouse-server
```

## connect

connect to server from native client:

```bash
docker run -it --rm --link some-clickhouse-server:clickhouse-server yandex/clickhouse-client --host clickhouse-server
```


## start

start clickhouse server first:

```bash
# docker run -d --name clickhouse-server --ulimit nofile=262144:262144 -p 9000:9000 yandex/clickhouse-server


mkdir etc
mkdir data

# 挂在当前目录到 /work 下面
docker run -it --rm --entrypoint=/bin/bash -v $PWD:/work --privileged=true --user=root yandex/clickhouse-server

# cp /etc/clickhouse-server/* /work/etc/
# 进行拷贝

```


运行

```bash
docker run -d --name clickhouse-server --ulimit nofile=262144:262144 -p 9000:9000 -p 8123:8123 -p 9009:9009 -v $PWD/etc:/etc/clickhouse-server \
-v $PWD/data:/var/lib/clickhouse --privileged=true --user=root yandex/clickhouse-server
```


客户端连接：

```bash
docker run -it --rm --link clickhouse-server:clickhouse-server yandex/clickhouse-client --host clickhouse-server --password
```

默认用户名为：
default


权限：

在users.conf中，放开注释：

```bash
access_management 
```






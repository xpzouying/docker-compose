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


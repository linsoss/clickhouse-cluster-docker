# ClickHouse Cluster Docker Compose

![4cc49380-82ee-11ea-9baf-d971dbaafe63](https://cdn.jsdelivr.net/gh/Al-assad/md-img@master/bucket-3/202011271720.png)

**[English](README.md)** ｜ [**中文**](README-CN.md)

<br>

用于快速构建 ClickHouse Server 集群环境的 docker-compose 脚本，基于 [yandex/clickHouse-server](yandex/clickHouse-server) 官方镜像，支持自定义 clickhosue-server 版本，默认组件版本如下：

* zookeeper：3.6；
* clickHouse-server：20.11 ；

### 快速开始

```shell
git clone https://github.com/Al-assad/clickhouse-cluster-docker.git
docker-compose up
```

默认创建的集群节点为 1 个 zookeeper 节点，3 个 clickhosue-server 节点（3 分片、1 副本）：

![image-20201127163735143](https://cdn.jsdelivr.net/gh/Al-assad/md-img@master/bucket-3/202011271637.png)

### 宿主机连接 ClickHosue 集群

1. 通过宿主机 ip 访问：

   ```shell
   clickhouse-server-ch01    127.0.0.1:8124
   clickhouse-server-ch02    127.0.0.1:8125
   clickhouse-server-ch03    127.0.0.1:8126
   ```

2. 通过 docker 子网 ip 访问：

   如果宿主机为 MacOS，可以通过 [mac-docker-connector](https://github.com/wenjunxiao/mac-docker-connector) 项目直接访问是 docker 子网络：

   ```shell
   clickhouse-server-ch01    172.18.1.5:8123
   clickhouse-server-ch02    172.18.1.6:8123
   clickhouse-server-ch03    172.18.1.7:8123
   ```

可以通过 DBeaver 或者 clickhosue-client 连接访问 clickhosue-server 集群。

### 其他集群模式

```shell
# zookeeper 单节点，clickhosue 3 分片 1 副本
docker-compose -f clickhosue_1zk-3shard-1replica up

# zookeeper 单节点，clickhosue 3 分片 3 副本
docker-compose -f clickhosue_1zk-3shard-3replica up

# zookeeper 3 节点，clickhosue 3 分片 1 副本
docker-compose -f clickhosue_3zk-3shard-1replica up

# zookeeper 3 节点，clickhosue 3 分片 3 副本
docker-compose -f clickhosue_3zk-3shard-3replica up
```

此外可以通过直接修改 `ch-conf/metrika_ch01.xml`、`ch-conf/metrika_ch02.xml`、`ch-conf/metrika_ch03.xml` 来修改 3 个 ch 节点的 metrika 配置。

### 其他 ClickHouse 版本

可以通过修改 `CLICKHOUSE_VERSION` 环境变量来自定义 CH 镜像版本，注意需要使用 yandex/clickhosue-server 的对应镜像版本。

```shell
# 使用 clickhouse-server 20.10 版本
export CLICKHOUSE_VERSION=20.10 && docker-compose config
```





<br>

<br>
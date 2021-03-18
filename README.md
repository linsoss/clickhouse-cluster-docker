# ClickHouse Cluster Docker Compose

![4cc49380-82ee-11ea-9baf-d971dbaafe63](https://github.com/Al-assad/md-img/blob/master/bucket-3/202011271720.png)

**[English](README.md)** ｜ [**中文**](README-CN.md)

<br>

Docker-compose script for quickly building a ClickHouse cluster environment, based on the official [yandex/clickhouse-server](https://hub.docker.com/r/yandex/clickhouse-server) image, supports custom clickhosue-server versions. 

The default component version is as follows ：

* **zookeeper**：3.6；
* **clickHouse-server**：20.11 ；

### Quick Start

```shell
git clone https://github.com/Al-assad/clickhouse-cluster-docker.git
docker-compose up
```

The default created cluster nodes includes 1 zookeeper node, 3 clickhosue-server nodes (3 shards, 1 replica each node).

![image-20201127163735143](https://cdn.jsdelivr.net/gh/Al-assad/md-img@master/bucket-3/202011271637.png)

### Connect ClickHouse Cluster from Host Machine

1. Access via host machine ip: 

   ```shell
   clickhouse-server-ch01    127.0.0.1:8124
   clickhouse-server-ch02    127.0.0.1:8125
   clickhouse-server-ch03    127.0.0.1:8126
   ```

2. Access via docker subnetwork ip:

   If your docker host machine is MacOS,  you can access the docker subnetwork directly through the project [wenjunxiao/mac-docker-connector](https://github.com/wenjunxiao/mac-docker-connector). 

   ```shell
   clickhouse-server-ch01    172.18.1.5:8123
   clickhouse-server-ch02    172.18.1.6:8123
   clickhouse-server-ch03    172.18.1.7:8123
   ```

Then you can connect the clickhouse-server cluster through DBeaver GUI Tool or clickhosue-client command-line tool. Enjoy it : ) 

### Other Cluster Mode

```shell
# single zookeeper node，clickhosue 3 shards and 1 replica
docker-compose -f clickhosue_1zk-3shard-1replica up

# single zookeeper node，clickhosue 3 shards and 3 replicas
docker-compose -f clickhosue_1zk-3shard-3replica up

# 3 zookeeper 3 nodes，clickhosue 3 shards and 1 replica
docker-compose -f clickhosue_3zk-3shard-1replica up

# 3 zookeeper 3 nodes，clickhosue 3 shards and 3 replicas
docker-compose -f clickhosue_3zk-3shard-3replica up
```

In addition, you can also modify the metrika configuration for the three CH nodes by directly modifying ```ch-conf/metrika_ch01.xml```,  ```ch-conf/metrika_ch02.xml```,  ```and ch-conf/metrika_ch03.xml```.

### Other ClickHouse Image Version

You can customize the CH image version by modifying the environment variable ```CLICKHOUSE_VERSION```.

```shell
# use clickhouse-server v20.10
export CLICKHOUSE_VERSION=20.10 && docker-compose config
```

<br>

<br>


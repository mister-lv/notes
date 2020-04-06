# Docker redis 集群搭建

Redis 集群是一个提供在多个 Redis 节点间共享数据的程序集。

Redis 集群并不支持处理多个 keys 的命令,因为这需要在不同的节点间移动数据，从而达不到像 Redis 那样的性能，在高负载的情况下可能会导致不可预料的错误.

Redis 集群通过分区来提供一定程度的可用性，在实际环境中当某个节点宕机或者不可达的情况下继续处理命令。

Redis 集群的优势:

- 自动分割数据到不同的节点上。
- 整个集群的部分节点失败或者不可达的情况下能够继续处理命令。

Redis 集群没有使用一致性 hash, 而是引入了哈希槽的概念。Redis 集群有 16384 个哈希槽，每个 key 通过 CRC16 校验后对 16384 取模来决定放置哪个槽，集群的每个节点负责一部分 hash 槽。

### 1、下载 redis.conf

下载地址：https://github.com/antirez/redis/blob/unstable/redis.conf

### 2、修改 redis.conf

**开启集群功能：**

```
cluster-enabled yes
```

**设置节点端口：**

```
port 6391
```

**节点超时时间，单位毫秒:**

```
cluster-node-timeout 15000
```

**集群内部配置文件:**

```
cluster-config-file "nodes-6379.conf"
```

### 3、编写 docker-compose.yml

节点规划图如下：

[![img](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster1.png)](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster1.png)

配置如下：

```
version: "3.6"
services:
  redis-master1: 
     image: redis:5.0 # 基础镜像
     container_name: redis-master1 # 容器服务名
     working_dir: /config # 工作目录
     environment: # 环境变量
       - PORT=6391 # 跟 config/nodes-6391.conf 里的配置一样的端口
     ports: # 映射端口，对外提供服务
       - "6391:6391" # redis 的服务端口
       - "16391:16391" # redis 集群监控端口
     stdin_open: true # 标准输入打开
     networks: # docker 网络设置
        redis-master:
            ipv4_address: 172.50.0.2
     tty: true
     privileged: true # 拥有容器内命令执行的权限
     volumes: ["/c/project/docker/redis/config:/config"] # 映射数据卷，配置目录
     entrypoint: # 设置服务默认的启动程序
       - /bin/bash
       - redis.sh
  redis-master2:
       image: redis:5.0
       working_dir: /config
       container_name: redis-master2
       environment:
              - PORT=6392
       networks:
          redis-master:
             ipv4_address: 172.50.0.3
       ports:
         - "6392:6392"
         - "16392:16392"
       stdin_open: true
       tty: true
       privileged: true
       volumes: ["/c/project/docker/redis/config:/config"]
       entrypoint:
         - /bin/bash
         - redis.sh
  redis-master3:
       image: redis:5.0
       container_name: redis-master3
       working_dir: /config
       environment:
              - PORT=6393
       networks:
          redis-master:
            ipv4_address: 172.50.0.4
       ports:
         - "6393:6393"
         - "16393:16393"
       stdin_open: true
       tty: true
       privileged: true
       volumes: ["/c/project/docker/redis/config:/config"]
       entrypoint:
         - /bin/bash
         - redis.sh
  redis-slave1:
       image: redis:5.0
       container_name: redis-slave1
       working_dir: /config
       environment:
            - PORT=6394
       networks:
          redis-slave:
             ipv4_address: 172.30.0.2
       ports:
         - "6394:6394"
         - "16394:16394"
       stdin_open: true
       tty: true
       privileged: true
       volumes: ["/c/project/docker/redis/config:/config"]
       entrypoint:
         - /bin/bash
         - redis.sh
  redis-salve2:
       image: redis:5.0
       working_dir: /config
       container_name: redis-salve2
       environment:
             - PORT=6395
       ports:
         - "6395:6395"
         - "16395:16395"
       stdin_open: true
       networks:
          redis-slave:
              ipv4_address: 172.30.0.3
       tty: true
       privileged: true
       volumes: ["/c/project/docker/redis/config:/config"]
       entrypoint:
         - /bin/bash
         - redis.sh
  redis-salve3:
       image: redis:5.0
       container_name: redis-slave3
       working_dir: /config
       environment:
          - PORT=6396
       ports:
         - "6396:6396"
         - "16396:16396"
       stdin_open: true
       networks:
          redis-slave:
            ipv4_address: 172.30.0.4
       tty: true
       privileged: true
       volumes: ["/c/project/docker/redis/config:/config"]
       entrypoint:
         - /bin/bash
         - redis.sh
networks:
  redis-master:
     driver: bridge # 创建一个docker 的桥接网络
     ipam:
       driver: default
       config:
          -
           subnet: 172.50.0.0/16
  redis-slave:
       driver: bridge
       ipam:
         driver: default
         config:
            -
             subnet: 172.30.0.0/16
```

### 4、编写 redis 默认的启动脚本

创建文件 config/redis.sh，内容如下：

```
redis-server  /config/nodes-${PORT}.conf
```

### 5、启动集群

启动服务命令如下：

```
$ docker-compose up -d
```

[![img](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster2.png)](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster2.png)

查看服务运行：

```
$ docker ps
```

[![img](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster3.png)](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster3.png)

初始化集群（这一步开始命令须在 redis5.0 及以上版本运行）。

创建 3 主 3 从的 redis 集群：

```
$ redis-cli --cluster create 192.168.99.100:6391 192.168.99.100:6392 192.168.99.100:6393 192.168.99.100:6394 192.168.99.100:6395 192.168.99.100:6396 --cluster-replicas 1
```

[![img](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster4.png)](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster4.png)

输入 yes，确认要初始化：

[![img](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster5.png)](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster5.png)

查看初始化结果。

进入 redis-cli, 查看节点信息：

```
root@ae9e587e62f4:/data# redis-cli -h 192.168.99.100 -p 6391
192.168.99.100:6391> cluster nodes
```

[![img](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster6.png)](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster6.png)

上图显示，redis 集群符合预期。

### 6、测试集群

普通模式连接：由于 test 根据哈希槽计算，是分布在 6392 服务上。所以这里会提示转到 6392。

```
root@ae9e587e62f4:/data# redis-cli -h 192.168.99.100 -p 6391
```

[![img](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster7.png)](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster7.png)

集群模式连接：以下例子显示操作正常。

```
root@ae9e587e62f4:/data# redis-cli -c -h 192.168.99.100 -p 6391 set test 1
root@ae9e587e62f4:/data# redis-cli -c -h 192.168.99.100 -p 6391 get test
```

[![img](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster8.png)](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster8.png)

集群模式连接读写正常，集群搭建成功。

本例涉及到的文件下载：

[docker-redis](https://www.runoob.com/wp-content/uploads/2019/11/docker-redis-cluster.zip)
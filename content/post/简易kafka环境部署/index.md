---
title: 部署简易Kafka测试环境
slug: 
date: 2023-11-10 00:00:00+0000
# image: BWeLyHqW.jpg
categories:
    - 技术分享
tags:
    - Linux
    - Dokcer
    - Kafka
weight: 2       # You can add weight to some posts to override the default sorting (date descending)
---

因为Kafka依赖于[zookeeper](https://so.csdn.net/so/search?q=zookeeper&spm=1001.2101.3001.7020)做分布式管理，因此需要先安装zookeeper

1. zookeeper启动

    ```docker
    docker run -d --name zookeeper -p 2181:2181 \
    -t wurstmeister/zookeeper
    ```
2. kafka启动
    ```docker
    docker run -d --name kafka -p 9092:9092 -e KAFKA_BROKER_ID=0 \
    -e KAFKA_ZOOKEEPER_CONNECT=124.223.***.176:2181 \
    -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://124.223.***.176:9092 \
    -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 \
    -t wurstmeister/kafka
    ```
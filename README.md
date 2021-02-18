# OpenJDK Docker
![Docker Pulls](https://img.shields.io/docker/pulls/bincent/openjdk.svg?maxAge=60480)

### 简介
基于 官方 OpenJDK镜像构建，默认为 `/data/app.jar`；

### Version
- 1.8
- 11
- 15

### Docker Composer
```yaml
version: '3'

services:
  java:
    image: bincent/openjdk:1.8
    container_name: java
    restart: always
    environment: # 默认配置
      TIME_ZONE: "Asia/Shanghai"
      BASE_DIR: "/data"   // 注意：修改此路径，需同步修改volumes对应路径
      JVM_XMS: "2g"
      JVM_XMX: "2g"
      JVM_XMN: "1g"
      JVM_MS: "128m"
      JVM_MMS: "320m"
      JVM_PLG: false # GC日志打印
    volumes:
      - ./logs:/data/logs
      - ./config:/data/config:ro
      - ./target/data-service-0.0.1-SNAPSHOT.jar:/data/app.jar
    ports:
      - 8080:8080/tcp
    network_mode: bridge
```
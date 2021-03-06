# OpenJDK Docker
![Docker Pulls](https://img.shields.io/docker/pulls/bincent/openjdk.svg?maxAge=60480)

### 简介
基于 官方 OpenJDK镜像构建，默认为 `/data/app.jar`；

### Version
- 1.8
- 11
- 16

### Docker Run
```shell
docker run -p 8080:8080 \
  -v ./target/data-service-0.0.1-SNAPSHOT.jar:/data/app.jar \
  -v ./config:/data/config \
  -v ./logs:/data/logs \
  --env JVM_XMS=1024m \
  --env JVM_XMX=1024m \
  --env JVM_XMN=256m \
  --env JVM_MS=256m \
  --env JVM_MMS=256m \
  --name projectname bincent/openjdk:1.8 
```

### Docker Composer
#### docker-composer.yml 示例
```yaml
version: '3'

services:
  java:
    image: bincent/openjdk:1.8
    container_name: java
    restart: always
    environment: # 默认配置
      TIME_ZONE: Asia/Shanghai
      BASE_DIR: /data   # 注意：修改此路径，需同步修改volumes对应路径
      JAVA_OPTS: -XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=128m -Xms1024m -Xmx1024m -Xmn256m -Xss256k -XX:SurvivorRatio=8 -XX:+UseConcMarkSweepGC # JAVA启动参数
    volumes:
      - ./logs:/data/logs
      - ./config:/data/config:ro
      - ./target/data-service-0.0.1-SNAPSHOT.jar:/data/app.jar
    ports:
      - 8080:8080/tcp
    network_mode: bridge
```

#### 执行命令

```shell
docker-composer -f docker-composer.yml up -d
```
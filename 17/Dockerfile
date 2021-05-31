FROM openjdk:17-jdk-slim

# set environment
ENV TIME_ZONE="Asia/Shanghai" \
    BASE_DIR="/data" \
    JAVA_OPTS="-XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=128m -Xms1024m -Xmx1024m -Xmn256m -Xss256k -XX:SurvivorRatio=8 -XX:+UseConcMarkSweepGC" 

WORKDIR /$BASE_DIR

RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list \
	&& apt-get update && apt-get -y upgrade \
    && ln -snf /usr/share/zoneinfo/$TIME_ZONE /etc/localtime && echo $TIME_ZONE > /etc/timezone \
    && mkdir $BASE_DIR/config && mkdir $BASE_DIR/logs \
    && rm -rf /var/lib/apt/lists/*

CMD java -Djava.security.egd=file:/dev/./urandom -jar $BASE_DIR/app.jar  $JAVA_OPTS --appendonly yes
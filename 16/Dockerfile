FROM openjdk:16-slim-buster

# set environment
ENV TIME_ZONE="Asia/Shanghai" \
    BASE_DIR="/data" \
    JAVA_OPTS="-Xms2g -Xmx2g -Xmn1g -XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=320m" 

WORKDIR /$BASE_DIR

RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list
RUN set -eux; \
	apt-get update; \
	apt-get -y upgrade;
RUN ln -snf /usr/share/zoneinfo/$TIME_ZONE /etc/localtime && echo $TIME_ZONE > /etc/timezone

CMD java -Djava.security.egd=file:/dev/./urandom -jar $BASE_DIR/app.jar  $JAVA_OPTS --appendonly yes
FROM openjdk:8u282-slim-buster

# set environment
ENV TIME_ZONE="Asia/Shanghai" \
    BASE_DIR="/data" \
    JVM_XMS="2g" \
    JVM_XMX="2g" \
    JVM_XMN="1g" \
    JVM_MS="128m" \
    JVM_MMS="320m" 
    
ENV JAVA_OPT = -Xms$JVM_XMS -Xmx$JVM_XMX -Xmn$JVM_XMN -XX:MetaspaceSize=$JVM_MS -XX:MaxMetaspaceSize=$JVM_MMS

WORKDIR /$BASE_DIR

RUN ln -snf /usr/share/zoneinfo/$TIME_ZONE /etc/localtime && echo $TIME_ZONE > /etc/timezone

CMD java -Djava.security.egd=file:/dev/./urandom -jar $BASE_DIR/app.jar  $JAVA_OPT --appendonly yes
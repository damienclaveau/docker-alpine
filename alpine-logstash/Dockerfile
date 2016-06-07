FROM jolokia/alpine-jre-8
MAINTAINER kost, https://github.com/kost/docker-alpine

# Set environment variables
ENV LOGSTASH_NAME logstash
ENV LOGSTASH_VERSION 2.3.1
ENV LOGSTASH_URL http://download.elastic.co/$LOGSTASH_NAME/$LOGSTASH_NAME/$LOGSTASH_NAME-all-plugins-$LOGSTASH_VERSION.tar.gz
ENV LOGSTASH_CONFIG /opt/$LOGSTASH_NAME/etc/logstash.json

RUN apk update \
 && apk add bash openssl \
 && cd /tmp \
 && wget $LOGSTASH_URL \
 && mkdir -p /opt \
 && tar xzf /tmp/$LOGSTASH_NAME-all-plugins-$LOGSTASH_VERSION.tar.gz -C /opt/ \
 && ln -s /opt/$LOGSTASH_NAME-$LOGSTASH_VERSION /opt/$LOGSTASH_NAME \
 && rm -rf /tmp/*.tar.gz /var/cache/apk/* \
 && mkdir -p /scripts/pre-exec.d \
 && mkdir /scripts/pre-init.d \
 && chmod -R 755 /scripts

# Add logstash config file
ADD etc /opt/$LOGSTASH_NAME/etc
ADD scripts /scripts

WORKDIR /opt/$LOGSTASH_NAME

ENTRYPOINT ["/scripts/run.sh"]

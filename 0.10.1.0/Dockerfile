FROM anapsix/alpine-java

MAINTAINER bin liu

RUN apk add --update wget coreutils

ENV KAFKA_VERSION 2.11-0.10.1.0
RUN cd /tmp && \
    wget http://ftp.riken.jp/net/apache/kafka/0.10.1.0/kafka_${KAFKA_VERSION}.tgz && \
    tar xfz kafka_${KAFKA_VERSION}.tgz -C /opt && \
    rm /tmp/kafka_${KAFKA_VERSION}.tgz

VOLUME ["/kafka", "/zookeeper"]
EXPOSE 9092 2181

ENV KAFKA_HOME /opt/kafka_${KAFKA_VERSION}


ADD config/ $KAFKA_HOME/config/

ADD start-kafka.sh /start-kafka.sh
RUN chmod +x /start-kafka.sh
CMD ["/start-kafka.sh"]

# Install Ruby
RUN apk update && apk upgrade && apk --update add \
    ruby ruby-irb ruby-rake ruby-io-console ruby-bigdecimal ruby-json ruby-bundler ruby-dev gcc build-base\
    libstdc++ tzdata bash ca-certificates \
    &&  echo 'gem: --no-document' > /etc/gemrc \
    && rm -rf /var/cache/apk/*

# Install airbnb/kafkat
RUN gem install kafkat
COPY etc/kafkatcfg /etc/kafkatcfg
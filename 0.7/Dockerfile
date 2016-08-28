FROM armhf/ubuntu
MAINTAINER Theo Pack <tf.pack@gmail.com>

ENV CONSUL_VERSION=0.7.0-rc1

RUN apt-get update && apt-get -qy install \
 wget unzip
WORKDIR /root/
RUN wget \
 https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_arm.zip
RUN mkdir /data

ADD https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_web_ui.zip /tmp/webui.zip
RUN mkdir /ui && cd /ui && unzip /tmp/webui.zip && rm /tmp/webui.zip

RUN unzip consul*.zip -d /usr/local/bin/

RUN consul version

EXPOSE 8300 8301 8301/udp 8302 8302/udp 8400 8500 53/udp

VOLUME ["/data"]
ADD ./config /config/

ENV DNS_RESOLVES consul
ENV DNS_PORT 8600

ENTRYPOINT ["/usr/local/bin/consul", "agent", "-config-dir=/config"]

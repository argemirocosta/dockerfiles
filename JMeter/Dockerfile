FROM debian:latest

LABEL version="1.0" description="debian/jmeter&telegraf"

#BAIXANDO E ATUALIZANDO GERENCIADOR E PACOTES
RUN apt-get update && apt-get install wget apt-transport-https gnupg2 procps -y

#BAIXANDO E DESCOMPACTANDO JMETER
RUN wget https://downloads.apache.org//jmeter/binaries/apache-jmeter-5.4.1.tgz 
RUN tar zxvf apache-jmeter-5.4.1.tgz && \
  mv apache-jmeter-5.4.1 /opt/
WORKDIR /opt/apache-jmeter-5.4.1/bin
COPY Example.jmx ./

#BAIXANDO E CONFIGURANDO O TELEGRAF
RUN wget -qO- https://repos.influxdata.com/influxdb.key | apt-key add - && \
  echo "deb https://repos.influxdata.com/debian buster stable" | tee /etc/apt/sources.list.d/influxdb.list
RUN apt-get update && apt-get install telegraf default-jre -y
RUN apt-get clean
COPY telegraf.conf /usr/local/etc/telegraf.conf

#DEFININDO VARIÁVEIS DE AMBIENTE
ENV JMETER_HOME=/opt/apache-jmeter-5.4.1
ENV JMETER_BIN=/opt/apache-jmeter-5.4.1/bin
ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/apache-jmeter-5.4.1/bin:$JAVA_HOME

#ADICIONANDO PLUGINS AO JMETER
COPY jmeter-plugins-manager-1.6.jar /opt/apache-jmeter-5.4.1/lib/ext 
COPY ./basic-graphs/jmeter-plugins-cmn-jmeter-0.4.jar /opt/apache-jmeter-5.4.1/lib 
COPY ./basic-graphs/ext/jmeter-plugins-graphs-basic-2.0.jar /opt/apache-jmeter-5.4.1/lib/ext
COPY ./basic-graphs/ext/jmeter-plugins-manager-0.20.jar /opt/apache-jmeter-5.4.1/lib/ext 
COPY ./custom-thread-groups/jmeter-plugins-cmn-jmeter-0.6.jar /opt/apache-jmeter-5.4.1/lib 
COPY ./custom-thread-groups/ext/jmeter-plugins-casutg-2.9.jar /opt/apache-jmeter-5.4.1/lib/ext
COPY ./custom-thread-groups/ext/jmeter-plugins-manager-1.3.jar /opt/apache-jmeter-5.4.1/lib/ext

#INICIANDO O SERVIÇO DO TELEGRAF
ENTRYPOINT service telegraf start && bash
FROM centos:latest

LABEL version="1.0" description="centos/tomcat"

#CRIANDO PASTA PARA O TOMCAT
RUN mkdir /opt/tomcat/
WORKDIR /opt/tomcat

#BAIXANDO E INSTALANDO O TOMCAT
RUN curl -O https://downloads.apache.org/tomcat/tomcat-8/v8.5.61/bin/apache-tomcat-8.5.61.tar.gz &&\
tar xvfz apache-tomcat-8.5.61.tar.gz &&\
mv apache-tomcat-8.5.61/* /opt/tomcat/.

#COPIANDO ARQUIVOS DE CONFIGURAÇÃO
WORKDIR /opt/tomcat/conf/
RUN rm tomcat-users.xml
COPY tomcat-users.xml ./
WORKDIR /opt/tomcat/webapps/manager/WEB-INF
RUN rm web.xml
COPY web.xml ./
WORKDIR /opt/tomcat/webapps/manager/META-INF
RUN rm context.xml
COPY context.xml ./

#INSTALANDO O JAVA
RUN yum -y install java
RUN java -version

#INSTALANDO O VIM
RUN  yum install vim-enhanced -y

WORKDIR /opt/tomcat/webapps

#BAIXANDO EXEMPLO DE WAR PARA TESTE DE DEPLOY
RUN curl -O -L https://github.com/AKSarav/SampleWebApp/raw/master/dist/SampleWebApp.war

WORKDIR /opt/tomcat/bin

EXPOSE 8080
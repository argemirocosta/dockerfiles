# Tomcat Dockerfile

Dockerfile for Apache Tomcat

## Getting started

Clone the project:

```shell
git clone https://github.com/argemirocosta/dockerfiles.git
```

Inside the folder:

```shell
docker build . -t name_tag
```

```shell
docker run --rm -it -p 8081:8080 id_created bash  
```

Inside the image:
```shell
./startup.sh 
```

Acess http://localhost:8081/SampleWebApp/ in browser.

## Description

Dockerfile with Java and Apache Tomcat in a CentOS.

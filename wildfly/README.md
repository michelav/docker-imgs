## Wildfly Images

This repository contains some handy Wildfly images.

### Tags

- [16-alpine](16/alpine/Dockerfile)
- [16-stretch](16/stretch/Dockerfile)

Both images uses OpenJDK11.

### Usage

All images have an administrator account created: admin \ admin. Also, the images exposes 9990 and 8080
as management and application ports respectively. You may change default configuration by passing 
server-config as parameter:

```
$ docker run -p 9990:9990 -p 8080:8080 michelav/wildfly:16-stretch --server-config=standalone-full.xml
```
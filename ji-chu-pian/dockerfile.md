# Dockerfile

## demo

```
FROM ubuntu:18.04
COPY . /app
RUN make /app
CMD python /app/app.py
```

## base image

```
FROM centos:7
```

## 添加文件

## 运行指令

## CMD
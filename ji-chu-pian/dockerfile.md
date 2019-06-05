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

```
// COPY
// 将当前目录下的文件复制到image中
COPY . /app

// ADD
```

## 运行指令

## CMD
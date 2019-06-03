# image相关

image是docker启动容器的镜像文件。
image里面包含了操作系统，安装包，库，以及代码。
image同代码一样，也是有tag的，默认是latest。

## 查看image

```
// image list
docker image ls

// history
docker image history centos:latest
docker image history mysql:latest

// 详细信息 inspect
docker image inspect centos
```

## pull

## push

## build

## remove
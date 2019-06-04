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

```
docker image pull centos
docker image pull centos:7
docker image pull registry-ip:port/centos
```

## push

```
docker image push centos
docker image push centos:7
docker image push registry-ip:port/centos
```

## build

## tag

```
// docker image tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
docker image tag centos my_centos:7
```

## remove

```
// rm
docker image rm centos

// prune, remove unused image
docker image prune
```
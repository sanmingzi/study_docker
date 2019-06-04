# container相关

## 查看container的运行状态

```
// 查看正在运行的container
docker container ls

// 查看所有container
docker container ls -a
docker container ls --all

// 只显示container id
docker container ls -q
```

## 创建

```
// https://docs.docker.com/engine/reference/commandline/container_create/
docker container create --name my_centos centos
```

## 重命名

```
// docker container rename CONTAINER NEW_NAME
docker container rename my_centos new_centos
```

## 启动

```
// https://docs.docker.com/engine/reference/commandline/container_start/
docker container start my_centos

// run
docker container run -d -it --name my_centos centos:latest
```

## 停止

```
// https://docs.docker.com/engine/reference/commandline/container_stop/
docker container stop my_centos

// kill
docker container kill my_centos
```

## 重启

```
docker container restart my_centos
```

## 删除

```
// remove
docker container rm my_centos

// prune, remove all unused container
docker container prune
```

## 查看container的资源使用情况

```
// https://docs.docker.com/engine/reference/commandline/container_stats/
docker container stats my_centos

// 查看所有container的资源使用情况
docker container stats -a
```

## 进入运行中的container

```
// attach
docker container attach my_centos

// exec
docker container exec -it my_centos /bin/bash
```

## 查看container的日志

```
docker container logs -f my_centos
```

## container与local system之间的文件传输

```
// docker container cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
docker cp docker-start.cmd my_centos:/root

// docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH
docker container cp my_centos:/root/docker-start.cmd test.cmd
```

## container中的文件持久化

## 将container保存为image

```
// docker container commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
```
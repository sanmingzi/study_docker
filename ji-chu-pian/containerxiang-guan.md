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
docker container create --name myCentos centos
```

## 启动

## 停止

## 重启

## 删除

## 进入运行中的container

## 进入非运行中的container

## 查看container的日志

## container与local system之间的文件传输

## container中的文件持久化

## 将container保存为image
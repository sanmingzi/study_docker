# docker在windows上的安装与配置

## 安装

- 安装docker

对于非pro版的windows来讲，需要安装docker tool。

## 启动

```
安装完成之后运行脚本：C:\Program Files\Docker Toolbox\start.sh

运行命令：docker-machine ls

如果看到如下内容：
NAME      ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER     ERRORS
default   *        virtualbox   Running   tcp://192.168.99.100:2376           v18.09.6

说明docker daemon已经成功启动，并且监听的是2376端口。
此时我们就可以在终端通过docker的cli与docker daemon进行交互了。
```


## 配置

- 镜像源
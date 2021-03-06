# docker在windows上的安装与配置

## 安装

- 安装docker

对于非pro版的windows来讲，需要安装[docker tool](https://docs.docker.com/toolbox/toolbox_install_windows/)。

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

## 修改镜像源

由于网络原因，我们需要将镜像源改成国内的。

```
第一步，进入docker-daemon
docker-machine ssh

第二步，配置文件
sudo vi /etc/docker/daemon.json
{
  "registry-mirrors": ["https://registry.docker-cn.com",
                       "https://hub-mirror.c.163.com",
                       "https://docker.mirrors.ustc.edu.cn"]
}

保存文件，退出

第三步，重启
docker-machine restart

第四步，检查是否修改成功
运行命令：docker info

如果看到如下内容：
Registry Mirrors:
 https://registry.docker-cn.com/
 https://hub-mirror.c.163.com/
 https://docker.mirrors.ustc.edu.cn/
 
说明镜像源修改成功
```

# shadowsocks 为 docker 提供代理

## 参考

- [docker http proxy](https://www.jianshu.com/p/13f4b23824d8)

## 为什么要为 docker 提供代理

```m
原因只有一个，慢！！！

在大陆访问 docker 是很慢的，但是在香港访问却没有问题。
不知道为什么要屏蔽 docker，也不知道为什么要屏蔽 github。

网上大量的方法是使用国内镜像，有网易镜像，中科大镜像等，我尝试过了，pull了好几次，都是到一半的时候 crash，一下午的时间花花的溜走了。

恰好手上有一个shadowsocks，想着也许使用 proxy 能够解决这个问题，没想到成功了。
```

## 我的环境

```m
windows wsl2
Ubuntu 18.04 TLS
Docker version 19.03.12
```

## privoxy

```m
shadowsocks 是 socks5 的代理。

privoxy 可以将收到的http请求转给一个 socks 代理，也就是 shadowsocks。
```

- 安装

```
sudo apt-get install privoxy
```

- 配置

```
shadowsocks 监听的端口是 1090
privoxy 默认监听的端口是 8118

在 /etc/privoxy/config 文件最后加一句
forward-socks5 / 127.0.0.1:1090 .

在docker配置 /etc/default/docker 加一句
export http_proxy="http://127.0.0.1:8118"
```

- 重启

```
sudo service privoxy restart
sudo service docker restart
```

# Dockerfile

## Simple Demo

```
FROM ubuntu:18.04
COPY . /app
RUN make /app
CMD python /app/app.py
```

## FROM...AS

我们可以使用FROM...AS构建一个临时的base image，然后在里面安装一些编译需要的东西。
最后使用真正的base image，将编译好的东西COPY过去。
这样的好处在于能够是最终的image的大小是正好合适的: Don’t install unnecessary packages

```
FROM golang:1.11-alpine AS build

# Install tools required for project
# Run `docker build --no-cache .` to update dependencies
RUN apk add --no-cache git
RUN go get github.com/golang/dep/cmd/dep

# List project dependencies with Gopkg.toml and Gopkg.lock
# These layers are only re-built when Gopkg files are updated
COPY Gopkg.lock Gopkg.toml /go/src/project/
WORKDIR /go/src/project/
# Install library dependencies
RUN dep ensure -vendor-only

# Copy the entire project and build it
# This layer is rebuilt when a file changes in the project directory
COPY . /go/src/project/
RUN go build -o /bin/project

# This results in a single layer image
FROM scratch
COPY --from=build /bin/project /bin/project
ENTRYPOINT ["/bin/project"]
CMD ["--help"]
```

如果我们不使用这种方法，而是在同一个image中先安装包，然后再删除包，那结果是整个image会变得很大。因为image是由layer堆积而成的，安装包的时候那个layer的大小就已经固定了，而后来的操作只会新增layer，而不会影响原有的layer。

## COPY && ADD

```
// COPY
// 将当前目录下的文件复制到image中
COPY . /app

// ADD
```

## RUN

```
RUN apt-get update && apt-get install -y \
    aufs-tools \
    automake \
    build-essential \
    curl \
    dpkg-sig \
    libcap-dev \
    libsqlite3-dev \
    mercurial \
    reprepro \
    ruby1.9.1 \
    ruby1.9.1-dev \
    s3cmd=1.1.* \
 && rm -rf /var/lib/apt/lists/*
```

## CMD && ENTRYPOINT

## EXPOSE

## ENV

有些软件需要将其运行路径添加到环境变量中去才能运行。

```
ENV PG_MAJOR 9.3
ENV PATH /usr/local/postgres-$PG_MAJOR/bin:$PATH
```

ENV命令会创建一个新的layer，正是因为这个原因，所以即使我们在future layer中unset这个环境变量，但是该变量在当前layer中依旧存在。

```
FROM alpine
ENV ADMIN_USER="mark"
RUN echo $ADMIN_USER > ./mark
RUN unset ADMIN_USER
```

```
$ docker run --rm test sh -c 'echo $ADMIN_USER'

mark
```

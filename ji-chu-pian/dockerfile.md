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

## COPY and ADD

```
// COPY
// 将当前目录下的文件复制到image中
COPY . /app

// ADD
```

## RUN

## CMD
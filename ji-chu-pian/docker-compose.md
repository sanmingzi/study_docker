# docker-compose

[compose-file](https://docs.docker.com/compose/compose-file/)

## demo

```
version: "3.7"

services:
  webapp:
    build:
      context: ./dir
      dockerfile: Dockerfile-alternate
      args:
        buildno: 1 // should define this arg in Dockerfile first
    image: webapp:tag
```

##
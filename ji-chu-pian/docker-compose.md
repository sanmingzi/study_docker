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
    image: webapp:tag
```

##
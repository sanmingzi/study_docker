# docker-compose

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
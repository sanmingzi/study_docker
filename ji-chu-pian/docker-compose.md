# docker-compose

[compose-file](https://docs.docker.com/compose/compose-file/)

## demo

```
version: "3.7"

services:
  webapp:
    depends_on:
      - mysql
      - redis
    build:
      context: ./dir
      dockerfile: Dockerfile-alternate
      args:
        buildno: 1 // should define this arg in Dockerfile first
      labels:
        com.example.description: "Accounting webapp"
        com.example.department: "Finance"
        com.example.label-with-empty-value: ""
    image: webapp:tag
    container_name: my-web-container
    ports:
      - "8080:80"
    networks:
      - overlay
    command: bundle exec thin -p 3000
  redis:
    image: redis
    deploy:
      replicas: 6
      mode: global
  mysql:
    image: mysql
    volumes:
       - db-data:/var/lib/mysql/data
    networks:
       - overlay
    
volumes:
  db-data:

networks:
  overlay:
```

##
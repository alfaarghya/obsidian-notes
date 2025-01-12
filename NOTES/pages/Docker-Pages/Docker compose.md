# Docker compose

## Start our application with `docker-compose.yml`

```docker
version: '3.8'
services:
  mongodb:
    image: mongo
    container_name: mongodbServer
    ports:
      - "27017:27017"
    volumes:
      - mongodb_data:/data/db

  backend22:
    image: backend
    container_name: backend_app
    depends_on:
      - mongodb
    ports:
      - "3000:3000"
    environment:
      MONGO_URL: "mongodb://mongodbServer:27017/testDB"

volumes:
  mongodb_data:

```

## Start an application for development(hot-reload) using docker

```docker
version: '3.8'

services:
  app:
    build: .
    container_name: alfa-leetcode-api-docker
    ports:
      - '3000:3000'
    restart: always
    environment:
      - WDS_SOCKET_HOST=127.0.0.1 
      - CHOKIDAR_USEPOLLING=true
      - WATCHPACK_POLLING=true
    #bind mounts for hot reload
    volumes:
      - .:/usr/src/app
      - /usr/src/app/node_modules
    command: npm run dev
```

### start the compass

```bash
docker-compose up
```

### Stop everything (including volumes)

```bash
 docker-compose down --volumes
```
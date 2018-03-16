### Step 1
```
docker run -d redis:latest
```
### Step 2
```
docker inspect <friendly-name|container-id>
docker logs <friendly-name|container-id>
```
### Step 3
```
docker run -d --name redisHostPort -p 6379:6379 redis:latest
```
### Step 4
```
docker run -d --name redisDynamic -p 6379 redis:latest
docker port redisDynamic 6379
docker ps
```
### Step 5
```
docker run -d --name redisMapped -v "$PWD/data":/data redis  
docker inspect -f  '{{.Mounts}}' redisMapped 
``` 
### Step 6
```
$ docker run ubuntu ps
$ docker run -it ubuntu bash
```
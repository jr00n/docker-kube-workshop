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
```
### Step 5
```
mkdir $PWD/data  
docker run -d --name redisMapped -v "$PWD/data":/data redis  
docker inspect -f  '{{.Mounts}}' redisMapped 
``` 

###Step 1
```
docker network create backend-network
```
```
docker run -d --name=redis --net=backend-network redis
```
### Step 2
```
docker run --net=backend-network alpine cat /etc/resolv.conf
```
```
docker run --net=backend-network alpine ping -c1 redis
```
### Step 3
```
docker network create frontend-network
```
```
docker network connect frontend-network redis
```
```
docker run -d -p 3000:3000 --net=frontend-network katacoda/redis-node-docker-example
```
```
curl localhost:3000
```
### Step 4
```
docker network create frontend-network2
docker network connect --alias db frontend-network2 redis
```
```
docker run --net=frontend-network2 alpine ping -c1 db
```

### Step 5
```
docker network ls
```
```
docker network inspect frontend-network
```
```
docker network disconnect frontend-network redis
```

###extra-sources:
katacoda redis-node-docker: 
```https://github.com/katacoda/redis-node-docker```
####server.js
```
// Inspired by https://github.com/mranney/node_redis/blob/master/examples/web_server.js

var http = require("http");
var redis_client = require("redis").createClient(6379, 'redis');

var server = http.createServer(function (request, response) {
  response.writeHead(200, {
    "Content-Type": "text/plain"
  });

  var total_requests;

  redis_client.incr("requests", function (err, reply) {
    total_requests = reply; // stash response in outer scope
  });
  redis_client.hincrby("ip", request.connection.remoteAddress, 1);
  redis_client.hgetall("ip", function (err, reply) {
    // This is the last reply, so all of the previous replies must have completed already
    response.write("This page was generated after talking to redis.\n\n" +
                   "Application Build: 1" + "\n\n" + 
                   "Total requests: " + total_requests + "\n\n" +
                   "IP count: \n");
    Object.keys(reply).forEach(function (ip) {
      response.write("    " + ip + ": " + reply[ip] + "\n");
    });
    response.end();
  });
}).listen(3000);
console.log('Listening on port 3000');
```
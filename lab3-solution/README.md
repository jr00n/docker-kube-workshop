###Step 1
```
FROM node:7-alpine

RUN mkdir -p /src/app

WORKDIR /src/app
```
### Step 2
```
FROM node:7-alpine

RUN mkdir -p /src/app

WORKDIR /src/app

COPY package.json /src/app/package.json

RUN npm install
```
### Step 3
```
FROM node:7-alpine

RUN mkdir -p /src/app

WORKDIR /src/app

COPY package.json /src/app/package.json

RUN npm install

COPY . /src/app

EXPOSE 3000

CMD [ "npm", "start" ]
```
###Step 4
```
docker build -t my-nodejs-app .
docker run -d --name my-running-app -p 3000:3000 my-nodejs-app
curl http://localhost:3000
```
###Step 5
```
docker run -d --name my-production-running-app -e NODE_ENV=production -p 3000:3000 my-nodejs-app
```
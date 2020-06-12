## Vue Events Bulletin Board
[Tutorial link](https://docs.docker.com/get-started/)

This is the code for the Vue.js [tutorial on Scotch.io](https://scotch.io/tutorials/build-a-single-page-time-tracking-app-with-vue-js-introduction). In the tutorial we build a events bulletin board application and cover the basics of [Vue](http://vuejs.org/).

## Installation

1. Run `npm install`.
2. Run `node server.js`.
3. Visit [http://localhost:8080](http://localhost:8080).

## RESTful API (contributed by Jason Lam)

1. **Use Node.js & Express for backend server and router.**
2. **RESTful requests towards the server to simulate CRUD on *events* model, instead of local hardcoded ones.**
3. Translated into Traditional Chinese.

## RESTful API written in Go 

If you would like to use a backend written in Go, [thewhitetulip](http://github.com/thewhitetulip) has written on. See [the source code](https://github.com/thewhitetulip/go-vue-events).

---

## Modified by Julie Erlemeier 

## Dockerfile
Be literal and specific

```
FROM node:current-slim

WORKDIR /usr/src/app
COPY package.json .
RUN npm install

EXPOSE 8080
CMD [ "npm", "start" ]

COPY . .
```

## Node use in Dockerfile
- COPY, not ADD
- npm/yarn install, make sure you cleanup (RUN npm install && npm cache clean --force)
- CMD node, not npm
- WORKDIR, not RUN mkdir (unless you need chown)

## Ideal Dockerfile
```
FROM node:current-slim

EXPOSE 8080

WORKDIR /usr/src/app

COPY package.json .
COPY . .

RUN npm install && npm cache clean --force

CMD [ "node", "./bin/www" ]
```

## Docker CLI working with Docker only
1. Connect to Docker Daemon
2. `docker build --tag <NAMEOFIMAGE> .`
3. `docker run --publish 8000:8080 --detach --name bb bb:1.0`

## Docker CLI working with AWS
1. Connect to Docker Daemon
2. Get AUTH TOKEN: `aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 842337631775.dkr.ecr.us-west-2.amazonaws.com`
3. `docker build --tag <NAMEOFIMAGE> .`
4. `docker tag juliebb:latest 842337631775.dkr.ecr.us-west-2.amazonaws.com/juliebb:latest`
5. `docker push 842337631775.dkr.ecr.us-west-2.amazonaws.com/juliebb:latest`
 
## Test
1. `curl http://localhost:8000`
2. Go to browser and type http://localhost:8000 in address bar.

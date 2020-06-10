FROM node:current-slim

EXPOSE 8080

WORKDIR /usr/src/app

COPY package.json .
COPY . .

RUN npm install && npm cache clean --force

CMD [ "node", "./bin/www" ]
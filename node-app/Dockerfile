FROM node:9.9.0-alpine

# install express and git
RUN npm install express \
    && apk add --no-cache git

# clone git repo to /tmp/
RUN git clone https://github.com/kkenan/basic-microservices.git /tmp/basic-microservices

# switch working directory to new directory
WORKDIR /tmp/basic-microservices/node-app

EXPOSE 8081

CMD ["node", "index.js"]

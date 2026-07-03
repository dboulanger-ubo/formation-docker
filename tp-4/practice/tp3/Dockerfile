FROM node

WORKDIR /app

COPY package.json .
COPY server.js .

RUN apt update
RUN apt install iputils-ping -y

RUN npm install

ENTRYPOINT ["npm", "start"]
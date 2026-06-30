FROM node

WORKDIR /app

COPY package.json .
COPY server.js .

RUN npm install

ENTRYPOINT ["npm", "start"]
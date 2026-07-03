FROM node:22

WORKDIR /app

RUN mkdir backend
RUN mkdir client

COPY backend/ ./backend/
COPY client/ ./client/

# image du client

WORKDIR /app/client
RUN npm install
RUN npm run build

RUN cp -R dist/* /app/backend/src/static/

WORKDIR /app/backend
RUN npm install

ENTRYPOINT ["npm", "run", "dev"]
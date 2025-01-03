ARG NODE_VERSION=20.18.0
FROM node:${NODE_VERSION}

ENV PORT=3001
ENV MESSAGE="Hello Docker!"

WORKDIR /app

COPY . .

CMD [ "node", "index.js" ]
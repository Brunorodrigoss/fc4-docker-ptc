ARG NODE_VERSION=20.18.0
#FROM node:${NODE_VERSION}
#FROM node:${NODE_VERSION}-alpine
FROM node:${NODE_VERSION}-slim

ENV PORT=3001
ENV MESSAGE="Hello Docker!"

WORKDIR /app

RUN apt-get update && \
    apt-get install -y vim && \
    rm -rf /var/lib/apt/lists/*

COPY package*.json .

RUN npm install 

COPY . .

# RUN useradd -m mynode
# USER mynode

USER 1001

HEALTHCHECK --interval=10s --timeout=5s --start-period=5s --retries=3 \
    CMD [ "curl", "-f", "http://localhost:3001" ]

VOLUME [ "/data" ]

EXPOSE 3001

CMD [ "node", "index.js" ]
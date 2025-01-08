ARG NODE_VERSION=20.18.0
FROM node:${NODE_VERSION}

ENV PORT=3001
ENV MESSAGE="Hello Docker!"

WORKDIR /app

COPY package*.json .

RUN npm install 

COPY . .

# RUN useradd -m mynode
# USER mynode

USER 1001

HEALTHCHECK --interval=10s --timeout=5s --start-period=5s --retries=3 \
    CMD [ "curl", "-f", "http://localhost:3001" ]

CMD [ "node", "index.js" ]
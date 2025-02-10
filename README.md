# fc4-docker-ptc

| Commands |
|----------|
| docker ps -a -q |
| docker rm -f $(docker ps -a -q) |
||
|docker run -d --rm -p 8080:80 -v $(pwd)/my_nginx_html:/usr/share/nginx/html nginx|
|docker run -d -p 8080:80 --mount type=bind,source=$(pwd)/my_nginx_html,target=/usr/share/nginx/html nginx|
||
|docker volume create my_volume|
|docker inspect my_volume|
|docker volume ls|
|docker volume prune|
||
|docker run -d -p 8080:80 -v my_volume:/usr/share/nginx/html nginx|
|docker cp $(pwd)/my_nginx_html/index.html 644:/usr/share/nginx/html|
||
|docker run --rm -v my_volume:/data -v $(pwd)/backup_host:/backup busybox tar czf /backup/backup.tar.gz /data|
|docker run --rm -v my_volume:/data -v $(pwd)/backup_host:/backup busybox tar xzf /backup/backup.tar.gz -C /|
||
|docker rm containerID/containerName|
|docker rmi dockerImage|
|docker rmi $(docker images -q)|
||
|docker inspect dockerImage|
|docker inspect --format='{{.Id}}' nginx|
||
|docker search|
||
|docker image prune|
|docker image prune -a|
||
|docker images --filter before=nginx:1.22|
||
|docker system df|
||
|docker build -t brunorodrigoss/docker-node-example:latest .|
|docker run -p 3000:3000 brunorodrigoss/docker-node-example:latest|
||
|docker build --build-arg NODE_VERSION=21.0.0 -t brunorodrigoss/docker-node-example:latest .|
|docker run -it -p 3001:3001 brunorodrigoss/docker-node-example:latest|
|docker run -it -p 3001:3001 -e MESSAGE="HELLO" brunorodrigoss/docker-node-example:latest|
||
|docker run -it -u root -p 3001:3001 -e MESSAGE="HELLO" brunorodrigoss/docker-node-example:latest|
||
|docker build -t brunorodrigoss/docker-golang-example:latest .|
|docker run -it --rm -p 8080:8080 brunorodrigoss/docker-golang-example:latest|
||
|docker build -t brunorodrigoss/docker-golang-example:latest . --no-cache|
|docker run -it --rm -p 8080:8080 brunorodrigoss/docker-golang-example:latest ls -la|
||
|docker inspect brunorodrigoss/docker-golang-example:latest|
|docker ps --filter "label=env=production"|
||
|docker build -t brunorodrigoss/docker-node-base:latest -f Dockerfile.base .|
|docker build -t brunorodrigoss/docker-node-child:latest -f Dockerfile.child .|
|docker run --rm brunorodrigoss/docker-node-child:latest|
||
|docker buildx ls|
|docker context|
|docker context ls|
|docker buildx create --name mybuilder --driver docker-container --use|
|docker buildx use mybuilder|
|docker buildx use desktop-linux|
||
|docker exec -it buildx_buildkit_mybuilder0 sh|
|ps aux|
|docker buildx use mybuilder|
|docker buildx build --platform linux/amd64,linux/arm64 -t brunorodrigoss/docker-node-example:latest .|
|docker buildx build --platform linux/amd64,linux/arm64 -t brunorodrigoss/docker-node-example:latest --push .|
||
|docker buildx build --cache-to type=local,dest=../docker-cache --cache-from type=local,src=../docker-cache -t brunorodrigoss/docker-node-example:latest .|
||
|docker buildx prune|
|docker buildx prune --filter=until=24h|
|docker buildx rm mybuilder|
|docker context rm your-context-name|
||
|docker login|
|docker build -t brunorodrigoss/docker-golang-example:latest .|
|docker push brunorodrigoss/docker-golang-example:latest|
||
|docker network ls|
|docker network create my-network|
|docker run -d --rm --name web --network my-network nginx|
|docker run -d --rm --name db --network my-network mongo|
|docker exec -it web bash|
||
|docker build -t mynode_app_network .|
|docker run -it -d --rm --name appnode --network my-network mynode_app_network|
|docker logs appnode|
|docker logs -f appnode|
||
|docker network create backend-net|
|docker network create db-net|
|docker run -d --rm --name db --network db-net mongo|
|docker run -d --name app --network backend-net mynode_app_network|
|docker network connect db-net app|
|docker run -d --name app --network backend-net --network db-net mynode_app_network|
||
|docker run -d --rm --name nginx --network host nginx|
||
|docker network inspect bridge|
|docker run -it -d --rm --add-host=host.docker.internal:host-gateway --name nginx nginx|
|root@49ee7edcc423:/# curl host.docker.internal:3000|
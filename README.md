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












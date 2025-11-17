## Paso 1: Crear una red Docker
Primero, crear una red para que los contenedores se comuniquen:

docker network create mongo-network

## Paso 2: Crear los 3 contenedores MongoDB
Ejecutar estos comandos:

docker run -d \\
  --name mongo1 \\
  --network mongo-network \\
  -p 27019:27017 \\
  -e MONGO_INITDB_ROOT_USERNAME=admin \\
  -e MONGO_INITDB_ROOT_PASSWORD=password123 \\
  mongo:latest

docker run -d \\
  --name mongo2 \\
  --network mongo-network \\
  -p 27020:27017 \\
  -e MONGO_INITDB_ROOT_USERNAME=admin \\
  -e MONGO_INITDB_ROOT_PASSWORD=password123 \\
  mongo:latest

docker run -d \\
  --name mongo3 \\
  --network mongo-network \\
  -p 27021:27017 \\
  -e MONGO_INITDB_ROOT_USERNAME=admin \\
  -e MONGO_INITDB_ROOT_PASSWORD=password123 \\
  mongo:latest

  ## Paso 3: Crear el archivo de configuración de NGINX
  Crear una carpeta para docker mongo

  Dentro de la carpeta añadir el archivo de configuración nginx.conf

 ## Paso 4: Crear el contenedor NGINX
 docker run -d \\
  --name nginx-balancer \\
  --network mongo-network \\
  -p 8080:27017 \\
  -v /mnt/c/docker-mongo/nginx.conf:/etc/nginx/nginx.conf:ro \\
  nginx:latest

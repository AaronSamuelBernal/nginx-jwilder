# Rproxy

## Como integrar a tu docker
### 1. Genere un archivo .env o edite en caso de ya tenerlo (debe corresponderse con el docker-compose de tu aplicación)
### 2. Escriba lo siguiente en el mismo
```
VIRTUAL_HOST=<URL DE TU APP>
VIRTUAL_PORT=<PUERTO DEL DOCKER>
LET_ENC_HOST=<URL DE TU APP>
LET_ENC_EMAIL=infra@puelotech.com
```
### 3. edite el archivo docker-compose.yml, debe quedar de la siguiente manera
```
    ports:
      - "${VIRTUAL_PORT}>:80"
      - "<CUALQUIER PUERTO LIBRE>:443"
    environment:
      VIRTUAL_HOST: ${VIRTUAL_HOST}
      VIRTUAL_PORT: ${VIRTUAL_PORT}
      LETSENCRYPT_HOST: ${LET_ENC_HOST}
      LETSENCRYPT_EMAIL: ${LET_ENC_EMAIL}
```
#### También puede escribir el entorno como
```
    environment:
      - VIRTUAL_HOST= ${VIRTUAL_HOST}
      - VIRTUAL_PORT= ${VIRTUAL_PORT}
      - LETSENCRYPT_HOST:= ${LET_ENC_HOST}
      - LETSENCRYPT_EMAIL= ${LET_ENC_EMAIL}
```
#### añada también al docker de la aplicación la red de nginx

```
networks:
  docker-app:
  nginx-proxy:
     external:
         name: nginx-proxy

```


Start proxy
```
$ docker-compose up -d reverse-proxy
```

Requires add network:
```
$ docker network create traefik_proxy
```

In containers `docker-compose.yml` add:
```
version: '3'
services:
  xxx:
    networks:
      - traefik_proxy
      - default
    labels:
      - traefik.frontend.rule=Host:jakas-domena.test
      - traefik.docker.network=traefik_proxy

networks:
  traefik_proxy:
    external:
      name: traefik_proxy
  default:
    driver: bridge

```

Also need add in `hosts` file
```
127.0.0.1       jakas-domena.test www.jakas-domena.test
```

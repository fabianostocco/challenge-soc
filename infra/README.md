Esse documento apresenta instruções passo a passo sobre como implantar a stack abaixo utilizando containers em Docker através do orquestrador Docker Compose para ambientes de desenvolvimento e testes.

- Abaixo estão as versões de cada software utilizado nesse projeto:
  - Fedora v32
  - Docker v19.03.8
  - Docker Compose v1.25.5

### Índice

<!--ts-->

- [Implantação Stack](#implantação-stack)
- [Deletar a Stack](#deletar-a-stack)
- [Recriação da Stack](#recriação-da-stack)
- [Não utilização de Docker Secrets](#não-utilização-de-docker-secrets)
<!--te-->

---

## Implantação Stack

As variáveis utilizadas no docker-compose.yml podem ser definidas como um arquivo .env dentro do diretório **compose**

Para prosseguir nesta etapa é necessário executar o seguinte comando no diretório **compose** onde contém o arquivo [Makefile](Makefile):

```
[username@hostname ~]$ make all
```

Será implantado a stack, sendo composta por um frontend, wordpress e banco de dados MySQL.


### Containers

```
[username@hostname ~]$ docker ps -a
CONTAINER ID        IMAGE                COMMAND                  CREATED             STATUS              PORTS                   NAMES
32639b2ff903        nginx:1.15.12-alpine "docker-entrypoint.s…"   4 minutes ago       Up 4 minutes        0.0.0.0:80->8080/tcp    frontend
32639b2ff903        wordpress            "docker-entrypoint.s…"   4 minutes ago       Up 4 minutes        0.0.0.0:9000->9000/tcp  wordpress
12ae8cf2642e        mysql:57             "docker-entrypoint.s…"   4 minutes ago       Up 4 minutes        0.0.0.0:3306->3306/tcp  db
```

## Deletar a Stack

Para prosseguir nesta etapa é necessário executar o seguinte comando no diretório **compose** onde contém o arquivo [Makefile](Makefile):

```
[username@hostname ~]$ make delete
```

## Recriação da Stack

Para prosseguir nesta etapa é necessário executar o seguinte comando no diretório **compose** onde contém o arquivo [Makefile](Makefile):

```
[username@hostname ~]$  make recreate
```

---

## Não utilização de Docker Secrets

- **Nesse projeto não foi utilizado Docker Secrets, pois não visto necessidade de subir o Swarm (requisito para utilizar Secrets no Docker) para ambiente de testes**

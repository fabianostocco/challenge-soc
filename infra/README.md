Esse documento apresenta instruções passo a passo sobre como implantar a stack abaixo utilizando containers em Docker através do orquestrador Docker Compose para ambientes de desenvolvimento e testes.

- Abaixo estão as versões de cada software utilizado nesse projeto:
  - Fedora v32
  - Docker v19.03.8
  - Docker Compose v1.25.5

### Índice

<!--ts-->

- [Implantação Stack](#implantação-stack)
- [Alterações realizadas](#alterações-realizadas)
<!--te-->

---

## Implantação Stack

As variáveis utilizadas no docker-compose.yml podem ser definidas como um arquivo .env dentro do diretório **compose**

Para prosseguir nesta etapa é necessário executar o seguinte comando no diretório **compose** onde contém o arquivo [Makefile](Makefile):

```
[username@hostname ~]$ make all
```

Isso irá implantar a stack, sendo composta por um frontend, backend e banco de dados MySQL.

Esse comando irá criar os seguintes recursos:

- 3 containers, sendo dois em Node.JS e um banco de dados MySQL.
- Somente o primeiro container terá acesso externo (rede local do host), sendo os outros containers acessíveis somente na VLAN criada pelo Docker.
- Foi colocado um script de **wait-for-it**, que o backend espera o socket do banco de dados subir para criar o seu socket (ou seja, subir a aplicação), assim como no frontend que espera o backend "subir" para criar o seu socket.

### Containers

```
[username@hostname ~]$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
32639b2ff903        wordpress           "docker-entrypoint.s…"   4 minutes ago       Up 4 minutes        0.0.0.0:80->8080/tcp   wordpress
12ae8cf2642e        postgres:12         "docker-entrypoint.s…"   4 minutes ago       Up 4 minutes        5432/tcp, 5432/tcp     db
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

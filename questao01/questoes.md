# Kubedev - Desafio de Docker

## Questão 01
Execute os comandos para criar os 4 bancos de dados listados com containers, e use
como se tivesse instalado eles localmente na sua máquina (Não esquece de garantir
que não vai perder os dados caso o container seja excluido).

- MongoDB
- MariaDB
- PostgreSQL
- Redis

## Respostas - Questão 01

### MongoDB

Vamos criar o volume para não perder os dados em caso do container ser excluido.

```bash
docker volume create mongodb_vol
```

O comando para criação do container.

```bash
docker container run -d \
	--name mongodb \
	-p 27017:27017 \
	-v mongodb_vol:/data/db \
	-e MONGO_INITDB_ROOT_USERNAME="mongouser" \
	-e MONGO_INITDB_ROOT_PASSWORD="mongopwd" \
	mongo:4.4.3
```

### MariaDB

Criar o volume para não perder os dados em caso do container ser excluido.

```bash
docker volume create mariadb_vol
```

Comando para criação do container.

```bash
docker container run -d \
	--name mariadb \
	-p 3306:3306 \
	-v mariadb_vol:/var/lib/mysql \
	-e MARIADB_USER="mariadbuser" \
	-e MARIADB_PASSWORD="mariadbpwd" \
	-e MARIADB_ROOT_PASSWORD="mariadbpwdroot" \
	mariadb:10.7.1
```

### PostrgreSQL

Criar o volume para não perder os dados em caso do container ser excluido.

```bash
docker volume create postgres_vol
```

Comando para criação do container.

```bash
docker container run -d \
	--name postgres \
	-p 5432:5432 \
	-v postgres_vol:/var/lib/postgresql/data \
	-e POSTGRES_USER="postgresuser" \
	-e POSTGRES_PASSWORD="postgrespwd" \
	postgres:9.6.24
```

### Redis

Criar o volume para não perder os dados em caso do container ser excluido.

```bash
docker volume create redis_vol
```

Comando para criação do container.

```bash
docker container run -d \
	--name redis \
	-p 6379:6379 \
	-v redis_vol:/data \
	redis:6.2.6
```

>Este Desafio de Docker faz parte do Curso [KubeDev.io](https://kubedev.io/).
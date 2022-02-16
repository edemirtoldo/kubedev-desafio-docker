## Kubedev - Desafio de Docker

## Questão 01
Execute os comandos para criar os 4 bancos de dados listados com containers, e use
como se tivesse instalado eles localmente na sua máquina (Não esquece de garantir
que não vai perder os dados caso o container seja excluido).

- MongoDB
- MariaDB
- PostgreSQL
- Redis

### MongoDB

Vamos criar o volume para não perder os dados em caso do container ser excluido.

```bash
docker volume create mongodb_vol
```

O comando para criação do container.

```bash
docker container run -d \
	-e MONGO_INITDB_ROOT_USERNAME=mongouser \
	-e MONGO_INITDB_ROOT_PASSWORD=mongopwd \
	-v mongodb_vol:/data/db \
	-p 27017:27017 \
	--name mongodb \
	mongo:4.4.3
```

### MariaDB

Vamos criar o volume para não perder os dados em caso do container ser excluido.

```bash
docker volume create mariadb_vol
```

O comando para criação do container.

```bash
docker container run -d \
	--name mariadb \
	--network mariadb_net \
	-p 3306:3306 \
	-v mariadb_vol:/var/lib/mysql \
	-e MARIADB_USER="mariadbuser" \
	-e MARIADB_PASSWORD="mariadbpwd" \
	-e MARIADB_ROOT_PASSWORD="mariadbpwdroot" \
	mariadb:10.7.1
```

### PostrgreSQL

Vamos criar o volume para não perder os dados em caso do container ser excluido.

```bash
docker volume create postgres_vol
```

O comando para criação do container.

```bash
docker container run -d \
	--name postgres \
	--network postgres_net \
	-p 5432:5432 \
	-v postgres_vol:/var/lib/postgresql/data \
	-e POSTGRES_USER="postgresuser" \
	-e POSTGRES_PASSWORD="postgrespwd" \
	postgres:9.6.24
```

### Redis

Vamos criar o volume para não perder os dados em caso do container ser excluido.

```bash
docker volume create redis_vol
```

O comando para criação do container.

```bash
docker container run -d \
	--name redis \
	--network redis_net \
	-p 6379:6379 \
	-v redis_vol:/data \
	redis:6.2.6
```
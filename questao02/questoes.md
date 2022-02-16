## Kubedev - Desafio de Docker

## Questão 02
Certo, você conseguiu criar 4 bancos na sua máquina utilizando containers. Mas tem uma coisa, não adianta só conectar a aplicação no banco quando se está desenvolvendo, é preciso também acessar o banco, executar comandos e consultar a base. Então vamos fazer isso da forma KubeDev de ser, com containers !!! Cada banco
de dados tem uma ferramenta administrativa com interface web que você pode usar.

- MongoDB ⇒ Mongo Express - <https://github.com/mongo-express/mongo-express>

- MariaDB ⇒ phpmyadmin - <https://www.phpmyadmin.net/>




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
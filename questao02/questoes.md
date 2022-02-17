## Kubedev - Desafio de Docker

## Questão 02
Certo, você conseguiu criar 4 bancos na sua máquina utilizando containers. Mas tem uma coisa, não adianta só conectar a aplicação no banco quando se está desenvolvendo, é preciso também acessar o banco, executar comandos e consultar a base. Então vamos fazer isso da forma KubeDev de ser, com containers !!! Cada banco
de dados tem uma ferramenta administrativa com interface web que você pode usar.

MongoDB ⇒ Mongo Express <https://github.com/mongo-express/mongo-express>

MariaDB ⇒ phpmyadmin <https://www.phpmyadmin.net/>

PostgreSQL ⇒  Pgadmin <https://www.pgadmin.org/>

Redis ⇒ Redis-commander <https://hub.docker.com/r/rediscommander/redis-commander>

### MongoDB => Mongo Express

Criar o volume para não perder os dados em caso do container ser excluido.

```bash
docker volume create mongodb_vol
```

Criar a network para acesso da ferramenta administrativa especifica.

```bash
docker network create mongodb_net
```

Executar o container do MongoDB.

```bash
docker container run -d \
    --name mongodb \
    --network mongodb_net \
    -p 27017:27017 \
    -v mongodb_vol:/data/db \
    -e MONGO_INITDB_ROOT_USERNAME="mongouser" \
    -e MONGO_INITDB_ROOT_PASSWORD="mongopwd" \
    mongo:4.4.3
```

Executar o container do Mongo Express.

```bash
docker container run -d \
    --name mongo-express \
    --network mongodb_net \
    -p 8081:8081 \
    -e ME_CONFIG_OPTIONS_EDITORTHEME="ambiance" \
    -e ME_CONFIG_BASICAUTH_USERNAME="" \
    -e ME_CONFIG_MONGODB_URL="mongodb://mongouser:mongopwd@mongodb:27017/admin
" \
    mongo-express
```
Link para acesso ao Mongo Express <http://localhost:8081/>

Pagina do Mongo-Express

![Mongo-Express](https://github.com/edemirtoldo/kubedev-desafio-docker/blob/main/img/mongo-express.png)

### MariaDB => phpmyadmin

Criar o volume para não perder os dados em caso do container ser excluido.

```bash
docker volume create mariadb_vol
```

Criar a network para acesso da ferramenta administrativa especifica.

```bash
docker network create mariadb_net
```

Executar o container do MariaDB.

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

Executar o container do phpmyadmin.

```bash
docker container run -d \
	--name phpmyadmin \
	--network mariadb_net \
	-p 8082:80 \
	-v mariadb_vol:/var/lib/mysql \
	-e PMA_ARBITRARY="1" \
	phpmyadmin:5.1.3
```
Link para acesso ao phpmyadmin <http://localhost:8082/>

Credenciais de login
- Servidor: mariadb
- Usuário: root
- Senha: mariadbpwdroot

Pagina do phpmyadmin login

![phpmyadmin1](https://github.com/edemirtoldo/kubedev-desafio-docker/blob/main/img/phpmyadmin1.png)

Pagina do phpmyadmin

![phpmyadmin2](https://github.com/edemirtoldo/kubedev-desafio-docker/blob/main/img/phpmyadmin2.png)


### PostrgreSQL => Pgadmin 

Criar o volume para não perder os dados em caso do container ser excluido.

```bash
docker volume create postgres_vol
```

Criar a network para acesso da ferramenta administrativa especifica.

```bash
docker network create postgres_net
```

Executar o container do MariaDB.

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

Executar o container do PgAdmin.

```bash
docker container run -d \
	--name pgadmin4 \
	--network postgres_net \
	-p 8083:80 \
	-v pgadmin-data:/var/lib/pgadmin \
	-e PGADMIN_DEFAULT_EMAIL="postgresuser@postgresuser.com" \
	-e PGADMIN_DEFAULT_PASSWORD="postgrespwd" \
	-e PGADMIN_LISTEN_PORT="80" \
	dpage/pgadmin4:5.5
```
Link para acesso ao PgAdmin <http://localhost:8083/>

Credenciais de login
- Username: postgresuser@postgresuser.com
- Passwork: postgrespwd

Pagina do PgAdmin login

![pgadmin1](https://github.com/edemirtoldo/kubedev-desafio-docker/blob/main/img/pgadmin1.png)

Clique em Add New Server

Na aba General informe
- Name: postgres

![pgadmin2](https://github.com/edemirtoldo/kubedev-desafio-docker/blob/main/img/pgadmin2.png)

Na aba Connection informe
- Host name/address: postgres
- Port: 5432
- Maintenance database: postgres
- Username: postgresuser
- Password: postgrespwd 
- e clique no botão Save

![pgadmin3](https://github.com/edemirtoldo/kubedev-desafio-docker/blob/main/img/pgadmin3.png)

Pagina do PgAdmin

![pgadmin5](https://github.com/edemirtoldo/kubedev-desafio-docker/blob/main/img/pgadmin5.png)

### Redis => Redis-commander 

Criar o volume para não perder os dados em caso do container ser excluido.

```bash
docker volume create redis_vol
```

Criar a network para acesso da ferramenta administrativa especifica.

```bash
docker network create redis_net
```

Executar o container do Redis.

```bash
docker container run -d \
	--name redis \
	--network redis_net \
	-p 6379:6379 \
	-v redis_vol:/data \
	redis:6.2.6
```

Executar o container do Redis-Commander.

```bash
docker container run -d \
	--name redis-commander \
	--network redis_net \
	-p 8084:8081 \
	-e REDIS_HOSTS=local:redis:6379 \
	rediscommander/redis-commander:latest
```
Link para acesso ao PgAdmin <http://localhost:8084/>

Credenciais de login
- Username: postgresuser@postgresuser.com
- Passwork: postgrespwd

Pagina do PgAdmin login

![pgadmin1](https://github.com/edemirtoldo/kubedev-desafio-docker/blob/main/img/pgadmin1.png)


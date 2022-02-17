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

Executar o container do Maria.

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
Link para acesso ao phpmyadmin <http://localhost:8081/>

Pagina do phpmyadmin

![Mongo-Express](https://github.com/edemirtoldo/kubedev-desafio-docker/blob/main/img/mongo-express.png)



### PostrgreSQL => Pgadmin 



### Redis => Redis-commander 


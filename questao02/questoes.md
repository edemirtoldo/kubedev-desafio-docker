## Kubedev - Desafio de Docker

## Questão 02
Certo, você conseguiu criar 4 bancos na sua máquina utilizando containers. Mas tem uma coisa, não adianta só conectar a aplicação no banco quando se está desenvolvendo, é preciso também acessar o banco, executar comandos e consultar a base. Então vamos fazer isso da forma KubeDev de ser, com containers !!! Cada banco
de dados tem uma ferramenta administrativa com interface web que você pode usar.

MongoDB ⇒ Mongo Express <https://github.com/mongo-express/mongo-express>

MariaDB ⇒ phpmyadmin <https://www.phpmyadmin.net/>

PostgreSQL ⇒  Pgadmin <https://www.pgadmin.org/>

Redis ⇒ Redis-commander <https://hub.docker.com/r/rediscommander/redis-commander>

### MongoDB - Mongo Express

Vamos criar o volume para não perder os dados em caso do container ser excluido.

```bash
docker volume create mongodb_vol
```



O comando para criação do container.

```bash

```

### MariaDB - phpmyadmin

Vamos criar o volume para não perder os dados em caso do container ser excluido.

```bash

```

O comando para criação do container.

```bash

```

### PostrgreSQL

Vamos criar o volume para não perder os dados em caso do container ser excluido.

```bash

```

O comando para criação do container.

```bash

```

### Redis

Vamos criar o volume para não perder os dados em caso do container ser excluido.

```bash

```

O comando para criação do container.

```bash

```
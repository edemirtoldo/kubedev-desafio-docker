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

Vamos criar o volume para o MongoDB.

```bash
docker volume create mongodb_vol
```

O comando para criação do container do MongoDB.

```bash
docker container run -d -e MONGO_INITDB_ROOT_USERNAME=mongouser -e MONGO_INITDB_ROOT_PASSWORD=mongopwd -v mongodb_vol:/data/db -p 27017:27017 --name mongodb mongo:4.4.3
```

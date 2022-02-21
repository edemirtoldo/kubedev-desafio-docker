# Kubedev - Desafio de Docker

## Questão 04

Agora que você já afiou o seu conhecimento sobre criação de imagens Docker, tá na hora de fazer o deploy de uma aplicação 100% em containers Docker. A aplicação está no GitHub do KubeDev e um detalhe MUITO importante, a aplicação precisa ser toda criada com apenas uma linha de comando.

- link da aplicação: <https://github.com/KubeDev/rotten-potatoes>

## Docker Compose da aplicação rotten-potatoes.

docker-compose.yaml

```bash
vversion: "3.8"

networks:
  rotten-potatoes_net:
    driver: bridge

volumes:
  rotten-potatoes_vol:

services:
  app:
    image: edemirtoldo/rotten-potatoes:${TAG}
    build:
      dockerfile: ./Dockerfile
      context: ./src
    ports:
      - 5000:5000
    depends_on:
      - db
    networks:
      - rotten-potatoes_net
    environment:
      MONGODB_DB: admin
      MONGODB_HOST: db
      MONGODB_PORT: 27017
      MONGODB_USERNAME: mongouser
      MONGODB_PASSWORD: mongopwd

  db:
    image: mongo:4.4.3
    restart: always
    networks:
      - rotten-potatoes_net
    ports:
      - 27017:27017
    environment:
      MONGO_INITDB_ROOT_USERNAME: mongouser
      MONGO_INITDB_ROOT_PASSWORD: mongopwd
    volumes:
      - rotten-potatoes_vol:/data/db
```

Criando a aplicação com a linha de comando abaixo:

```bash
docker-compose up -d
```

Respositório com aplicação rotten-potatoes: <https://github.com/edemirtoldo/rotten-potatoes>

>Este Desafio de Docker faz parte do Curso [KubeDev.io](https://kubedev.io/).
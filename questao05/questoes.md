# Kubedev - Desafio de Docker

## Questão 05

Chegou um cliente pra você que possui todas as suas aplicações em data centers e a gestão dessas aplicações está cada vez mais complexa então pra iniciar um plano de gestão unificada e migração pra um ambiente cloud, as aplicações serão migradas pra containers. E hoje você precisa iniciar esse processo com um projeto piloto, o portal de conteúdos da empresa construido em Wordpress. Então hoje sua missão é criar esse ambiente wordpress pronto para a equipe de publicidade começar a popular.

docker-compose.yaml

```bash
version: '3.1'

volumes:
  wp_vol:
  db_vol:

networks:
  wp_net:
    driver: bridge

services:

  wordpress:
    image: wordpress
    restart: always
    ports:
      - 8080:80
    networks:
      - wp_net
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppwd
      WORDPRESS_DB_NAME: wpdb
    volumes:
      - wp_vol:/var/www/html
    depends_on:
      - db

  db:
    image: mysql:5.7
    restart: always
    networks:
      - wp_net
    environment:
      MYSQL_DATABASE: wpdb
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppwd
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - db_vol:/var/lib/mysql
```

>Este Desafio de Docker faz parte do Curso [KubeDev.io](https://kubedev.io/).
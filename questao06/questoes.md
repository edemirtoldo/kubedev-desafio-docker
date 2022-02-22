# Kubedev - Desafio de Docker


## Questão 06

Agora vamos aumentar mais a complexidade das coisas, chegou a hora de executar
uma aplicação baseada em arquitetura de microsserviços.
Essa aplicação é formada por 3 repositórios:

- Microsserviço de Filmes (https://github.com/KubeDev/rotten-potatoes-ms)
- Microsserviço de Avaliação (https://github.com/KubeDev/movie)
- Montar o ambiente com Docker compose baseado em arquivos de enviroment (https://github.com/KubeDev/review)



## Resposta - Questão 06
## Rotten Potatoes com Microserviços

Aplicação escrita em python com filmes com a opção de cadastrar resenhas de cada filme.

## Estrutura do projeto

Esse projeto é baseado em uma aquitetura de Microsserviços e depende de outros 2 projetos pra funcionar.

Que são:

[Microserviço Reviews](https://github.com/edemirtoldo/review/) - onde são armazenados os dados de resenha dos filmes apresentados pela aplicação que utiliza PostGresSQL como banco de dados.

[Microserviço Movies](https://github.com/edemirtoldo/movie) - onde estão cadastrados os filmes exibidos no site da aplicação que utiliza MongoDB como banco de dados.

Segue abaixo o diagrama:

![diagrama](https://github.com/edemirtoldo/rotten-potatoes-ms/blob/main/img/diagrama.png)

## Configuração

Foram criados 3 Dockerfile para criação da imagens docker.

Dockerfile - Rotten-Potatoes-MS - local: ./rotten-potatoes-ms/src/

```bash
FROM python:3.8-slim-buster
WORKDIR /app
COPY requirements.txt /app
RUN python -m pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["gunicorn", "--workers=3", "--bind", "0.0.0.0:5000", "app:app"]
```

Dockerfile - Movies - local: ./movie/src/

```bash
FROM node:16-alpine
EXPOSE 8181
WORKDIR /app
COPY package*.json /app/
RUN npm install
COPY . .
ENTRYPOINT [ "node", "server.js" ]
```

Dockerfile - Review - local: ./review/src/Review.Web

```bash
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY Review.Web.csproj /src/.
RUN dotnet restore Review.Web.csproj
COPY . .
RUN dotnet build Review.Web.csproj -c Release -o /app/build

FROM build AS publish
RUN dotnet publish Review.Web.csproj -c Release -o /app/publish

FROM base AS Final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT [ "dotnet", "Review.Web.dll" ]
```



Link para acesso a aplicação de Filmes (http://localhost:8080)



```bash

```



>Este Desafio de Docker faz parte do Curso [KubeDev.io](https://kubedev.io/).
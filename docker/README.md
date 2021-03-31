# Unidade Docker atividades

##### Projeto-gerenciador-tarefas, Projeto simples gerenciador de tarefas.

> ATIVIDADE 1º Criar imagen utilizando DockerFile subindo minha aplicação projeto-gerenciador-tarefas, utilzando ngnix.
> 
> * Criando a imagem, docker build -t lpradopires/nginx-tarefas:v1 .
> * Rodando a imagem, docker run -d -p 8089:80  lpradopires/nginx-tarefas:v1
> * Acessando o container, docker container exec -it 6cc68f3ae1d5 /bin/bash

> ATIVIDADE 2º Criar imagem com base na imagem node, carregando o projeto lista para poder ser alterado.
>              Ao subir a imagem já o projeto deve ser startado. Como o projeto esta utilizando angular cli, ele deve ser instalado na imagem.
> 
> * criando a imagem, docker build -t lpradopires/projetoangular:v1 .
> * rodando a imagem, docker docker run -it  --name app -p 8089:4200 --mount type=bind,source="$(pwd)"/lista,target=/usr/projetos lpradopires/projetoangular:v1 /bin/bash


> ATIVIDADE 3º Nesta atividade existe um projeto em node, que realiza um crud simples em um arquivo JSON, esse arquivo está na pasta data/items.json. Cria uma imagem docker que rode esse projeto, suba 3 containers e crie um volume único para compartilhar o arquivo de persistência. Postman para teste. 
> 
> * crie a imagem Dockerfile ativ3, docker build -t lppires/crud:v1 .
> * crie um volume chamado dbjson, docker volume create dbjson.
> * Local volume, \\wsl$\docker-desktop-data\version-pack-data\community\docker\volumes\db_json\_data
> * rodar os 3 containers, estão corpartilhando o arquivo do volume
> 1. docker run --name crudjson -d -p 8089:3000 --mount type=volume,source=dbjson,target=/usr/projetos/data lppires/crud:v1
> 2. docker run --name crudjson1 -d -p 8090:3000 --mount type=volume,source=dbjson,target=/usr/projetos/data lppires/crud:v1
> 3. docker run --name crudjson2 -d -p 8091:3000 --mount type=volume,source=dbjson,target=/usr/projetos/data lppires/crud:v1





## Links Interessantes de pesquisa

[Guia rápido comandos Docker](https://github.com/lpradopires/curso-fullcycle/blob/main/documentos/docker_cheatsheet_r3v2.pdf)

[Livro Docker introdução - Wesley Willians](https://github.com/lpradopires/curso-fullcycle/blob/main/documentos/docker-e-docker-compose-na-pratica.pdf)

[Difrença Bind Mounts e Volume](https://4sysops.com/archives/introduction-to-docker-bind-mounts-and-volumes/#:~:text=The%20main%20difference%20a%20bind,volumes%2C%20similar%20to%20bind%20mounts.)

[Diferença Bind Mouns e Volume (2)](https://escoladaprogramacao.com.br/diferencas-entre-volume-e-bind-mount-no-docker/)

## Anotações

**Comando criar uma imagem**

   * docker build -t usuario/nomeimagem:tag raizDockerFile

**Acessando container em execução, abre o bash do container**

   * docker container exec -it idContainner /bin/bash

**Remover todos containers, inativos e ativos.**
  
   * docker rm $(docker ps -a -q) -f
   
**Podemos quando necessario limpar os volumes não utilizados**
  
   * docker volume prune
   
**Trabalhando com volume** 

* docker volume ls
* docker volume create nome_volume
* docker volume inspect nome_volume


### Desafio

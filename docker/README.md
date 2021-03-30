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


## Links Interessantes de pesquisa

[Guia rápido comandos Docker](https://github.com/lpradopires/curso-fullcycle/blob/main/documentos/docker_cheatsheet_r3v2.pdf)

[Livro Docker introdução - Wesley Willians](https://github.com/lpradopires/curso-fullcycle/blob/main/documentos/docker-e-docker-compose-na-pratica.pdf)

## Anotações

##### Comando criar uma imagem

   * docker build -t usuario/nomeimagem:tag raizDockerFile

##### Acessando container em execução, abre o bash do container

   * docker container exec -it idContainner /bin/bash

##### Remover todos containers, inativos e ativos.
  
   * docker rm $(docker ps -a -q) -f

### Desafio

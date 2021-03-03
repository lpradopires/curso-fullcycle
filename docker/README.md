# Unidade Docker atividades 

projeto-gerenciador-tarefas, projeto simples gerenciador de tarefas. 

ATIVIDADE 1º Criar imagen utilizando DockerFile subindo minha aplicação projeto-gerenciador-tarefas, utilzando ngnix.

    Criando a imagem, docker build -t lpradopires/nginx-tarefas:v1 .
    Rodando a imagem, docker run -d -p 8089:80  lpradopires/nginx-tarefas:v1
    Acessando o container, docker container exec -it 6cc68f3ae1d5 /bin/bash

ATIVIDADE 2º Criar imagem com base na imagem node e realizar as seguintes configuações no dockerfile

        - Instalar Angular CLI
        - Criar um pasta no container usuario/projetos/lista         
        - Mapear a pasta atividade2/projeto/lista para a pasta usuario/projetos/lista
        - Criar um novo projeto Angular na pasta lista
        - Subir projeto, o projeto deve ser acessado na porta 8030 na maquina local.
        - Abrir o projeto no vscode e alterar o arquivo, deve atualizar o projeto no container

        --mount type=bind,source="$(pwd)"/lista,target=/usr/projetos/lista/projeto-lista

### Links Interessantes de pesquisa


### Documentos 

[Guia rápido comandos Docker ](https://github.com/lpradopires/cursofullcycle/blob/main/documentos/docker_cheatsheet_r3v2.pdf)

[Livro Docker introdução - Wesley Willians ](https://github.com/lpradopires/cursofullcycle/blob/main/documentos/docker-e-docker-compose-na-pratica.pdf)

### Artigos


### Anotações 

Comando criar uma imagem 
    -docker build -t usuario/nomeimagem:tag raizDockerFile

Acessando container em execução, abre o bash do container
    -docker container exec -it idContainner /bin/bash 

Remover todos containers, inativos e ativos.
    - docker rm $(docker ps -a -q) -f

### Desafio
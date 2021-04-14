# Unidade Docker

**Configuração Ambiente**

[Instalação WSL2 - Docker](https://github.com/codeedu/wsl2-docker-quickstart)

##### Exemplo .wslconfig
[wsl2]  
memory=8GB  
processors=2  
swap=0  
localhostForwarding=true  


## Links Interessantes de pesquisa

[Guia rápido comandos Docker](https://github.com/lpradopires/curso-fullcycle/blob/main/documentos/docker_cheatsheet_r3v2.pdf)

[Livro Docker introdução - Wesley Willians](https://github.com/lpradopires/curso-fullcycle/blob/main/documentos/docker-e-docker-compose-na-pratica.pdf)

[Comandos Docker](https://medium.com/xp-inc/principais-comandos-docker-f9b02e6944cd)

[Difrença Bind Mounts e Volume](https://4sysops.com/archives/introduction-to-docker-bind-mounts-and-volumes/#:~:text=The%20main%20difference%20a%20bind,volumes%2C%20similar%20to%20bind%20mounts.)

[Diferença Bind Mouns e Volume (2)](https://escoladaprogramacao.com.br/diferencas-entre-volume-e-bind-mount-no-docker/)

[Diferença Entrypoint vs CMD](https://phoenixnap.com/kb/docker-cmd-vs-entrypoint#:~:text=CMD%20is%20an%20instruction%20that,container%20with%20a%20specific%20executable.)

## Anotações

#### Opções mais utilizadas para o comando `docker run`
 - `-i` permite interagir com o container
 - `-t` associa o seu terminal ao terminal do container
 - `-it` é apenas uma forma reduzida de escrever `-i -t`
 - `--name algum-nome` permite atribuir um nome ao container em execução
 - `-p 8080:80` mapeia a porta 80 do container para a porta 8080 do host
 - `-d` executa o container em background
 - `-v /pasta/host:/pasta/container` cria um volume '/pasta/container' dentro do container com o conteudo da pasta '/pasta/host' do host
 
 ### docker run [options] [image] [command] [args]
**Coloca um container em execução, por exemplo:**
```
docker run -it ubuntu bash
```
```
root@13d2fb2f08e1:/#
```
se tudo der certo deve ser visualizado um terminal, de dentro do container em execução

**Acessando container em execução, abre o bash do container**
```
docker container exec -it idContainner /bin/bash
```
**Remover todos containers, inativos e ativos.**
```
docker rm $(docker ps -a -q) -f
```

**Comando criar uma imagem**
```
docker build -t usuario/nomeimagem:tag raizDockerFile
```

## Trabalhando com volume 
**Lista volumes**
```
docker volume ls
```
**Criando volume**
```
docker volume create nome_volume
```
**Especionando Volume**
```
docker volume inspect nome_volume
```

**Podemos quando necessario limpar os volumes não utilizados**
```
docker volume prune
```

## Trabalhando com imagens
**Lista Imagens**
```
docker images
```
**Baixando uma imagen** 
````
docker pull nome_imagen
docker pull ubuntu
docker pull php:rc-alpine
````
**Removendo Imagen**
```
docker rmi nome_imagen
docker rmi ubuntu
docker rmi php:rc-alpine
```

**Criando uma imagen com Dockerfile**
````
//Exemplo Simples Dockerfile
FROM nginx:latest
RUN apt-get update
RUN apt-get install vim -y
````
````
docker build -t nome_usuario_dockerHub/nome_imagem:versão local_dockerfile
docker build -t lppires/nginx-com-vim:latest .
````
**Publicando imagen no DockerHub**
````
docker login
docker push lppires/nginx-com-vim:latest
````

## Trabalhando com Networks
Tipos Networks
* **bridge** (Rede padrão, rede criada pelo docker)
* **host** (Mescla a rede docker com rede da maquina host)
* **overlay** (comunicação entre maquinas docker)
* **maclan**(?)
* **none**(não faz parte de nenhuma rede)

**Lista Comandos NetWork**
````
docker network COMMAND
````
**Lista Nteworks**
````
docker network ls
````
**Removendo todas Networks**
````
docker network prune
````
**Inspecionando a rede padrão**
````
docker run -d -it --name ubuntu1 bash
docker run -d -it --name ubuntu2 bash
docker inspect bridge
````
**Conectando no containner**
````
docker attach ubuntu1
````

**Criando Network** 
````
docker network create --driver bridge minha_rede
`````
**Rodando containner na network criada**
````
docker run -d -it --name ubuntu1 --network minha_rede bash
docker run -d -it --name ubuntu2 --network minha_rede bash
docker run -d -it --name ubuntu3 bash
````
**Conectando containner na network criada**
````
docker network connect minha_rede ubunto3
`````
> Ao criar uma rede é possível uma comunicação entre os containers usando o nome dado para o container.Um exemplo do container ubuntu1 é possível se comunicar com ubuntu2 pelo nome a uma resolução.
> Já na rede padrão é possível se comunicar apenas pelo ip gerado na rede.

#### Host Network

**Subindo container na mesma rede da maquina host docker**
````
docker rum --rm -d --name nginx_lppires --network host nginx
````

#### Container acessando maquina host docker

Para um container acessar a maquina host docker podemos utilizar a opção 
http://host.docker.internal:port.
Exemplo, na maquina host tem uma aplicação rodando na porta 8000, para meu container consumir esse recurso poderia ser utilizado este comando. 
````
curl http://host.docker.internal:8000
````
## Práticas 

##### 1) Na pasta pratica-lareval, essa pratica demostra a criação e instalação do framework laravel em um dockerfile.

**Criando imagem**
````
docker build -t lppires/laravel:latest .
````
**Subindo a imagen laravel utilizando CMD do dockerfile**
````
docker run --rm --name laravel -p 8000:8000 lppires/laravel:latest
````
**Subindo a imagen laravel subistituindo o CMD do dockerfile, pelo argumento pasado(--host=0.0.0.0 --port=8001)**
````
docker run --rm --name laravel -p 8000:8000 lppires/laravel:latest --host=0.0.0.0 --port=8001
````

#### 2)Na pasta pratica-node é criando um ambiente de desenvolvimento em node onde o que é alterado no container é alterado na maquina host e o que é alterado na host é alterado no container.
````
docker run --rm -it -v $(pwd)/:/usr/src/app -p 3000:3000 node:15 bash
````

## Otimizando Imagens

**No exemplo foi gerado o arquivo dockerfile.prod do projeto laravel. Quando este build for executado ele vai rodar em dois estagios reduzindo o tamanho da imagem.**
````
docker build -t lppires/laravel:prod . -f Dockerfile.prod
````

![Exemplo Tamanhos](https://github.com/lpradopires/curso-fullcycle/blob/main/documentos/imagemlaravel.png)


## Desafio



## Meus exercicios

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
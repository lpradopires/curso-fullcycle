FROM node

LABEL authors="Leandro Prado Pires"

# instalando a angular-cli
RUN npm install -g npm@7.7.6
RUN npm install -g @angular/cli

# navegando pasta projetos em usuario, se não existir vai criar.
WORKDIR /usr/projetos/

# atualizando bibliotecas do projetos
RUN npm install

# subindo o projeto.
ENTRYPOINT [ "ng", "serve", "--host", "0.0.0.0"]

EXPOSE 4200

# docker run -d --name app -p 8089:4200 --mount type=bind,source="$(pwd)"/lista,target=/usr/projetos lpradopires/projetoangular:v1

# docker build -t lpradopires/projetoangular:v1 .


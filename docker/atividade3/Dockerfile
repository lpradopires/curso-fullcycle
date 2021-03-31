FROM node

LABEL authors="Leandro Prado Pires"

RUN npm install -g npm@7.7.6

WORKDIR /usr/projetos/

COPY ["./*", "/usr/projetos/"]

RUN npm install

ENTRYPOINT ["node", "index.js"]

EXPOSE 3000
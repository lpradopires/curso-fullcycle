FROM node

LABEL authors="Leandro Prado Pires"

RUN npm install -g @angular/cli

# RUN ng new projeto-lista --interactive=false --directory=/usr/projetos/lista

# "$(pwd)"/lista

#  docker run  -d --name app -p 8089:4200 --mount type=bind,source="/usr/projetos/lista,target="$(pwd)"/lista lpradopires/projetoangular

WORKDIR /usr/projetos

RUN npm install

ENTRYPOINT [ "ng", "serve", "--host", "0.0.0.0", "--port", "4200"]

EXPOSE 4200

# RUN node -v
# RUN npm -v





# COPY ["package.json", "npm-shrinkwrap.json*", "./"]
# RUN npm install --silent
# COPY . .
# RUN ng build --prod

# # Node server
# FROM node:12-alpine as node-server
# WORKDIR /usr/src/app
# COPY ["package.json", "npm-shrinkwrap.json*", "./"]
# RUN npm install --production --silent && mv node_modules ../
# COPY server.js .
# COPY /server /usr/src/app/server

# # Final image
# FROM node:12-alpine
# WORKDIR /usr/src/app
# COPY --from=node-server /usr/src /usr/src
# COPY --from=client-app /usr/src/app/dist ./
# EXPOSE 3000
# # CMD ["node", "server.js"]
# CMD ["npm", "start"]

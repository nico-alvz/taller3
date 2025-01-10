FROM node:16

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["sh", "-c", "npx sequelize db:create && npx sequelize db:migrate && npx sequelize db:seed:all && npm start"]

FROM node
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
EXPOSE 80
ENV DB_USERNAME=
ENV DB_PASSWORD=
ENV DB_URL=
CMD [ "npm", "start"]
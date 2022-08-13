FROM node:14.16.0-alpine3.13
RUN addgroup joaoc && adduser -S -G joaoc joaoc
USER joaoc
WORKDIR /app/
RUN mkdir data
COPY package*.json .
RUN npm install
COPY . .
ENV API_URL=http://api.orders:8080
EXPOSE 3000
CMD ["npm" ,"start"]
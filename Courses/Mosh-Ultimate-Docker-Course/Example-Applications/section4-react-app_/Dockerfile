FROM node:14.16.0-alpine3.13
WORKDIR /app/
COPY . .
RUN npm install
ENV API_URL=http://api.orders:8080
EXPOSE 3000
RUN addgroup joaoc && adduser -S -G joaoc joaoc
USER joaoc
FROM node:16-alpine AS builder
LABEL authors="snkatvit"

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

RUN npm run ng build

FROM nginx:1.25-alpine-slim

COPY ./nginx.conf /etc/nginx/nginx.conf
COPY --from=builder /app/dist/frontend /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
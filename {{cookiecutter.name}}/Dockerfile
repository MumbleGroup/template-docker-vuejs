# syntax = docker/dockerfile:experimental
# develop stage
FROM node:18-alpine as build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

RUN npm run build

# production stage
FROM nginx:1.25.0-alpine as production-stage
COPY --from=build-stage /app/dist/spa /usr/share/nginx/html
# RUN rm /etc/nginx/conf.d/default.conf
COPY --from=build-stage /app/nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
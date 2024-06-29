# Build stage
FROM node:12.1-alpine as node

WORKDIR /src
COPY . .

RUN npm install && npm run build

# Run Stage
FROM nginx:alpine as run
COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=node /src/dist /usr/share/nginx/html/movies

# docker build -t movies-app:dev .
# docker run -d -p 4400:80 movie-app:dev --name movies-app

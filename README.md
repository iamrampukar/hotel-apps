# Stage 1
FROM node:14.20.0-alpine as node
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build --prod
# Stage 2
FROM nginx:alpine
COPY --from=node /app/dist/hotel-apps /usr/share/nginx/html

# Source
-- https://javascript.plainenglish.io/how-to-dockerize-angular-application-3cd67e963832
# How to run
-- docker build -t hotel-apps .
-- docker run -d -it -p 80:80/tcp --name hotel-apps hotel-apps:latest
OR
-- docker run -d -p 8080:80 --name hotel-apps hotel-apps:latest
-- docker run -d -p 4200:80 --name hotel-apps hotel-apps:latest

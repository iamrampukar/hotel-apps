# Stage 1
FROM node:14.20.0-alpine as node
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build --prod
# Stage 2
FROM nginx:alpine
COPY --from=node /app/dist/hotel-apps /usr/share/nginx/html

# How to run
-- docker build -t hotel-apps .
-- docker run -d -it -p 80:80/tcp --name hotel-apps hotel-apps:latest

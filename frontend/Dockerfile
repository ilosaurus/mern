#Stage 1
FROM node:10.16-alpine AS builder

#Set Workdir and Copy Context
WORKDIR /app
COPY package.json .
RUN npm install --quiet
COPY . .

#Set ENV
ARG API_SERVER
ENV API_SERVER=$API_SERVER
ARG API_PORT
ENV API_PORT=$API_PORT

#Build Package
RUN npm run build

#Stage 2
FROM nginx:stable-alpine
COPY --from=builder /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

#Construcción
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

#Servidor Web (Nginx)
FROM nginx:alpine
# Copia a la carpeta de Nginx
COPY --from=builder /app/dist /usr/share/nginx/html

# Minimo privilegio para Nginx
RUN chown -R nginx:nginx /usr/share/nginx/html /var/cache/nginx /var/log/nginx /etc/nginx/conf.d
USER nginx

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
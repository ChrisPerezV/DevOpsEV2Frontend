# ETAPA 1: compilar con Node
FROM node:20-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
ARG VITE_API_DESPACHO
ARG VITE_API_VENTAS
ENV VITE_API_DESPACHO=$VITE_API_DESPACHO
ENV VITE_API_VENTAS=$VITE_API_VENTAS
RUN npm run build

# ETAPA 2: servir con Nginx sin privilegios
FROM nginxinc/nginx-unprivileged:alpine
COPY --from=build /app/dist /usr/share/nginx/html
# Copiamos el archivo como un template
COPY nginx.conf /etc/nginx/templates/default.conf.template
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
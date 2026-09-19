# Étape 1 : Build de l'application React avec Vite
FROM node:20-alpine AS build

WORKDIR /app

# Copie des fichiers de dépendances
COPY package*.json ./
RUN npm ci

# Copie du code source et compilation
COPY . .
RUN npm run build

# Étape 2 : Serveur de production Nginx
FROM nginx:alpine

# Copie de la configuration personnalisée Nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copie du build statique depuis l'étape de compilation
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

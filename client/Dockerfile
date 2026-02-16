# ===== Build Stage =====
FROM node:20-alpine AS builder

WORKDIR /app

# Copier les fichiers de dépendances
COPY package*.json ./

# Installer les dépendances
RUN npm ci --only=production

# Copier tout le code source
COPY . .

# Build pour production (crée le dossier /build)
RUN npm run build

# ===== Production Stage avec Nginx =====
FROM nginx:alpine

# Copier les fichiers buildés depuis le stage builder
COPY --from=builder /app/build /usr/share/nginx/html

# Créer une configuration nginx personnalisée
RUN rm /etc/nginx/conf.d/default.conf

COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 3000


CMD ["nginx", "-g", "daemon off;"]

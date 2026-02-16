FROM node:20-alpine

WORKDIR /app

COPY package*.json ./

RUN npm ci --only=production

COPY . .

RUN npm run build

# Ce service n'expose pas de port HTTP

CMD ["npm", "start"]


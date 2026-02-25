# -------- STAGE 1 : BUILD --------
FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm ci 

COPY . .

RUN npm run build

# Ce service n'expose pas de port HTTP
# -------- STAGE 2 : PRODUCTION --------
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY --from=builder /app/build ./build

CMD ["npm", "start"]


# -------- STAGE 1 : BUILD --------
FROM node:20-alpine AS Builder

WORKDIR /app

COPY package*.json ./

RUN npm ci

COPY . .

RUN npm run build

# -------- STAGE 2 : PRODUCTION --------
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./

RUN npm ci --only=production

COPY --from=builder /app/build ./build

EXPOSE 3000

CMD ["npm", "start"]


# Stage 1: Build
FROM node:20-alpine AS builder

WORKDIR /app
COPY package.json pnpm-lock.yaml* package-lock.json* yarn.lock* ./
RUN npm install -g pnpm && pnpm install

COPY . .
RUN pnpm build

# Stage 2: Run
FROM node:20-alpine

WORKDIR /app

# ✅ 本番ステージでも pnpm をインストールする
RUN npm install -g pnpm

COPY --from=builder /app ./

ENV NODE_ENV=production
ENV HOST=0.0.0.0
EXPOSE 3000

CMD ["pnpm", "start"]
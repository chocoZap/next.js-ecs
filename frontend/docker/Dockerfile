# --- Stage 1: Build stage ---
FROM node:20-alpine AS builder

WORKDIR /app

# グローバルに pnpm インストール
RUN npm install -g pnpm

# package.json のみを確実にコピー
COPY package.json ./

# ソースコードを全体コピー
COPY . .

# lockファイルがある場合だけ追加コピー（ないなら無視）
# これは Dockerfile では直接 if 分岐できないので、1行でやるなら:
COPY pnpm-lock.yaml* ./

# 依存関係インストール（dev含む）
RUN pnpm install

# 本番ビルド（.next を生成）
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

FROM node:20-alpine AS builder

WORKDIR /app


COPY package.json package-lock.json ./


COPY backend/package.json ./backend/


RUN npm install --workspace backend --legacy-peer-deps


COPY backend/tsconfig.json ./backend/
COPY backend/src ./backend/src


RUN npm run build --workspace backend


FROM node:20-alpine AS production

WORKDIR /app


COPY package.json package-lock.json ./
COPY backend/package.json ./backend/


RUN npm install --workspace backend --omit=dev --legacy-peer-deps


COPY --from=builder /app/backend/dist ./backend/dist

WORKDIR /app/backend

EXPOSE 5000

CMD ["node", "dist/server.js"]

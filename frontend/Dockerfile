
FROM node:20-alpine AS builder

WORKDIR /app


COPY package.json package-lock.json ./


COPY frontend/package.json ./frontend/


RUN npm install --workspace frontend --legacy-peer-deps


COPY frontend/ ./frontend/


ARG VITE_API_URL
ENV VITE_API_URL=${VITE_API_URL}


RUN cd frontend && npx vite build


FROM nginx:alpine AS production


COPY --from=builder /app/frontend/dist /usr/share/nginx/html


COPY frontend/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

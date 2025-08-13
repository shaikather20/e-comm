# Build stage
FROM node:18 AS builder
WORKDIR /app

# 1. Copy package files
COPY package.json package-lock.json ./

# 2. Install all dependencies (including Vite)
RUN npm install

# 3. Copy frontend source code
COPY frontend/ .

# 4. Build the app (outputs to /app/frontend/dist)
RUN npm run build

# Production stage
FROM nginx:alpine

# 5. Copy built files to nginx
COPY --from=builder /app/frontend/dist /usr/share/nginx/html

# 6. Basic nginx config for React routing
RUN echo "server {" > /etc/nginx/conf.d/default.conf && \
    echo "    listen 80;" >> /etc/nginx/conf.d/default.conf && \
    echo "    location / {" >> /etc/nginx/conf.d/default.conf && \
    echo "        root /usr/share/nginx/html;" >> /etc/nginx/conf.d/default.conf && \
    echo "        index index.html;" >> /etc/nginx/conf.d/default.conf && \
    echo "        try_files \$uri \$uri/ /index.html;" >> /etc/nginx/conf.d/default.conf && \
    echo "    }" >> /etc/nginx/conf.d/default.conf && \
    echo "}" >> /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

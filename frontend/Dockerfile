# Build stage
FROM node:18 AS builder
WORKDIR /app

# Copy package files
COPY package.json package-lock.json ./

# Install all dependencies (including devDependencies)
RUN npm install --include=dev

# Copy frontend source
COPY frontend/ .

# Build the app
RUN npm run build

# Production stage
FROM nginx:alpine
COPY --from=builder /app/frontend/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

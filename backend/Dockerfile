FROM node:18

WORKDIR /app

COPY package*.json ./
COPY . .

RUN npm install

# Use production start, not dev
CMD ["npm", "start"]

EXPOSE 5000

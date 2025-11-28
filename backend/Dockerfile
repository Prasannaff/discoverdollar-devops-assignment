FROM node:18-alpine

WORKDIR /usr/src/app

# Copy package files
COPY package*.json ./

# Install ALL dependencies instead of using npm ci production only
RUN npm install --legacy-peer-deps

# Copy the rest of the backend code
COPY . .

ENV NODE_ENV=production
EXPOSE 3000

CMD ["node", "server.js"]

# backend/Dockerfile
FROM node:18-alpine

WORKDIR /usr/src/app

# copy dependency manifests for caching
COPY package*.json ./

# install production deps
RUN npm install --only=production

# copy rest of backend source (context is backend/)
COPY . .

# If you need a build step, uncomment:
# RUN npm run build

ENV NODE_ENV=production
EXPOSE 3000

# Use npm start (ensure package.json has "start")
CMD ["npm", "start"]

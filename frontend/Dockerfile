# frontend/Dockerfile
FROM node:18-alpine as builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build -- --configuration production

FROM nginx:stable-alpine
COPY --from=builder /app/dist/your-app-name /usr/share/nginx/html
# optional: include your custom nginx conf if you want to control caching etc.
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

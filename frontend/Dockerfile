# frontend/Dockerfile

# -------- build stage --------
FROM node:18-alpine AS build
WORKDIR /app

# copy package files and install deps (use package-lock if present)
COPY package*.json ./
RUN npm install

# copy entire frontend source (context is the frontend folder)
COPY . .

# build the Angular app (generic command works for recent Angular)
RUN npm run build

# -------- runtime stage (nginx) --------
FROM nginx:stable-alpine AS runtime
# the dist folder name must match what you saw earlier: angular-15-crud
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

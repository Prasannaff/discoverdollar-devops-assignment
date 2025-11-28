# frontend/Dockerfile (multi-stage)

# ------------ Stage 1: build the Angular app ------------
FROM node:18-alpine AS builder
WORKDIR /app

# copy package files and install dependencies
COPY package*.json ./
RUN npm ci

# copy source and build production
COPY . .
RUN npm run build -- --configuration production

# ------------ Stage 2: serve with nginx ------------
FROM nginx:stable-alpine
# set default dist folder so Dockerfile is self-contained
ARG DIST_FOLDER=angular-15-crud

# clean default nginx html
RUN rm -rf /usr/share/nginx/html/*

# copy built files from builder stage (uses ARG)
COPY --from=builder /app/dist/${DIST_FOLDER} /usr/share/nginx/html

# (optional) If you want to use your custom nginx config, uncomment:
# COPY nginx/default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

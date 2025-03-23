# Stage 1: Build the static website
FROM node:18-alpine AS builder

WORKDIR /app

# Install dependencies using npm
COPY package.json package-lock.json ./

# Install without dev dependencies
RUN npm ci --omit=dev

# Copy source files
COPY . .

# Build Expo static web
RUN npx expo export --platform web

# Stage 2: Serve with NGINX
FROM nginx:alpine

# Copy built static site to NGINX serving directory
COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

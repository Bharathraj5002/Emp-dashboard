# Build stage
FROM node:18-alpine AS build

WORKDIR /app

COPY package*.json ./

# Install dependencies
RUN npm install

COPY . .

# Set legacy OpenSSL provider for Node 18+
ENV NODE_OPTIONS=--openssl-legacy-provider

# Build the Angular app
RUN npm run build --prod

# Production stage
FROM nginx:alpine

# Copy build output to nginx
COPY --from=build /app/dist/angular-frontend /usr/share/nginx/html

# Copy custom nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]

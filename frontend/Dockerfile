# frontend/Dockerfile

# ---- Stage 1: Build Angular App ----
FROM node:18-alpine AS build

WORKDIR /app

# Copy Angular package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the frontend code
COPY . .

# Build Angular app (outputs to dist folder)
RUN npm run build -- --output-path=dist

# ---- Stage 2: Serve App with Nginx ----
FROM nginx:stable-alpine

# Copy Angular build output to Nginx web root
COPY --from=build /app/dist/ /usr/share/nginx/html

# Copy custom Nginx config to handle SPA routing
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
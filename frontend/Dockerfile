# Step 1: Build the React app
FROM node:18-alpine AS build
WORKDIR /app
COPY package.json ./
RUN npm install
COPY . ./

# Step 6: Add the OpenSSL legacy provider environment variable
ENV NODE_OPTIONS=--openssl-legacy-provider

# Step 7: Build the app
RUN npm run build

# Step 8: Serve the React app with Nginx
FROM nginx:stable-alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

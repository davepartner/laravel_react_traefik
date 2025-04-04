# Use an official Node.js image
FROM node:18

# Set working directory
WORKDIR /usr/src/app

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the React app
COPY . .

# Build the React app for production
RUN npm run build

# Use a lightweight server to serve the app
FROM nginx:alpine
COPY --from=0 /usr/src/app/build /usr/share/nginx/html

# Expose port 80 (Nginx default)
EXPOSE 80
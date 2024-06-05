# Use an official Node.js image as the base image
FROM node:16 AS build

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application files to the container
COPY . .

# Build the React app
RUN npm run build

# Stage 2: Serve the React app with an HTTP server
FROM nginx:alpine

# Copy the built files from the previous stage to the Nginx html directory
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 1161

# Command to run Nginx
CMD ["nginx", "-g", "daemon off;"]

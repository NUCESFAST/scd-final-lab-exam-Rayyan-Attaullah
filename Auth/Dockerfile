# Use the official Node.js image as the base image
FROM node:16

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install

# Copy the rest of the code to the working directory
COPY . .

# Expose the port the auth service uses
EXPOSE 1161

# Command to run the auth service server
CMD ["node", "index.js"]

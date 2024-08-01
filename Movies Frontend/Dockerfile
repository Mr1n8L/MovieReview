# Use the official Node.js image as the base image
FROM node:18-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the React app
RUN npm run build

# Use the official Nginx image to serve the built React app
FROM nginx:alpine

# Copy the built React app to the Nginx HTML directory
COPY --from=0 /app/build /usr/share/nginx/html

# Expose the port Nginx will run on
EXPOSE 80

# Define the command to run Nginx
CMD ["nginx", "-g", "daemon off;"]

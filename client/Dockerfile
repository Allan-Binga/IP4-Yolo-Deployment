# Use an official Node runtime as a parent image
FROM node:14-slim AS build

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

# Install application dependencies
RUN npm install

# Copy the rest of the application code to the container
COPY . .

# Run the build command to generate the /app/build directory
RUN npm run build

# Stage 2: Use nginx to serve the build
FROM nginx:alpine

# Set the working directory for nginx
WORKDIR /app

# Install npm (if needed for the server-side part)
# RUN apk update && apk add npm

# Copy the build output from the first stage to the nginx server
COPY --from=build /usr/src/app/build /usr/share/nginx/html

# Expose the port the app runs on
EXPOSE 80

# Define the command to run nginx
CMD ["nginx", "-g", "daemon off;"]

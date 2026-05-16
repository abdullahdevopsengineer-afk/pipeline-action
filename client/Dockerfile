# Use an official Node.js runtime as a parent image
# FROM node:20
# # Set the working directory in the container
# WORKDIR /app
# # Copy package.json and package-lock.json to the working directory
# COPY package*.json .
# # Install the dependencies
# RUN npm install 
# # Copy the rest of the application code to the working directory
# COPY . .
# # Build the React application
# RUN npm run build 
# # Install serve to serve the built application
# RUN npm install -g serve
# # Expose the port that the application will run on
# EXPOSE 3000
# # Command to run the application
# CMD [ "serve","dist","-s","-l","3000"]

# ----Multistage Build----
# Use an official Node.js runtime as a parent image for the build stage
FROM node:20 AS builder
WORKDIR /app
COPY package*.json .
RUN npm install
COPY .  .
RUN npm run build 
# Use an official Node.js runtime as a parent image for the production stage
FROM node:20-alpine
WORKDIR /app
RUN npm install -g serve
COPY --from=builder /app/dist ./dist
EXPOSE 3000
CMD [ "serve","dist","-s","-l","3000"]


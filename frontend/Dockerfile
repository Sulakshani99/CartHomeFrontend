# Use the official Node.js image from the Docker Hub
FROM node:latest

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy the contents of the local "CartHome_Frontend" directory to the container's working directory
COPY CartHome_Frontend/ .

# Install dependencies using npm or yarn
RUN npm install

# Build your React app (if necessary)
# RUN npm run build

# Expose port 3000 to allow access to the React app from outside the container
EXPOSE 3000

# Start the React app (adjust as needed based on your application setup)
CMD ["npm", "start"]

# Start from Node.js 22 (LTS) image
FROM node:lts-alpine3.21

# Specify the directory the image in which all commands will run
WORKDIR /usr/src/app

# Copy package files and install dependencies.
COPY package*.json ./
RUN npm install
RUN npm install express

# Copy all of the app files into the image
COPY . .

# The default command to run when starting the container
CMD ["npm","start"]
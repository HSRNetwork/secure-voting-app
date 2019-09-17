# Using official and latest node runtime base image based on Linux Alpine (tag name: current-alpine)
FROM node:current-alpine

# Set the application directory
RUN mkdir -p /app
WORKDIR /app

# Install our python dependencies
RUN npm config set registry https://registry.npmjs.org
COPY package.json /app/package.json
RUN npm install \
 && npm ls \
 && npm cache clean --force \
 && mv /app/node_modules /node_modules

# Copy our code from the current folder to /app inside the container
COPY . /app

# Ensure the service user has access to the /app directory
RUN chown -R node:node /app

# Drop user priviledges to the already existing service user "node"
USER node

# Make port 80 available for links and/or publish
EXPOSE 80

# Set the environment variable PORT inside the docker image. Node uses this to choose the port to run on.
ENV PORT 80

# Define our default command to be run when launching the container
ENTRYPOINT [ "node" ]
CMD [ "server.js" ]

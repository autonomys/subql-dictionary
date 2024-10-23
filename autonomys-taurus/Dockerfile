# Use the base image for the subql-node
FROM onfinality/subql-node:latest

# Switch to root user to install packages
USER root

# Install Python and build tools
RUN apk update && apk add --no-cache python3 make g++

# Switch back to the default user
USER node

# Set the working directory
WORKDIR /app

# Copy the package.json files
COPY package.json ./

# Install dependencies
RUN yarn install

# Copy the rest of the application
COPY . .

# Change ownership of the directory to the node user
USER root
RUN chown -R node:node /app

# Switch back to the default user
USER node

# Run codegen and build
RUN yarn codegen && yarn build
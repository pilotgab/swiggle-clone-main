# Use Node.js 16 slim as the base image
FROM node:16-slim

# Create a non-root user and group
RUN groupadd -g 1001 appuser && \
    useradd -m -u 1001 -g appuser appuser

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install only production dependencies
RUN npm install --omit=dev

# Copy the rest of the application code
COPY . .

# Build the React app
RUN npm run build

# Change ownership of the app directory to the non-root user
RUN chown -R appuser:appuser /app

# Switch to the non-root user
USER appuser

# Expose port 3000 (since the app listen on port 3000)
EXPOSE 3000

# Start the Node.js server (since it serves the React app)
CMD ["npm", "start"]

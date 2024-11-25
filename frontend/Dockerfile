# Use a smaller Node.js version (e.g., 18-slim) to reduce image size
FROM node:18-slim as frontend

# Set the working directory
WORKDIR /app

# Copy only the package files first to optimize cache usage
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install --production

# Copy the rest of the application files
COPY . .

# Expose the port the development server runs on
EXPOSE 5173

# Run the development server (use --host to allow external connections)
CMD ["npm", "run", "dev", "--", "--host"]


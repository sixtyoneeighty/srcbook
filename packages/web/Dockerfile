FROM node:18-alpine

WORKDIR /app

# Copy package files
COPY package.json ./

# Install pnpm and dependencies
RUN npm install -g pnpm && \
    pnpm install

# Copy source code
COPY . .

# Build the application
RUN pnpm run build

# Install serve to host the static files
RUN npm install -g serve

# Expose port
EXPOSE 3000

# Start the server
CMD ["serve", "-s", "dist", "-p", "3000"]

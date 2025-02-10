FROM node:18-alpine

WORKDIR /app

# Copy package files
COPY package.json ./

# Install pnpm and typescript
RUN npm install -g pnpm typescript

# Install dependencies
RUN pnpm install

# Copy source code
COPY . .

# Build the application
RUN pnpm run build

# Expose port
EXPOSE 3000

# Start the application
CMD ["pnpm", "start"]

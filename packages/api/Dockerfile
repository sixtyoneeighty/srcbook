FROM node:18-alpine

WORKDIR /app

# Install build dependencies for better-sqlite3
RUN apk add --no-cache python3 make g++ sqlite-dev

# Copy package files
COPY package.json ./

# Install pnpm, typescript, and node-gyp
RUN npm install -g pnpm typescript node-gyp

# Install dependencies
RUN pnpm install

# Copy source code
COPY . .

# Build the application and rebuild better-sqlite3
RUN pnpm run build && cd node_modules/better-sqlite3 && node-gyp rebuild

# Expose port
EXPOSE 3000

# Set environment to production
ENV NODE_ENV=production

# Start the application
CMD ["pnpm", "start"]

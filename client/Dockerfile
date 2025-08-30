# Multi-stage build for React app
# Build stage
FROM node:16-alpine AS builder

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies (include devDependencies for build)
RUN npm install

# Copy source code
COPY . .

# Build arguments for React environment variables
ARG REACT_APP_BACK_URL
ARG REACT_APP_S3_URL
ARG REACT_APP_CHANNELTALK_PLUGIN_KEY
ARG REACT_APP_GA_TRACKING_ID

# Build the React app
RUN npm run build

# Runtime stage with nginx
FROM nginx:alpine

# Install curl for health check
RUN apk add --no-cache curl

# Copy built files from builder stage
COPY --from=builder /app/build /usr/share/nginx/html

# Copy nginx configuration
COPY nginx.conf /etc/nginx/nginx.conf

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]

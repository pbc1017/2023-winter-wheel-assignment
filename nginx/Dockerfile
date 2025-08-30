# Nginx reverse proxy
FROM nginx:alpine

# Install curl for health check
RUN apk add --no-cache curl

# Remove default nginx config
RUN rm /etc/nginx/nginx.conf

# Copy custom nginx configuration
COPY nginx.conf /etc/nginx/nginx.conf

# Create log directory
RUN mkdir -p /var/log/nginx

# Note: nginx -t test is skipped during build as upstream servers don't exist yet

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]

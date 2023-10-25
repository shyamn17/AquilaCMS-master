# Use the official Nginx image as the base image
FROM nginx:latest
# Remove the default Nginx configuration file
RUN rm /etc/nginx/conf.d/default.conf
# Copy your HTML files into the Nginx web root directory
COPY . /usr/share/nginx/html/
# Copy your custom Nginx configuration to replace the default one
COPY nginx.conf /etc/nginx/nginx.conf
# Expose the container on port 8000
EXPOSE 8000
# Start Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]

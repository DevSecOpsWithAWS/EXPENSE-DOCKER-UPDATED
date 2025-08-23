# Use stable nginx alpine image
FROM nginx:stable-alpine3.20-perl

# Clean default files
RUN rm -rf /usr/share/nginx/html/index.html \
    && rm -rf /etc/nginx/nginx.conf \
    && rm -rf /etc/nginx/conf.d/default.conf

# Create necessary temp/cache directories with proper permissions
RUN mkdir -p /var/cache/nginx/client_temp \
    && mkdir -p /var/cache/nginx/proxy_temp \
    && mkdir -p /var/cache/nginx/fastcgi_temp \
    && mkdir -p /var/cache/nginx/uwsgi_temp \
    && mkdir -p /var/cache/nginx/scgi_temp \
    && chown -R nginx:nginx /var/cache/nginx \
    && chown -R nginx:nginx /etc/nginx/ \
    && chmod -R 755 /etc/nginx/ \
    && chown -R nginx:nginx /var/log/nginx

# SSL dir if you later add HTTPS
RUN mkdir -p /etc/nginx/ssl/ \
    && chown -R nginx:nginx /etc/nginx/ssl/ \
    && chmod -R 755 /etc/nginx/ssl/

# Nginx PID file
RUN touch /var/run/nginx.pid \
    && chown -R nginx:nginx /var/run/nginx.pid /run/nginx.pid

# Copy your custom nginx configs
COPY nginx.conf /etc/nginx/nginx.conf
COPY default.conf /etc/nginx/conf.d/default.conf

# Copy frontend build files
COPY build/ /usr/share/nginx/html/

# Run container as non-root nginx user
USER nginx

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

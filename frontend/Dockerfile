FROM nginx
RUN rm -rf /usr/share/nginx/html/index.html
# RUN rm -rf /etc/nginx/nginx.conf
# COPY nginx.conf /etc/nginx/nginx.conf
# COPY code /usr/share/nginx/html

RUN rm -rf /etc/nginx/conf.d/default.conf

# Copy your custom nginx config into the right place
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copy frontend build files (React/Angular/Vue "build" folder should be mapped to code/)
COPY code /usr/share/nginx/html
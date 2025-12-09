FROM nginx
COPY app-code /usr/share/nginx/html
RUN rm -rf /etc/nginx/nginx.conf
RUN rm -rf /etc/nginx/conf.d/default.conf
COPY localhost.conf /etc/nginx/nginx.conf
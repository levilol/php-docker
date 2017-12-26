FROM nginx
COPY docker/nginx/app.conf /etc/nginx/conf.d/app.conf
COPY . /var/www/html
COPY docker/nginx/nginx.crt /etc/nginx/nginx.crt
COPY docker/nginx/nginx.key /etc/nginx/nginx.key
COPY docker/nginx/dhparam.pem /etc/nginx/dhparam.pem
EXPOSE 80 443

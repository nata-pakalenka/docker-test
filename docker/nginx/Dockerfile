FROM debian:jessie

RUN apt-get update && apt-get install -y \
    nginx

COPY nginx.conf /etc/nginx/
COPY symfony.conf /etc/nginx/sites-enabled/

RUN rm /etc/nginx/sites-available/default
#RUN echo "upstream php-upstream { server php:9000; }" > /etc/nginx/conf.d/upstream.conf

RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80
EXPOSE 443
FROM debian:jessie

# Import variables from docker-compose file
ARG PROJECT_NAME
ARG PROJECT_DOMEN

RUN apt-get update && apt-get install -y nginx

ADD nginx.conf /etc/nginx/
ADD settings.conf /etc/nginx/sites-available/

RUN rm /etc/nginx/sites-enabled/default
RUN mv /etc/nginx/sites-available/settings.conf /etc/nginx/sites-available/${PROJECT_NAME}.conf

RUN sed -i 's/{PROJECT_NAME}/'$PROJECT_NAME'/g' /etc/nginx/sites-available/${PROJECT_NAME}.conf
RUN sed -i 's/{PROJECT_DOMEN}/'$PROJECT_DOMEN'/g' /etc/nginx/sites-available/${PROJECT_NAME}.conf

RUN ln -s /etc/nginx/sites-available/${PROJECT_NAME}.conf /etc/nginx/sites-enabled/${PROJECT_NAME}.conf

RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80
EXPOSE 443

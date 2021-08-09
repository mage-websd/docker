FROM nginx:latest

COPY nginx.conf /etc/nginx/nginx.conf
RUN mkdir -p /etc/nginx/sites-available/
RUN mkdir -p /etc/ssl/sd_site/
COPY ./stage/sites/ /etc/nginx/sites-available/
COPY ./sd.conf /etc/nginx/sd.conf

RUN apt update -y && \
    apt install openssl -y && \
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/sd_site/nginx_cer_key.key -out /etc/ssl/sd_site/nginx_cer.crt -subj "/C=GB/ST=London/L=London/O=Global Security/OU=IT Department/CN=sd.net"

CMD ["nginx", "-g", "daemon off;"]

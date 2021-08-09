FROM nginx:latest

COPY nginx.conf /etc/nginx/nginx.conf
RUN mkdir -p /etc/nginx/sites-available/
RUN mkdir -p /etc/letsencrypt/
COPY ./prod/sites/ /etc/nginx/sites-available/
COPY ./sd.conf /etc/nginx/sd.conf

CMD ["nginx", "-g", "daemon off;"]

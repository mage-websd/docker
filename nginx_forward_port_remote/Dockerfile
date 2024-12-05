FROM nginx:1.27.0-alpine

RUN apk update && apk add openssh-client

COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./app.conf /etc/nginx/conf.d/default.conf

ENTRYPOINT ["nginx", "-g", "daemon off;"]

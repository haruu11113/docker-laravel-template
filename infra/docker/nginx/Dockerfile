FROM nginx:1.22

WORKDIR /home/ec2-user/code/ea

ENV TZ=UTC

COPY ./infra/docker/nginx/*.conf /etc/nginx/conf.d/
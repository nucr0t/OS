FROM debian:buster

RUN apt-get update -y -q && apt-get upgrade -y -q && \
apt-get install nginx -y -q && apt-get clean --dry-run
RUN rm -rf /var/www/* && mkdir --parents /var/www/rusal.com/img

COPY index.html /var/www/rusal.com/index.html
COPY img.jpg /var/www/rusal.com/img/img.jpg

RUN chmod -R '0754' /var/www/rusal.com/ && useradd rus && groupadd lan &&\
usermod -a -G lan rus && chown -R rus:lan /var/www/rusal.com/ && \
sed -i --follow-symlinks 's/\(^\s*root \)\(\/var\/www\/html;\)$/\1\/var\/www\/rusal\.com;/' /etc/nginx/sites-enabled/default &&\
sed -i 's/^user\s*\S*$/user rus;/' /etc/nginx/nginx.conf

EXPOSE 80/tcp

CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
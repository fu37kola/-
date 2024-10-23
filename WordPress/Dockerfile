FROM debian:latest

RUN apt-get -y -q update; \
    apt-get -y -q install apache2 xxd git unzip wget lsb-release apt-transport-https ca-certificates gnupg

RUN wget -qO - https://packages.sury.org/apt.gpg | apt-key add -; \
    echo "deb https://packages.sury.org/php/ $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/php.list; \
    apt-get -y -q update

RUN apt-get -y -q install php7.2 php7.2-simplexml php7.2-gd php7.2-ldap php7.2-zip php7.2-imap php7.2-mysql php7.2-mbstring mariadb-client mariadb-server

RUN service mariadb start; \
    mysql -u root -e "CREATE DATABASE db; CREATE USER 'db'@'%' IDENTIFIED BY 'db'; GRANT ALL PRIVILEGES ON *.* TO 'db'@'%' WITH GRANT OPTION; FLUSH PRIVILEGES;"

COPY wordpress-5.0-zh_CN.zip /tmp/wordpress-5.0-zh_CN.zip
RUN cd /var/www/html/; rm index.html; \
    unzip /tmp/wordpress-5.0-zh_CN.zip -d /var/www/html/; \
    rm /tmp/wordpress-5.0-zh_CN.zip

RUN chown www-data: -R /var/www/

RUN echo "#!/bin/bash" > /entrypoint.sh; \
    echo "service mariadb start" >> /entrypoint.sh; \
    echo "apachectl -D FOREGROUND" >> /entrypoint.sh; \
    chmod +x /entrypoint.sh

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

EXPOSE 80

CMD /entrypoint.sh

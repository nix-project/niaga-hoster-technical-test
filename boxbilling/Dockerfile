FROM debian:10
RUN apt update -y && apt install cron gnupg gnupg2 gnupg1 wget unzip -y && apt install apache2 php php-json php-pdo php-mysql \
   php-curl php-mbstring php-gettext libapache2-mod-php -y && apt install debconf-utils -y
RUN sed -i -e 's/Listen 80/Listen 80\nServerName localhost/' /etc/apache2/ports.conf
RUN a2enmod rewrite
COPY apache2.conf /etc/apache2/
RUN service apache2 start
RUN rm /var/www/html/index.html
WORKDIR /var/www/html
COPY daemon.sh .
RUN wget https://github.com/boxbilling/boxbilling/releases/download/v4.22-beta.1/BoxBilling.zip
RUN unzip BoxBilling.zip && rm BoxBilling.zip
RUN chmod 777 -R /var/www/html/*
RUN cp /var/www/html/bb-config-sample.php /var/www/html/bb-config.php
EXPOSE 80
RUN wget http://dev.mysql.com/get/mysql-apt-config_0.7.3-1_all.deb
RUN DEBIAN_FRONTEND=noninteractive apt install ./mysql-apt-config_0.7.3-1_all.deb -y
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 8C718D3B5072E1F5
RUN apt update
RUN DEBIAN_FRONTEND=noninteractive
RUN { \
        echo mysql-community-server mysql-community-server/data-dir select ''; \
        echo mysql-community-server mysql-community-server/root-pass password '123456'; \
        echo mysql-community-server mysql-community-server/re-root-pass password '123456'; \
        echo mysql-community-server mysql-community-server/remove-test-db select false; \
    } | debconf-set-selections && DEBIAN_FRONTEND=noninteractive apt install mysql-community-server -y
RUN chmod 777 -R /var/www/html/*
RUN echo "*/5 * * * * php /var/www/html/bb-cron.php" | crontab -
CMD ["./daemon.sh"]
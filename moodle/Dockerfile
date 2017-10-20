# Dockerfile for moodle instance. 
FROM ubuntu:16.04
MAINTAINER jumpei.iwamura<j.iwamura1986@gmail.com>

VOLUME ["/var/moodledata"]
EXPOSE 80 443

# Keep upstart from complaining
# RUN dpkg-divert --local --rename --add /sbin/initctl
# RUN ln -sf /bin/true /sbin/initctl

# Let the container know that there is no tty
ENV DEBIAN_FRONTEND noninteractive

ADD ./foreground.sh /etc/apache2/foreground.sh

RUN apt-get update && \
	apt-get dist-upgrade -y && \
	apt-get -y install mysql-client pwgen python-setuptools curl git unzip apache2 \
		php7.0 php7.0-gd libapache2-mod-php7.0 php7.0-cli php7.0-common php7.0-mbstring php7.0-intl php7.0-xml php7.0-mysql php7.0-mcrypt php7.0-zip \
		php7.0-soap postfix wget supervisor php7.0-pgsql curl libcurl3 \
		libcurl3-dev php7.0-curl php7.0-xmlrpc git-core && \
	cd /tmp && \
	rm /var/www/html/index.html && \
	chown -R www-data:www-data /var/www/html && \
	chmod +x /etc/apache2/foreground.sh

# Enable SSL, moodle requires it
RUN a2enmod ssl && a2ensite default-ssl # if using proxy, don't need actually secure connection

CMD ["/etc/apache2/foreground.sh"]

#RUN easy_install supervisor
#ADD ./start.sh /start.sh
#
#ADD ./supervisord.conf /etc/supervisord.conf
# RUN chmod 755 /start.sh /etc/apache2/foreground.sh
# EXPOSE 22 80
# CMD ["/bin/bash", "/start.sh"]

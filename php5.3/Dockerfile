FROM centos:6

WORKDIR /var/www/html
VOLUME /var/www/html


RUN yum install -y httpd \
	php \
	php-mysql

EXPOSE 80

#Config Apache2 Mod_Rewrite
ADD httpd/httpd.conf /etc/httpd/conf/
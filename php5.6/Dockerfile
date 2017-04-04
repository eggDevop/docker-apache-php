FROM centos:6

WORKDIR /var/www/html
VOLUME /var/www/html


RUN yum install -y wget \
	httpd \
	php \
	php-mysql

# Install php5.6
RUN wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm && rpm -Uvh epel-release-latest-6.noarch.rpm
RUN wget http://rpms.famillecollet.com/enterprise/remi-release-6.rpm && rpm -Uvh remi-release-6*.rpm

ADD yum_repo/remi.repo /etc/yum.repos.d/remi.repo

RUN yum -y upgrade php*


EXPOSE 80



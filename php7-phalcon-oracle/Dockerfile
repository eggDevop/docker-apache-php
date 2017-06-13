FROM debian:jessie

WORKDIR /var/www/html
VOLUME /var/www/html


#Install base debian
RUN apt-get update && apt-get install -y \
	wget \
	git \
	re2c \
	apt-utils \
	apt-transport-https \
	curl \
	vim \
	zip \
	lsb-release \ 
	build-essential 

RUN echo 'deb http://packages.dotdeb.org jessie all' > /etc/apt/sources.list.d/dotdeb.list \
    && wget https://www.dotdeb.org/dotdeb.gpg && apt-key add dotdeb.gpg  && rm dotdeb.gpg

RUN curl -s https://packagecloud.io/install/repositories/phalcon/stable/script.deb.sh | bash

RUN apt-get update && apt-get -y install \
	apache2 \
	php7.0 \
    libapache2-mod-php7.0 \
    php7.0-apcu \
    php7.0-apcu-bc \
    php7.0-imagick \
    php7.0-memcached \  
    php7.0-dev \      
    php7.0-mongodb \
    php7.0-readline \
    php7.0-xdebug \
	php7.0-cgi \ 
	php7.0-fpm \
	php7.0-mysql \
	php7.0-cli \        
	php7.0-json \      
	php7.0-odbc \     
	php7.0-redis \     
	php7.0-xsl \
	php7.0-common \
	php7.0-curl \
	php7.0-mcrypt \
	php7.0-zip \
	php7.0-phalcon

EXPOSE 80

# Install composer
RUN curl -sS --insecure https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

#install unitest
RUN wget https://phar.phpunit.de/phpunit-5.7.19.phar -O /usr/local/bin/phpunit && \
	chmod +x /usr/local/bin/phpunit

# Install Oracle Instantclient
RUN mkdir /opt/oracle && \
    cd /opt/oracle && \
    wget https://s3.amazonaws.com/merofile/instantclient-basic-linux.x64-12.1.0.2.0.zip && \
    wget https://s3.amazonaws.com/merofile/instantclient-sdk-linux.x64-12.1.0.2.0.zip && \
    unzip /opt/oracle/instantclient-basic-linux.x64-12.1.0.2.0.zip -d /opt/oracle && \
    unzip /opt/oracle/instantclient-sdk-linux.x64-12.1.0.2.0.zip -d /opt/oracle && \
    ln -s /opt/oracle/instantclient_12_1/libclntsh.so.12.1 /opt/oracle/instantclient_12_1/libclntsh.so && \
    ln -s /opt/oracle/instantclient_12_1/libclntshcore.so.12.1 /opt/oracle/instantclient_12_1/libclntshcore.so && \
    ln -s /opt/oracle/instantclient_12_1/libocci.so.12.1 /opt/oracle/instantclient_12_1/libocci.so && \
    rm -rf /opt/oracle/*.zip

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    echo 'instantclient,/opt/oracle/instantclient_12_1/' | pecl install oci8 && \
    docker-php-ext-configure pdo_oci --with-pdo-oci=instantclient,/opt/oracle/instantclient_12_1,12.1 && \
    docker-php-ext-enable oci8

# Config Apache2
RUN a2enmod rewrite

# Clear Trash
RUN rm -rf /usr/share/doc
RUN apt-get clean && apt-get autoclean

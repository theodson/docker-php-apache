FROM centos:6.9

ENV PHP_VERSION 5.3.3

RUN yum install -y \
        php \
        php-mbstring \
        php-pgsql \
        php-mysql \
        php-gd \
        php-cli \
        php-devel \ 
        php-pear \
        php-pdo \
        php-pgsql \
        php-sqlite \
        php-gd \
        php-intl \
        php-mbstring \
        php-process \
        php-mcrypt \
        php-xml \
        php-pecl-apc \
        php-pecl-amqp \
        php-pecl-json \
        php-pecl-jsonc \
        php-pecl-redis \
        php-pecl-ssh2 \
        git

# https://bugs.php.net/bug.php?id=63935
RUN ln -s /usr/lib64/libssl.so /usr/lib/libssl.so && \
    ln -s /usr/lib64/libcrypto.so /usr/lib/libcrypto.so 

RUN yum install -y \
    gcc gcc-c++ autoconf automake openssl-devel libssh2-devel && \
    pecl channel-update pecl.php.net && \
    yes "" | pear install VersionControl_GIT-alpha && \
    yes "" | pecl install ssh2 && \
    yes "" | pecl install stomp-1.0.9 && \
    echo "extension=stomp.so" > /etc/php.d/stomp.ini && \
    echo "extension=ssh2.so" > /etc/php.d/ssh2.ini && \
    echo "date.timezone = \"Australia/NSW\"" > /etc/php.d/custom.ini && \
    echo "max_execution_time = 1800" >> /etc/php.d/custom.ini && \
    echo "memory_limit = 512M" >> /etc/php.d/custom.ini && \    
    echo "upload_max_filesize = 4M" >> /etc/php.d/custom.ini         

RUN yum remove -y \
    gcc gcc-c++ autoconf automake openssl-devel libssh2-devel php-devel && \    
    yum clean all && \
    pecl clear-cache

RUN php -i && \
    php -m && \
    pecl list -a

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer    

CMD ["php", "-a"]
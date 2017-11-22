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
    php-pecl-ssh2 && \
    echo "# https://bugs.php.net/bug.php?id=63935 " && \
    ln -s /usr/lib64/libssl.so /usr/lib/libssl.so && \
    ln -s /usr/lib64/libcrypto.so /usr/lib/libcrypto.so && \
    echo "# https://unix.stackexchange.com/questions/90006/how-do-i-reduce-the-size-of-locale-archive " && \
    yum install -y \
    gcc gcc-c++ autoconf automake openssl-devel libssh2-devel && \
    pecl channel-update pecl.php.net && \
    yes "" | pear install VersionControl_GIT-alpha && \
    yes "" | pecl install ssh2 && \
    yes "" | pecl install stomp-1.0.9 && \
    echo "extension=stomp.so" > /etc/php.d/stomp.ini && \
    echo "extension=ssh2.so" > /etc/php.d/ssh2.ini && \
    echo "max_execution_time = 1800" >> /etc/php.d/custom.ini && \
    echo "memory_limit = 512M" >> /etc/php.d/custom.ini && \    
    echo "upload_max_filesize = 4M" >> /etc/php.d/custom.ini && \
    v=2.5.4 && \
    echo "Installation of git-$v started" && \
    yum install -y wget curl-devel expat-devel gettext-devel openssl-devel zlib-devel perl-ExtUtils-MakeMaker && \
    yum remove -y git && \
    pushd /usr/src  && \
    wget "https://www.kernel.org/pub/software/scm/git/git-$v.tar.gz"  && \
    tar -xvf "git-$v.tar.gz"  && \
    pushd "git-$v" && \
    make prefix=/usr/local/git all && \
    make prefix=/usr/local/git install && \
    echo "export PATH=\$PATH:/usr/local/git/bin" >> /etc/bashrc  && \
    echo "Installation of git-$v complete" && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer && \
    yum remove -y \
    gcc gcc-c++ wget curl-devel expat-devel autoconf automake openssl-devel libssh2-devel php-devel zlib-devel perl-ExtUtils-MakeMaker && \    
    yum clean all && \
    pecl clear-cache && \
    rm -rf /usr/src/* && \
    localedef --list-archive | grep -v -i ^en | xargs localedef --delete-from-archive && \ 
    mv -f /usr/lib/locale/locale-archive /usr/lib/locale/locale-archive.tmpl && \
    build-locale-archive 
    
CMD ["php", "-a"]
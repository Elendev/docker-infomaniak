FROM php:7.1-apache

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        git \
        unzip \
        libbz2-dev \
        libcurl3-dev \
        libxml2-dev \
        libssl-dev \
        libpng-dev \
        libgmp-dev \
        libc-client-dev \
        libkrb5-dev \
        libldap2-dev \
        libmcrypt-dev \
        unixodbc-dev \
        libpq-dev \
        libtidy-dev \
        libxml2-dev \
        libxslt1-dev \
    && rm -rf /var/lib/apt/lists/*


RUN docker-php-source extract; \
	{ \
		echo '# https://github.com/docker-library/php/issues/103#issuecomment-271413933'; \
		echo 'AC_DEFUN([PHP_ALWAYS_SHARED],[])dnl'; \
		echo; \
		cat /usr/src/php/ext/odbc/config.m4; \
	} > temp.m4; \
	mv temp.m4 /usr/src/php/ext/odbc/config.m4; \
	apk add --no-cache unixodbc-dev; \
	docker-php-ext-configure odbc --with-unixODBC=shared,/usr;

RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
    docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ && \
    CFLAGS="-I/usr/src/php" docker-php-ext-install \
        mysqli \
        pdo_mysql \
        bcmath \
        bz2 \
        calendar \
        ctype \
        curl \
        dom \
        exif \
        fileinfo \
        ftp \
        gd \
        gmp \
        iconv \
        imap \
        intl \
        json \
        ldap \
        mbstring \
        mcrypt \
        odbc \
        opcache \
        pdo \
        pgsql \
        session \
        simplexml \
        soap \
        tidy \
        xml \
        xmlreader \
        xmlrpc \
        xmlwriter \
        xsl \
        zip


RUN echo 'memory_limit = 640M' >> /usr/local/etc/php/php.ini && \
    echo 'post_max_size = 360M' >> /usr/local/etc/php/php.ini && \
    echo 'upload_max_filesize = 360M' >> /usr/local/etc/php/php.ini
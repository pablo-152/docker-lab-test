FROM php:7.4-apache

RUN apt-get update && apt-get install -y \
    gnupg \
    curl \
    apt-transport-https \
    unixodbc \
    unixodbc-dev \
    libgssapi-krb5-2 \
    autoconf \
    g++ \
    make \
    pkg-config \
    libtool \
    libtool-bin \
    build-essential \
    && rm -rf /var/lib/apt/lists/*


# Microsoft SQL Server Driver
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl https://packages.microsoft.com/config/debian/10/prod.list \
       > /etc/apt/sources.list.d/mssql-release.list \
    && apt-get update \
    && ACCEPT_EULA=Y apt-get install -y msodbcsql17 \
    && rm -rf /var/lib/apt/lists/*


# Extensiones MySQL
RUN docker-php-ext-install mysqli pdo pdo_mysql


# PECL
RUN pecl channel-update pecl.php.net


# Solución libtool/libltdl
RUN find /usr -name "libltdl.la" -delete \
    && ldconfig


# SQL Server PHP Driver
RUN pecl install sqlsrv-5.10.1 \
    && pecl install pdo_sqlsrv-5.10.1 \
    && docker-php-ext-enable sqlsrv pdo_sqlsrv


RUN a2enmod rewrite


WORKDIR /var/www/html
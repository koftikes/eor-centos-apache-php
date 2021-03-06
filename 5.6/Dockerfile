# =============================================================================
# cetres/eor-centos-apache-php
# CentOS-7, Apache 2.4, PHP 5.6
# =============================================================================
FROM centos:centos7
MAINTAINER Konstantin Litvinov <koftikes@gmail.com>

RUN yum -y -q --setopt=tsflags=nodocs --nogpgcheck update > /dev/null && \
    yum -y -q --setopt=tsflags=nodocs --nogpgcheck install wget mc unzip > /dev/null && \
    wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm 2> /dev/null && \
    wget https://rpms.remirepo.net/enterprise/remi-release-7.rpm 2> /dev/null && \
    yum -y -q install remi-release-7.rpm epel-release-latest-7.noarch.rpm 2> /dev/null && \
    yum-config-manager -y -q --enable remi-php56 > /dev/null && \
    yum -y -q --setopt=tsflags=nodocs --nogpgcheck install \
    httpd \
    php \
    php-cli \
    php-common \
    php-devel \
    php-mysqlnd \
    php-pgsql \
    php-mcrypt \
    php-mbstring \
    php-soap \
    php-gd \
    php-ldap \
    php-pear \
    php-pdo \
    php-intl \
    php-xml \
    php-zip \
    php-pecl-xdebug \
    libaio > /dev/null && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer > /dev/null && \
    yum clean all && rm -rf /var/cache/yum && rm -f /etc/httpd/conf.d/{userdir.conf,welcome.conf} && \
    chmod -R g+w /var/www/html && mkdir -p /var/xdebug/profiler && chmod -R 777 /var/xdebug && \
    touch /tmp/xdebug.log && chmod 666 /tmp/xdebug.log

# -----------------------------------------------------------------------------
# Project settings
# -----------------------------------------------------------------------------
COPY ./dist/httpd.local.conf /etc/httpd/conf.d/httpd.local.conf
COPY ./dist/web.php.ini /etc/php.d/web.php.ini

# -----------------------------------------------------------------------------
# Set ports and env variable HOME
# -----------------------------------------------------------------------------
EXPOSE 80
WORKDIR /var/www/html

# -----------------------------------------------------------------------------
# Start
# -----------------------------------------------------------------------------
CMD ["/usr/sbin/httpd", "-DFOREGROUND"]

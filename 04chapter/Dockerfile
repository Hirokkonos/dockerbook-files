FROM amazonlinux:2.0.20181114

## Repository mainline of nginx 1.15
ADD nginx/nginx.repo /etc/yum.repos.d/nginx.repo

## Install Packages
RUN yum update -y
RUN yum --enablerepo=nginx install -y nginx 
RUN yum install -y zip \
                   procps \
                   iputils \
                   awscli \
                   unzip \
                   libtool-ltdl \
                   libtool \
                   libXpm \
                   mysql \
                   ncurses-compat-libs \
                   httpd \
                   libtiff \
                   autoconf \
                   gcc \
                   gcc-c++ \
                   awslogs \
                   automake \
                   git \
                   systemd-sysv \
                   libxslt \
                   openssl-devel \
                   libxml2-devel \
                   libedit-devel \
                   https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
                   http://rpms.famillecollet.com/enterprise/remi-release-7.rpm

RUN yum install -y --enablerepo=amzn2-core gd-last
RUN yum install -y supervisor
## Install PHP7.2
RUN yum install --enablerepo=remi-php72 --disablerepo=amzn2-core -y php \
                                           php-fpm \
                                           php-devel \
                                           php-mbstring \
                                           php-pdo \
                                           php-mysqlnd \
                                           php-gd \
                                           php-xml \
                                           php-mcrypt

## Modify TimeZone 
RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
## Add nginx settings
ADD nginx/nginx.conf /etc/nginx/nginx.conf
ADD nginx/default.conf /etc/nginx/conf.d/default.conf

## ADD php-fpm config
ADD php-fpm/php.ini /etc/php.ini
ADD php-fpm/php-fpm.conf /etc/php-fpm.conf
ADD php-fpm/www.conf /etc/php-fpm.d/www.conf

ADD nginx/info.php /var/www/html/info.php
## Add supervisor
ADD supervisor/supervisord.conf /etc/supervisord.d/supervisord.conf
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.d/supervisord.conf"]

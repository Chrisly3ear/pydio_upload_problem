FROM php:7.1-apache
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libldap2-dev \
        cifs-utils \
        wget \
        zip \
    && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install ldap \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd
#   docker-php-ext-install pdo 
RUN docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli
    # && docker-php-ext-install mysql 

#Enable Mods
RUN a2enmod \
    actions \
    asis \
    authz_groupfile \
    cgi \
    expires \
    include \
    mpm_prefork \
    proxy \
    proxy_http \
    rewrite \
    socache_shmcb \
    ssl

# Local Network Shares. Won't start if they aren't available!
# RUN mkdir -p /mnt/production \
#     && mkdir -p /mnt/archive \
#     && mkdir -p /mnt/hpbackup \
#     && mkdir -p /mnt/projects \
#     && echo '# Netzwork Mounts' >> /etc/fstab \
#     && echo '//SOME_SHARE_1 /mnt/hpbackup   cifs  uid=33,gid=33,file_mode=0777,dir_mode=0777,username=USERNAME_REMOVED,password=PASSWROD_REMOVED,domain=DOMAIN_REMOVED,_netdev  0       0' >> /etc/fstab \
#     && echo '//SOME_SHARE_2 /mnt/projects   cifs  uid=33,gid=33,file_mode=0777,dir_mode=0777,username=USERNAME_REMOVED,password=PASSWROD_REMOVED,domain=DOMAIN_REMOVED,_netdev  0       0' >> /etc/fstab \
#     && echo '//SOME_SHARE_3 /mnt/production cifs  uid=33,gid=33,file_mode=0777,dir_mode=0777,username=USERNAME_REMOVED,password=PASSWROD_REMOVED,domain=DOMAIN_REMOVED,_netdev  0       0' >> /etc/fstab \
#     && echo '//SOME_SHARE_4 /mnt/archive    cifs  uid=33,gid=33,file_mode=0777,dir_mode=0777,username=USERNAME_REMOVED,password=PASSWROD_REMOVED,domain=DOMAIN_REMOVED,_netdev  0       0' >> /etc/fstab

RUN wget https://download.pydio.com/pub/core/archives/pydio-core-8.0.2.zip -O /tmp/pydio.zip && \
    unzip /tmp/pydio.zip  -x "*/.gitignore" -d /tmp/ && \
    cp -rf /tmp/pydio-core-*/. /var/www/html/

COPY php.ini /usr/local/etc/php/
COPY pydio.conf /etc/apache2/sites-enabled/00_pydio.conf

# Certificates and Key NOT included in Github Repo!!
# COPY certs /etc/ssl/servercerts
# COPY private_key /etc/ssl/private


RUN chown -R 33:33 ./

EXPOSE 80

CMD ["apache2-foreground"]




FROM mariadb

COPY etc_my.cnf.d /etc/my.cnf.d
COPY msql_config /etc/mysql/conf.d
RUN  mkdir -p /var/lib/mysql-files && \
     chown -R 33:33 /var/lib/mysql-files

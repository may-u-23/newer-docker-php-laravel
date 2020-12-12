FROM mysql:8.0.22
# https://hub.docker.com/_/mysql?tab=tags&page=1&ordering=last_updated

ENV MYSQL_DATABASE=laravel_local \
  MYSQL_USER=phper \
  MYSQL_PASSWORD=secret \
  MYSQL_ROOT_PASSWORD=secret \
  TZ=Asia/Tokyo

# Windows環境でボリュームマウント時のパーミッション777問題対策
COPY ./my.cnf /etc/mysql/conf.d/my.cnf
RUN chmod 644 /etc/mysql/conf.d/my.cnf
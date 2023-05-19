FROM debian:10-slim

LABEL maintainer="Madev"
LABEL description="XtraBackup based MySQL / MariaDB backup docker image to create incremental backups periodically"

# installing xtrabackup according to https://docs.percona.com/percona-xtrabackup/2.4/installation/apt_repo.html

RUN . /etc/os-release \
    && apt-get update \
    && apt-get -y install wget lsb-release gnupg2 cron curl \
    && rm -rf /etc/cron.* \
    && . /etc/os-release

RUN apt-get update \
    && wget https://repo.percona.com/apt/percona-release_latest.$(lsb_release -sc)_all.deb \
    && dpkg -i percona-release_latest.$(lsb_release -sc)_all.deb \
    && apt-get update \
    && apt-get -y install percona-xtrabackup-24 qpress \ 
    && percona-release enable-only tools release
    

ADD scripts /scripts

VOLUME /backup /var/lib/mysql
WORKDIR /backup

CMD ["/scripts/start.sh"]
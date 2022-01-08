FROM debian:bullseye

ENV MANTIS_VER 2.25.2
ENV MANTIS_SHA512 f8e1da19f86d7aea567f6aedbd08ad3470a47bdd7432dc60276d2f41a30683f6323c85b5eb8acb2dd13e8283bb7ddebb4a616fad2b1e67c145f86cb8c7319d43
ENV MANTIS_URL https://downloads.sourceforge.net/project/mantisbt/mantis-stable/${MANTIS_VER}/mantisbt-${MANTIS_VER}.tar.gz
ENV MANTIS_FILE mantisbt.tar.gz

RUN apt-get update && \ 
    apt-get -y install apache2 \
    php7.4 \
    libapache2-mod-php7.4 \
    php7.4-json \
    php7.4-mysql \
    php7.4-pdo \
    php7.4-cli \
    php7.4-mbstring \
    curl

RUN set -xe \
    && curl -fSL ${MANTIS_URL} -o ${MANTIS_FILE} \
    && sha512sum ${MANTIS_FILE} \
    && echo "${MANTIS_SHA512}  ${MANTIS_FILE}" | sha512sum -c \
    && tar xvfz ${MANTIS_FILE} \
    && mv mantisbt-${MANTIS_VER} /opt/mantisbt \
    && chown -R www-data:www-data /opt/mantisbt \
    && ln -s  /opt/mantisbt /var/www/html \
    && mkdir -p /var/mantisbt \
    && chown -R www-data:www-data /var/mantisbt

VOLUME ["/var/mantisbt","/opt/mantisbt"]
CMD ["apachectl", "-D", "FOREGROUND"]
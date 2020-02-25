FROM phpdockerio/php56-fpm:latest
WORKDIR "/application"

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install  php5-mysql php5-intl php5-ldap php5-odbc php5-xdebug\
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

#install odbc driver
RUN apt-get update && apt-get -y install unixodbc-dev libmyodbc
RUN apt-get -f install

COPY ibm-iaccess-1.1.0.4-1.0.amd64.deb /tmp/ibm-iaccess-1.1.0.4-1.0.amd64.deb
ENV ODBCINI=/etc/odbc.ini
ENV LD_LIBRARY_PATH=/opt/ibm/iSeriesAccess/lib64/

RUN dpkg -i /tmp/ibm-iaccess-1.1.0.4-1.0.amd64.deb

COPY sqlodbc.log sqlodbc.log
COPY odbc.ini /etc/odbc.ini
COPY odbcinst.ini /etc/odbcinst.ini

RUN echo "/opt/ibm/iSeriesAccess/lib64" > /etc/ld.so.conf.d/iSeriesAccess.conf
RUN rm /usr/lib/x86_64-linux-gnu/libodbcinst.so.2
RUN ln -s /usr/lib/x86_64-linux-gnu/libodbcinst.so.1 /usr/lib/x86_64-linux-gnu/libodbcinst.so.2
RUN /sbin/ldconfig
RUN ldd /opt/ibm/iSeriesAccess/lib64/libcwbodbc.so

ADD xdebug.ini /etc/php5/cli/conf.d/20-xdebug.ini
ADD xdebug.ini /etc/php5/fpm/conf.d/20-xdebug.ini


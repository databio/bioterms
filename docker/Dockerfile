FROM httpd:2.4-alpine
RUN mkdir /usr/local/apache2/htdocs/schemas
COPY ./schemas/ /usr/local/apache2/htdocs/schemas/
COPY ./apache_conf/httpd.conf /usr/local/apache2/conf/httpd.conf
COPY ./contents/* /usr/local/apache2/htdocs/

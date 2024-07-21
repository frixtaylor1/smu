FROM httpd:2.4

RUN apt-get update && apt-get install -y curl

# Copia el archivo de configuración
COPY ./config/load-balancer.conf /usr/local/apache2/conf/httpd.conf

# Habilita módulos necesarios
RUN sed -i '/^#LoadModule socache_shmcb_module modules\/mod_socache_shmcb.so/s/^#//' /usr/local/apache2/conf/httpd.conf \
    && sed -i '/^#LoadModule slotmem_shm_module modules\/mod_slotmem_shm.so/s/^#//' /usr/local/apache2/conf/httpd.conf \
    && sed -i '/^#LoadModule ssl_module modules\/mod_ssl.so/s/^#//' /usr/local/apache2/conf/httpd.conf

# Crea directorios y establece permisos
RUN mkdir -p /usr/local/apache2/logs && \
    chown -R www-data:www-data /usr/local/apache2/logs

# Copia los certificados
COPY ./certs/server.key /usr/local/apache2/conf/server.key
COPY ./certs/server.crt /usr/local/apache2/conf/server.crt

# Establece permisos para los certificados y configuración
RUN chmod 644 /usr/local/apache2/conf/server.key /usr/local/apache2/conf/server.crt
RUN chmod -R 755 /usr/local/apache2/logs
RUN chmod 644 /usr/local/apache2/conf/httpd.conf

EXPOSE 8080 8443 80 443
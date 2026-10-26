# Imagen de Apache basada en Ubuntu
FROM ubuntu/apache2

#Comando para cambiar el puerto por defecto a uno inteno personalizado
RUN sed -i 's/Listen 80/Listen 8093/' /etc/apache2/ports.conf

#Copia los archivos de configuración de Virtual Hosts desde el host al contenedor
COPY ./apache/sites-available/ /etc/apache2/sites-available/

# Apagar la página web por defecto de Ubuntu/Apache
RUN a2dissite 000-default.conf

## Habilita automáticamente tus Virtual Hosts personalizados de NimbusDocs
RUN a2ensite 000-default.conf infoweb.conf infonet.conf


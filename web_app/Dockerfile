FROM php:7.4-apache

# Instalar la extensión mysqli
RUN docker-php-ext-install mysqli

# Copiar los archivos PHP a la carpeta web del contenedor
COPY . /var/www/html/

# Exponer el puerto 80
EXPOSE 80

# Mantener Apache en primer plano
CMD ["apache2-foreground"]

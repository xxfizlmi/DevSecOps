FROM php:8.0-apache

# Instal ekstensi mysqli
RUN docker-php-ext-install mysqli

# Copy file aplikasi ke dalam container
COPY index.php /var/www/html/

# Ekspose port 80 untuk server Apache
EXPOSE 80

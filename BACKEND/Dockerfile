# Utiliser une image de base PHP avec Apache
FROM php:8.1-apache

# Définir le répertoire de travail
WORKDIR /var/www/html

# Copier le contenu de votre projet dans le conteneur
COPY . .

# Installer les dépendances via Composer
RUN apt-get update && \
    apt-get install -y libzip-dev unzip apt-utils && \
    docker-php-ext-install zip && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Changer les permissions du répertoire de travail
RUN chown -R www-data:www-data /var/www/html && chmod -R 755 /var/www/html

# Exécuter Composer en tant qu'utilisateur www-data pour éviter les problèmes de permission
USER www-data

# Installer les dépendances Composer et vérifier l'installation
RUN composer install --prefer-dist --no-interaction && \
    ls -al /var/www/html/vendor/symfony/polyfill-php80/ && \
    ls -al /var/www/html/vendor/symfony/polyfill-php80/Resources

# Revenir à l'utilisateur root pour la suite des opérations
USER root

# Exposer le port 80
EXPOSE 80

# Démarrer Apache
CMD ["apache2-foreground"]

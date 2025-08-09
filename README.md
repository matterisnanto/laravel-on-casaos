# laravel-on-casaos
Cara deploy laravel di casaos

* Masuk ke docker menggunakan terminal casaos atau melalui aplikasi putty
docker exec -it laravel-web bash

* Install package dan composer
apt update && apt install -y libzip-dev libpng-dev libonig-dev libxml2-dev zip unzip nano git
docker-php-ext-install pdo pdo_mysql zip gd mbstring exif pcntl bcmath intl
curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

* Jalankan composer install
composer install

* Ubah isi /etc/apache2/sites-available/000-default.conf
nano /etc/apache2/sites-available/000-default.conf

* Hapus semua isinya dan ubah dengan kode ini:
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/public
   
    <Directory /var/www/html/public>
        AllowOverride All
        Require all granted
    </Directory>
   
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>


* Install nodejs & npm (sesuai dengan versi yang digunakan di laravel)
apt install -y nodejs npm

* Jalankan npm install
Npm install

* Aktifkan mod rewrite
a2enmod rewrite

* Restart Apache
service apache2 restart

jangan lupa setting .env
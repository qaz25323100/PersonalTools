## Laravel(build in docker apache)  
  
  apt install zip unzip  
  apt-get install libzip-dev  
  docker-php-ext-install zip  
  docker-php-ext-install mysqli pdo pdo_mysql  
  service apache2 restart  

  sudo chown -R www-data:www-data xxxxxxxxxx/  
  composer install  
  php artisan key:generate  

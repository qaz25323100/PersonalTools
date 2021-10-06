## Laravel(build in docker apache)  
  
  ### Enable zlib Library  
    
  apt install zip unzip  
  apt-get install libzip-dev  
  docker-php-ext-install zip  
  
  ### Enable mysql library  
    
  docker-php-ext-install mysqli pdo pdo_mysql  
  
  ### Enable Rewrite module
  a2enmod rewrite
  service apache2 restart  

  ### Laravel Projoect initial  
    
  sudo chown -R www-data:www-data xxxxxxxxxx/  
  composer install  
  php artisan key:generate  

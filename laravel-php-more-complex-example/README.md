docker-compose run --rm composer create-project --prefer-dist laravel/laravel .</br>
docker-compose up -d server php mysql</br>
docker-compose run --rm artisan migrate
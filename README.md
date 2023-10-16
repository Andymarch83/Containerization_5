# Containerization_5

подробно разобранный docker-compose.yml файл:

# Указываем версию синтаксиса файла docker-compose

version: '3.1'

# Описываем сервисы, которые будут запущены

services:

  # Первый сервис: MySQL сервер
  
  some-mysql:
  
    # Используемый Docker образ
    
    image: mysql:8.0.31
    
    # Переменные окружения для MySQL
    
    environment:
    
      MYSQL_ROOT_PASSWORD: my-secret-pw


  # Второй сервис: phpMyAdmin
  
  myphp:
  
    # Используемый Docker образ
    
    image: phpmyadmin/phpmyadmin
    
    # Проброс портов: хост:контейнер
    
    ports:
    
      - 8081:80
      
    # Указываем зависимость от MySQL сервиса
    
    depends_on:
    
      - some-mysql
      
    # Переменные окружения для phpMyAdmin
    
    environment:
    
      PMA_HOST: some-mysql

# Описываем тома

volumes:

  mysql_data:
  
Пояснение:

version: Указывает версию синтаксиса файла docker-compose. Это нужно для корректного чтения файла Docker Compose.

services: Секция, в которой определяются все контейнеры, которые должны быть запущены.

some-mysql: Имя первого сервиса, запускающего MySQL.

image: Docker образ, который будет использован для этого контейнера.

environment: Переменные окружения для контейнера. В данном случае, устанавливаем пароль root пользователя MySQL.

volumes: Здесь мы монтируем том для сохранения данных MySQL. Это нужно для сохранения данных между перезапусками контейнера.

myphp: Имя второго сервиса, запускающего phpMyAdmin.

depends_on: Указывает, что данный сервис зависит от some-mysql, и нужно сначала его запустить.

PMA_HOST: Указывает на имя хоста MySQL сервера, к которому должен подключиться phpMyAdmin. Здесь это имя сервиса some-mysql.

volumes: В этой секции описываются тома, которые будут использованы. В данном случае, это mysql_data для MySQL.

Этот файл делает то же, что и команды docker run, но в более удобном и управляемом формате.

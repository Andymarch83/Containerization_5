# Урок 5. Docker Compose и Docker Swarm

1) создать сервис, состоящий из 2 различных контейнеров: 1 - веб, 2 - БД (compose)

2)  Задание со звездочкой - повышенной сложности..
** не обязательно 2) необходимо создать 3 сервиса в каждом окружении (dev, prod, lab)
** не обязательно 3) по итогу на каждой ноде должно быть по 2 работающих контейнера

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


![Home5](https://github.com/Andymarch83/Containerization_5/assets/122732408/8505e71f-c256-46d4-93c3-4744ddb735bb)

![Home5 1](https://github.com/Andymarch83/Containerization_5/assets/122732408/b72fc68f-243a-4f9a-82cf-95d39d4a05da)

![Home5 1 2](https://github.com/Andymarch83/Containerization_5/assets/122732408/e3db8f4c-93a0-45fe-a566-7f940f6e4cdd)

![Home5 2](https://github.com/Andymarch83/Containerization_5/assets/122732408/76f933b6-4b37-4731-a339-d9c3dc8000a7)



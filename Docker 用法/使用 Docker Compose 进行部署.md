## 案例一 整套项目打包部署
- 直接将文件 docker-compose 放入 /usr/local/bin/ 下（记得赋予执行权限）
学会写yaml配置文件
  ```
  version: '3'
  services:
    nginx:
      hostname: nginx
      build:
        context: ./nginx
        dockerfile: Dockerfile
      ports:
        - 80:80
      networks:
        - lnmp
      volumes:
        - ./nginx/php.conf:/usr/local/nginx/conf/vhost/php.conf
        - ./wwwroot:/usr/local/nginx/html

    php:
      hostname: php
      build:
        context: ./php
        dockerfile: Dockerfile
      networks:
        - lnmp
      volumes:
        - ./wwwroot:/usr/local/nginx/html

    mysql:
      hostname: mysql
      image: mysql:5.7
      ports:
        - 3306:3306
      networks:
        - lnmp
      volumes:
        - ./mysql/conf:/etc/mysql/conf.d
        - ./mysql/data:/var/lib/mysql
      command: --character-set-server=utf8
      environment:
        MYSQL_ROOT_PASSWORD: 123456
        MYSQL_DATABASE: test 
        MYSQL_USER: user
        MYSQL_PASSWORD: user123456 

  networks:
    lnmp: {} 

  ```
- 配置文件常用字段

- docker-compose 常用命令

- 案例：一键部署LNMP网站平台

- compose_lnmp 文件夹的目录结构：
  - mysql
      - conf
          - my.cnf
      - date
  - nginx
      - Dockerfile
      - nginx.conf
      - nginx-1.15.5.tar.gz
      - php.conf
  - php
      - Docker
      - php
      - php-5.6.36.tar.gz
      - php-fpm.conf
  - wwwroot
  - index.php
  - docker-compose.yaml

- 构建命令：`docker-compose -f docker-compose.yml up`
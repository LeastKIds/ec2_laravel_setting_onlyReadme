# ec2_laravel_setting_onlyReadme

1. Php 7.3 버전 이상으로 설치

   - sudo amazon-linux-extras | grep php
   - sudo amazon-linux-extras install php7.4
   - sudo amazon-linux-extras enable php7.4
   - sudo yum install  php-cli php-common php-gd php-mbstring  php-mysqlnd php-pdo php-fpm php-xml php-opcache php-zip php-bcmath

2. composer install

   - sudo curl -sS https://getcomposer.org/installer | sudo php
   - sudo mv composer.phar /usr/local/bin/composer
   - sudo ln -s /usr/local/bin/composer /usr/bin/composer

3. node.js

   - sudo **curl** -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
   - sudo . ~/.nvm/nvm.sh
   - sudo **nvm** install node

4. mysql

   - sudo yum install https:**//dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm**
   - sudo yum install mysql-community-server
   - sudo systemctl start mysqld
   - sudo systemctl status mysqld
   - sudo grep 'temporary password' /var/log/mysqld.log (초기 비밀번호)
   - sudo mysql_secure_installation -p'[비밀번호]'
   - mysql 8 user create
     - create` `user` `계정ID@``'%'` `identified ``by` `'계정비밀번호'` `;
     - grant all privileges on DB이름.* to 계정ID@'%' with grant option;
     - flush privileges;
   - create database
     - CREATE DATABASE 테이블이름

5. Git

   - sudo yum install git -y 

6. php-fpm 설정

   - cd /etc/php-fpm.d

   - Sudo vi www.conf

   - ```shell
     # 24행
     - user = apache
     + user = nginx
     - group = apache
     + group = nginx
     
     # 38행
     - listen = 127.0.0.1:9000
     + listen = /var/run/php-fpm/php-fpm.sock
     
     # 48행
     - ;listen.owner = nobody
     - ;listen.group = nobody
     - ;listen.mode = 0660
     + listen.owner = nginx
     + listen.group = nginx
     + listen.mode = 0660
     ```

   - ```shell
     sudo systemctl restart php-fpm
     $ cd /var/run/php-fpm/
     $ ls
     php-fpm.pid  php-fpm.sock
     ```

7. nginx 서버 설정 (laravel)

   - ```shell
     $ sudo vi /etc/nginx/conf.d/exemple.com.conf
     
     server {
     	listen 8000; # api포트는 8000번 포트로
     	listen [::]:8000;
     	
     	root /home/ec2-user/laravel_vue_project/laravel/public; # laravel public 주소
     	index index.php, index.html, index.htm; # public 폴더 안에 읽어오는 파일 확장자
     	
     	server_name 아이피주소;
     	
     	location / {
     		try_files $uri $uri/ /index.php?$query_string;
     	}
     	
     	location ~ \.php$ {
     		try_files $uri /index.php =404;
     		fastcgi_split_path_info ^(.+\.php)(/.+)$;
     		fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
     		fastcgi_index index.php;
     		fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
     		include fastcgi_params;
     	}
     }
     ```

   - Nginx 멀티 서버 설정(vue)

- 최초로 받기
  - 원하는 폴더 이동
  - git clone (주소)
  - Laravel 폴더로 이동해서 .env.example 파일을 복사본을 만들어서 .env 파일로 만듬
  - .env 파일 안에서 기초 설정 하기
  - laravel 폴더에서 composer install 실행
  - laravel 폴더에서 npm install 실행
  - laravel 폴더에서 php artisan key:generate 실행
  - laravel 폴더에서 php artisan migrate 실행
  - 그 다음은 php 서버를 키든가 하면 됨
  - Vue 폴더에서도 npm install 실행
  - 그 뒤로 뷰 서버를 열든가 하면 됨
- 두 번째 부터
  - 작업 하기 전에 git pull
  - Laravel 폴더에서 php artisan migrate 실행
  - laravel 폴더에서 npm install 실행
  - vue 폴더에서 npm install 실행
  - 작업을 하고 난 뒤 마스터 브랜치로 커밋하기
  - 커밋은 '이름: 내용'으로 한글로 작성하기
    - ex) 김진홍: README 파일 수정
  - git push origin master 로 푸시하기









# ubuntu 버전

sudo apt update

sudo apt upgrade



1. Nginx 설치
   1. sudo apt-**get** install nginx
   
2. Php 설치
   1. sudo apt-get install php7.4
   2. sudo apt install php-fpm
   3. sudo apt install php-mysql php-zip php-gd
   4. sudo apt install php-mbstring php-xml
   5. sudo apt-get install php-curl
   
3. Git 설치
   1. sudo apt-**get** install git
   
4. composer 설치
   1. curl -sS https://getcomposer.org/installer | php
   2. sudo mv composer.phar /usr/local/bin/composer
   3. chmod +x /usr/local/bin/composer
   
5. Nodes 설치
   1. sudo apt-get install curl
   2. curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
   3. sudo apt-get install -y nodejs
   4. sudo apt-get install build-essential
   
6. Mysql 설치
   1. sudo apt-get install mysql-server
   2. sudo systemctl start mysql
   3. sudo systemctl enable mysql
   4. sudo mysql -u root -p(비밀번호는 없거나, root)
   5. create user 'voca'@'%' identified by 'voca';
   6. grant all privileges on *.* to 'voca'@'%' with grant option;
   7. flush privileges;
   8. create database vocabulary;
   
7. apach 삭제
   1. sudo service apache2 stop
   2. sudo apt-get remove apache2*
   3. sudo apt-get --purge remove apache2*
   4. sudo apt-get autoremove
   5. sudo service apache-htcacheclean stop (오류 떠도 넘어가셈)
   6. sudo apt-get --purge remove apache* 
   7. sudo apt-get autoremove
   
7. git 으로 clone 하기
   
   1. cd
   2. git clone 주소
   3. cd ./라라벨폴더
   4. cp .env.exemple .env
   5. .env 파일 수정
   6. composer update
   7. composer install
   8. npm install
   9. npm run dev
   10. php artisan key:generate
   11. php artisan migrate
   
9. nginx 설정

   1. cd /etc/nginx/sites-available
   2. https://laravel.kr/docs/8.x/deployment
      1. 여기서 server_name [ec2 아이피]
      2. root [자기 라라벨 public 폴더 경로]
   3. sudo systemctl restart nginx

10. 권한 설정(만약 권한 문제 생기면)

   1. 라라벨 폴더로 이동

   2. mkdir -p bootstrap/cache

   3. chown -R www-data:www-data bootstrap/cache 

   4. mkdir -p storage/logs

   5. mkdir -p storage/framework/cache 

   6. mkdir -p storage/framework/sessions

   7. mkdir -p storage/framework/views 

   8. chown -R www-data:www-data storage

      

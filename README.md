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
5. Git
   - sudo yum install git -y 



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


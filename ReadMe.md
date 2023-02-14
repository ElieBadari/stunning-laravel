# Project 1 : Deploying a Laravel Project : findings and answers 
### IP Address for the deployed laravel project : http://46.101.176.182/ 
## Q/A
#### question1 : what is sudo and why is it used?
>'sudo' is short for 'superuser do' and is used to run commands as the superuse/root user. This means the commands are run by a user that has unrestricted access to all files and directories. A superuser can perform any actions that are possible on the system.
sudo is used to elevate privaleges which is beneficial because things like installing software or modifying system files require elevated privaleges. 
#### question2 : what is apt-get and why is it used?
>'apt-get' is cli utility used to manage pacakges. Its uses are, but not limited to, installing, removing and upgrading software pacakges.
'apt-get' and 'sudo' work well together since 'apt-get' usually requires superuser privaleges to run.
#### question3 : fix this command 'curl -sS https://getcomposer.org/installer | sudo php — — install-dir=/usr/local/bin — filename=comp'
>the problem with the above command is the format of the dashes, they should be repalced with two small dashes.
#### question4 : 'Create a file called .env which is a copy of .env.example. Which command did you use?' 
>cp .env.example .env
#### question5 : what does 'sudo chgrp -R www-data storage bootstrap/cache' mean ?
>The command 'sudo chgrp -R www-data storage bootstrap/cache' changes the group ownership of the storage and bootstrap/cache directories and all their contents recursively (-R) to the www-data group. The chgrp command is used to change the group ownership of files and directories.
#### question6 : what does 'sudo chmod -R ug+rwx storage bootstrap/cache' mean ?
>The command 'sudo chmod -R ug+rwx storage bootstrap/cache' modifies the permissions of the storage and bootstrap/cache directories and all their contents recursively (-R) to add read, write, and execute permissions (ug+rwx) for the user and group (ug) that own the directories.
## Findings : how to deploy the laravel website
#### connecting to the server and installing dependancies (using windows, puTTy)
> the following steps are after connected to the server and having the project ready for deployment 
>- sudo apt-get install apache2 
>- sudo apt-get install mysql-server
>- sudo apt-get install php
>- sudo apt-get install php-mysql
>- sudo apt-get install libapache2-mod-php
>- sudo apt-get install php-pear
>- sudo apt-get install curl
>- sudo apt-get install php-curl
>- sudo apt-get install php-cli
>- sudo apt-get install git
>- a2enmod rewrite
>- systemctl restart apache2
#### clone your project into /var/www/html 
>- cd ../var/www/htmll
>- git clone < link to repo >
#### install composer
>- curl -sS https://getcomposer.org/installer  | sudo php -- --install-dir=/usr/local/bin --filename=composer
>- composer install
#### create .env and generate key 
>- cp .env.example .env
>- vim .env
>> once inside vim (to modify the app name)
>>- i (insert)
>>- :x (save and exit)
>- php artisan key:generate
#### configure apache 
>- cd ../etc/apache2
>- vim apache2.conf
>> once inside vim (to modify the apache config directory)
>>- i
>>- :x
>- cd sites-enables
>- vim 000-default.conf
>> once inside vim (modify document root)
>>- i
>>- :x
>- systemctl restart apache2
#### setting folder rights 
>- sudo chgrp -R www-data storage bootstrap/cache
>- sudo chmod -R ug+rwx storage bootstrap/cache

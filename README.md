# spurt-commerce

## Node Js Installation (Version — 14.x)
* The Back-end API of Spurtcommerce is on NodeJS (v.14.x). 
```
 curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
```
```
 sudo apt-get install -y nodejs
```
```
 sudo apt-get install -y build-essential
```
* some of the additional dependencies software are required for Spurtcommerce
```
 sudo npm install forever -g
```
```
 sudo npm install apidoc -g
```

## Apache Installation
* Spurtcommerce deployment requires one of the web servers.
```
 sudo apt update
```
```
 sudo apt install apache2 -y
```
* you have to enable additional apache modules for Spurtcommerce deployment.
```
 sudo a2enmod proxy
```
```
 sudo a2enmod proxy_http
```
```
 sudo a2enmod headers
```
```
 sudo systemctl restart apache2
```
* Reverse Proxy Configuration of apache2 webserver.
```
  sudo nano /etc/apache2/sites-available/000-default.conf 
```
   — Add This Code in the above default.conf file
```
  ProxyRequests off

  <Proxy *>

        Order deny,allow

        Allow from all

  </Proxy>


  <Location /backend>

         ProxyPass http://127.0.0.1:8000
         ProxyPassReverse http://127.0.0.1:8000

  </Location>
  ```
  
## Mysql Installation
* To install MySQL database to deploy Spurtcommerce
```
sudo apt-get install mysql-server -y
```
```
sudo mysql -u root
```
* You have to create a password for the default root user using below commands
```
 SELECT User, Host, plugin FROM mysql.user;
```
```
 ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '<PASSWORD>';
```
```
 FLUSH PRIVILEGES;
```
### Creating Database for Spurtcommerce
```
 create database spurtcommerce;
```
```
 exit;
 ```
* import your sql file and set your root (do this where the file spurtcommerce.sql is present )
```
sudo mysql -u root
```
```
  mysql> sudo mysql -u root -p spurtcommerce < spurtcommerce.sql  
```
```
exit
```

## Imagemagick Installation
* We can install Imagemagick with the following commands;
```
sudo apt update
```
```
sudo apt install imagemagick
```
## Angular Installation
* The Front End of Spurtcommerce Application is built on Angular framework. By using the following command, you can install Angular in your server.
```
sudo npm install -g @angular/cli -y
```
# Application Setup

## Back End API Setup

## Downloading SpurtCommerce Zip file

* Downloading spurtcommerce from git hub using the below command in server root (/home/ubuntu)
```
git clone https://github.com/sanjayreddyg/spurt-commerce/raw/main/Spurtcommerce_3.0.2_community_LTS.zip
```
* Install Unzip using the following command
```
sudo apt install unzip -y
```
* Unzipping spurtcommerce zip file
```
unzip Spurtcommerce.zip
```
* In api folder change 'bcrypt':'3.0.1' to 'bcrypt':'5.0.1' in a file package.json

* Provide database name and password in " .env.production " and " .env " file in api folder.

* Installing dependencies based on package.json in server location (like spurtcommerce/api/)
```
npm install
```
```
npm install typeorm-seeding@1.0.0-beta.6
```
* To Build app 
```
npm run build
```
* Running Api in Backgroung forever
```
sudo NODE_ENV=production forever start dist/app.js
```
* After api running successfully, open browser and give 
```
http://public ip address/backend/apidoc/ 
```
 
## Front End Store Setup
* upload the environment url in the server location (like /home/ubuntu/spurtcommerce/store/src/environments)

* Provide store_url & image_url in " environments.ts " and " environments.prod.ts " file.
```
'StoreUrl': 'http://127.0.0.1/backend/api/'
'ImageUrl': 'http://127.0.0.1/backend/api/media/image-resize/'
```
* Installing dependencies based on package.json in server location (like spurtcommerce/store/)
```
npm install
```
* To Build app 
```
npm run build
```
* After  Build Completes it creates some directories

* Copy all the files in (./dist/browser/) to apache home directory (/var/www/html/)
```
sudo cp dist/browser/* /var/www/html
```
*After copying successfully, open the browser and go to `http://public_ip_address` and we will be able to see the store page...

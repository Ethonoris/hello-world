## Week 7: 

### Apache2: 

- The **Apache2** Web Server is a popular web server option for creating web pages and using other web services.
- After you find the package for Apache2 in Ubuntu, it can be installed using `sudo apt install apache2`

![Apache1](https://github.com/Ethonoris/hello-world/assets/44278023/455ddfd8-4d57-4778-af80-60f94f2b6627)


- A command that is useful for determining the status of Apache2 is the **systemctl** command.
  - It's used like this: `systemctl status apache2`
 
![Apache2](https://github.com/Ethonoris/hello-world/assets/44278023/2ae9bd26-b059-4c9d-a42e-a84ed8121418)


- If we wanted to use a text based web browser to view a web page, we could use **w3m**
  - We first want to install it: `sudo apt install w3m` 
- Using w3m, we can view the Apache2 default page by entering this: `w3m localhost`

![Apache3](https://github.com/Ethonoris/hello-world/assets/44278023/4aab00bf-7ecc-40bd-8a75-27262c56a1d1)


- You can also view it in a graphical browser by clicking on the link for the *external IP address*

![Apache4](https://github.com/Ethonoris/hello-world/assets/44278023/aa496489-a2a2-4073-8e03-205a7d1b97c4)


- To set up our own page, we'll want to move the default page to a new file, and create a new index page.
  - To get to the proper directory and then move the file, we will type: `cd /var/www/html/`
  - And then: `sudo mv index.html index.html.original`
  - Lastly, to create a new page: `sudo nano index.html`
 - The new page can then be written in html.

![Apache6](https://github.com/Ethonoris/hello-world/assets/44278023/83416464-ead7-4435-a333-784c560f7f7d)

![Apache7](https://github.com/Ethonoris/hello-world/assets/44278023/170d1588-1c0b-437a-9f14-e56137253ed0)

### PHP: 

- **PHP** is a *server-side programming language* which needs to be installed on a server to be used.
- To install PHP on Ubuntu, we will enter: `sudo apt install php libapache2-mod-php`
  - And then Apache2 needs to be restarted: `sudo systemctl restart apache2`
- We'll check to make sure it was installed correctly by first going back to `cd /var/www/html/`
  - We then create a file called info.php: `sudo nano info.php`
  - In that file, we will input:

![PHP1](https://github.com/Ethonoris/hello-world/assets/44278023/dc22596c-5315-4b88-afff-aad32c4bd137)

- We can visit it with the external IP address: [info.php](http://34.125.21.77/info.php)
- To configure it so that Apache2 opens a file called index.php first, instead of index.html, we will first go to the appropriate directory: `cd /etc/apache2/mods-enabled/`
- Then we will backup a file called dir.conf and use Nano to edit it: `sudo cp dir.conf dir.conf.bak`
  - `sudo nano dir.conf`
  - We want to change it so it looks like this, with index.php first on the list:
 
![PHP2](https://github.com/Ethonoris/hello-world/assets/44278023/8b6c83ef-96e2-42ea-a8f6-cc0ca5f93bf5)

- When making a config change, we will want to run this command: `apachectl configtest`
  - If it says that the syntax is ok, then we can reload and restart Apache2. 
  - To reload: `sudo systemctl reload apache2`
  - To restart: `sudo systemctl restart apache2`
- Now we need to create the index.php file: `sudo nano index.php`
- We are turning it into a browser and OS detecter using HTML and PHP.

![PHP3](https://github.com/Ethonoris/hello-world/assets/44278023/b48d652b-b20a-4761-81ee-d884c0196c15)

- It is now the first one to come up when we use the external IP as a link: [index.php](http://34.125.21.77/)
- However, the previous page is not gone and can still be viewed if you specify it in the URL: [index.html](http://34.125.21.77/index.html)

### MySQL: 

- Now we will install **MySQL Community Server** and ensure that it works with Apache2 and PHP.
- To install: `sudo apt install mysql-server`
- We will check to see if it is running correctly using this command: `systemctl status mysql`

![SQL1](https://github.com/Ethonoris/hello-world/assets/44278023/dc503ef4-195d-4e33-8e8d-e2f2c74def03)

- Now to set up MySQL securely, we have to run the secure installation script: `sudo mysql_secure_installation`
- Once that is sorted out, we can login as the root user to make sure that it works: `mysql -u root`
  - Then we type the command: `show databases;`
  - This is what we get:
 
![SQL2](https://github.com/Ethonoris/hello-world/assets/44278023/d016a2d4-2b9b-4609-91e4-756e6013a692)

- Next, we need to create a regular user account to use it: `create user 'opacuser'@'localhost' identified by 'XXXXXXXXX';`
- Then we create a new database: `create database opacdb;`
- We'll grant the user all the necessary privileges: `grant all privileges on opacdb.* to 'opacuser'@'localhost';`
- Using `show databases;` we can see the new database:

![SQL3](https://github.com/Ethonoris/hello-world/assets/44278023/ddf2a467-9ce6-488c-b9f5-b9d0606371e2)

- Logging in as the opacuser we created allows us to access the databases: `mysql -u opacuser -p`
- We can see the opacdb database that we created, so we'll `use opacdb;`
- Now we can create a simple table to put in the database using this basic SQL statement:

![SQL4](https://github.com/Ethonoris/hello-world/assets/44278023/add5dc50-ed93-4c36-97e6-8276b7cbdd29)

- With the commands `show tables;` and `describe books;` we can see the table we just made:

![SQL5](https://github.com/Ethonoris/hello-world/assets/44278023/1c5204ac-494f-4697-8d83-d68559f503b6)

- Now we can populate that table with some data:

![SQL6](https://github.com/Ethonoris/hello-world/assets/44278023/085e6d93-5fef-47bf-bef7-5660aef3f269)

- With this SQL statement, we can then view the records we entered into the table: `select * from books;`

![SQL7](https://github.com/Ethonoris/hello-world/assets/44278023/301b160f-9d09-4f80-9b8b-605b34e27190)

- We should install PHP support for MySQL: `sudo apt install php-mysql php-mysqli`
  - Then we'll restart Apache2 and MySQL: `sudo systemctl restart apache2` and `sudo systemctl restart mysql`
- We need to make sure PHP can authenticate with MySQL so here is what we have to do:
  - First, we change directories: `cd /var/www/html/`
  - Second: `sudo touch login.php`
  - Next, we have to enter `sudo chmod 640 login.php`
  - Then we want to change the ownership of it: `sudo chown :www-data login.php`
  - This shows us what has been changed: `ls -l login.php`
  - Now we finally can create login.php: `sudo nano login.php`
- Inside that file, we can add this, albeit with the specific names and password substituted in: 

![SQL8](https://github.com/Ethonoris/hello-world/assets/44278023/97a5e18b-4654-4a18-a455-a35f180c0da7)

- Now we'll create a file that interacts with the database, which we can put on the website: `sudo nano opac.php`
- In that file, we can enter in the necessary code: 

![SQL9](https://github.com/Ethonoris/hello-world/assets/44278023/4c01f247-ef51-48da-bb92-5079d789a968)

- All that's left is to check and see if the syntax the PHP works!
  - This command will output nothing if it is working correctly: `sudo php -f login.php`
  - This command will output HTML if it's working properly: `sudo php -f opac.php`
 - From there, all we need to do is enter the external IP address into the URL address bar and specify opac.php to see the web page: 

![SQL10 - Basic OPAC](https://github.com/Ethonoris/hello-world/assets/44278023/ba6f67fd-4ba9-4c57-a1ee-8d961682bbea)



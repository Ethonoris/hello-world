## Week 11: 

- This week we install Omeka and use it to make another website.
- First we have to install the necessary prerequisites to make sure that it'll run correctly, **ImageMagick** and **Apache Rewrite**

```
sudo apt install imagemagick
sudo a2enmod rewrite
```

- Then we'll reboot Apache2 and we're ready to start installing Omeka!
- We need to prepare a database and a database user in MySQL for the Omeka installation.
- Logging into MySQL as the root user is the first step as usual:

```
sudo su
mysql -u root
```

- Next, we can create the database and user:

```
create user 'omeka'@'localhost' identified by 'XXXXXXXXX';
create database omeka;
grant all privileges on omeka.* to 'omeka'@'localhost';
```

- Now we can change directories and download Omeka:

```
cd /var/www/html
sudo wget https://github.com/omeka/Omeka/releases/download/v3.1.2/omeka-3.1.2.zip
sudo unzip omeka-3.1.2.zip
```

- We'll want to rename the directory to be just "omeka" instead of "omeka-3.1.2" so we can do the following:

```
sudo mv /var/www/html/omeka-3.1.2 /var/www/html/omeka
```

- We can check that it worked by changing our directory to it:

```
cd /var/www/html/omeka
```

- Now that we're in that directory and we know that it's working, we should configure the database credentials for it.
- We will need to find the db.ini file and we will alter it similarly to what was done with the Wordpress config file.

```
sudo nano db.ini
```

- From there we enter the host as localhost, and the username, password, and database name.

  ![Omeka1](https://github.com/Ethonoris/hello-world/assets/44278023/fc05aa86-a6c5-4dc6-95d2-3f4ad4c56d89)

- Then we'll change the owner of the files in the Omeka directory like with Wordpress:

```
sudo chown -R www-data:www-data /var/www/html/omeka
```

- Now we want to restart Apache2 and MySQL and then we will go to our external IP web address and enter the form to set up the rest of Omeka:

```
sudo systemctl restart apache2
sudo systemctl restart mysql
```

- Once that is done, we can go to the Omeka dashboard and start tweaking the site.

![Omeka2](https://github.com/Ethonoris/hello-world/assets/44278023/6b010a54-a2fc-4d3c-8f15-f12bd084bd80)

![Omeka3](https://github.com/Ethonoris/hello-world/assets/44278023/334be569-21f7-4852-afbc-3d21f91bb682)

![Omeka4](https://github.com/Ethonoris/hello-world/assets/44278023/1716798d-477a-4bfb-8ccb-cd348f4e73d9)

![Omeka5](https://github.com/Ethonoris/hello-world/assets/44278023/b3115ed5-53a8-4076-8dee-7f49c35df455)

- It works! Looks like we're all set! 

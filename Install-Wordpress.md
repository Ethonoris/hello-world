## Week 10: 

- This week we're installing and activating Wordpress through our virtual machines.
- After making sure we are using the most up to date versions of PHP and SQL, we want to run a command to install several other required modules:

```
sudo apt install php-curl php-xml php-imagick php-mbstring php-zip php-intl
```

- Then we restart Apache2 and MySQL, and proceed with the Wordpress install.
- Next, we'll change directories to /var/www/html and then download Wordpress:

```
cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xzvf latest.tar.gz
```

- Now we can login to MySQL and create a new database and a user for Wordpress, similar to what we did before.
- First we change to the root user temporarily:

```
sudo su
mysql -u root
```

- Then we create the user and the database, which includes a new password for this user.[^1]
- Afterwards, we can grant the user privileges to access what it needs to.

```
create user 'wordpress'@'localhost' identified by 'XXXXXXXXX';
create database wordpress;
grant all privileges on wordpress.* to 'wordpress'@'localhost';
show databases;
\q
```
- Next up, we need to set up the config file for Wordpress.
- Changing to the new Wordpress directory, we will copy the existing config file and rename it before editing it:

```
cd /var/www/html/wordpress
sudo cp wp-config-sample.php wp-config.php
sudo nano wp-config.php
```

- Now we'll add the name of our new database and database user to the config file, as well as make sure we include the following line of code at the bottom to disable file transfer uploads to our new Wordpress website.
- Also we'll add our password here too were it says to do so. 

![Wordpress Config1](https://github.com/Ethonoris/hello-world/assets/44278023/e7b17064-26fe-49f4-9a17-ce82904fd9fb)

```
define('FS_METHOD','direct');
```

- We can optionally change the name of the directory to alter the URL of our website by doing this:

```
sudo mv /var/www/html/wordpress /var/www/html/blog
```

- This would change the URL to end in blog instead of Wordpress.
- Now we need to change ownership of the directory so that Wordpress can use it:

```
sudo chown -R www-data:www-data /var/www/html/wordpress
```

- Lastly, we have to run the install script for Wordpress in our browser by entering the following URL, and following the remaining instructions in the [Wordpress installation documentation](https://developer.wordpress.org/advanced-administration/before-install/howto-install/) starting from step 5.[^2]

```
http://11.111.111.11/wordpress/wp-admin/install.php
```

- Now all we need to do is set up a basic site and make sure that it works!



[^1]: This password should be an actual password that you write down. the X's are just a stand in for a password. 
[^2]: Just like before, the external IP address shown above is a stand in, and should be replaced with your own external IP. 

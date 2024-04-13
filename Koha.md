## Week 12: 

- This week we've been tasked with installing and configuring **Koha** the *integrated library system.*
- The first thing we need to do is create a new virtual machine that can actually support Koha.
- Similar to before, we will create the VM with these important differences:

1. Change "series" to "E2"
2. Set "Machine Type" to "2 vCPU"
3. Make sure it is set to have 4 GB of memory

- Once that's done, we have to create an exception to the current firewall rules for our new VM to allow Koha to use port 8080.
- The steps are as follows:

1. In Google Cloud, click the menu icon in the top left corner
2. Select the "VPC Network" option
3. Click on "Firewall"
4. Choose "Create a Firewall Rule" of the options at the top of the page
5. Name it something like "Koha" and give it a description such as "Open port 8080"
6. Select "All instances in the network"
7. In the box labeled "Source IPv4 ranges" type "0.0.0.0/0"
8. Click on "Specified protocols and ports" and check the "TCP" box, and type "8080" in the "Ports" text box
9. Click "Create"

- Now it's time to login and start prepping our new VM for Koha.
- We want to update the server first like always:

```
sudo apt update
sudo apt upgrade
sudo apt autoremove -y && sudo apt clean
```

- Then we can install **gnupg2** which we'll need for encryption of data and other tasks for Koha.

```
sudo apt install gnupg2
```

- Now we should reboot the VM after all of that:

```
sudo reboot now
```

- We'll need to create a Koha repository for sycronizing the current Koha data and keeping track of updates when they become available.
- We can become the root user in order to simplify the commands we're going to have to use and then add the repository and verify it:

```
sudo su
echo 'deb http://debian.koha-community.org/koha stable main' | sudo tee /etc/apt/sources.list.d/koha.list
wget -q -O- https://debian.koha-community.org/koha/gpg.asc | sudo apt-key add -
```

- At this point, we should run an update to sync the repository, and then we'll be ready to install Koha!

```
apt update
apt show koha-common
apt install koha-common
```

- Now we need to configure a few Koha files which we can start by modifying one in Nano:

```
nano /etc/koha/koha-sites.conf
```

- And this requires us to change the INTRAPORT line from "80" to "8080" in the config file we just opened.
- After that, we have to install and set up MySQL again[^1] and we'll set the root user password:[^2]

```
apt install mysql-server
mysqladmin -u root password bibliolib1
```

- Now since Apache2 was already installed along with Koha, we only need to activate URL rewrite and CGI tools, and then restart Apache2:

```
a2enmod rewrite
a2enmod cgi
systemctl restart apache2
```

- With that, we can create a database for Koha and edit another config file:

```
koha-create --create-db bibliolib
nano /etc/apache2/ports.conf 
```

- In the config file, we need to add "Listen 8080" right below where it says "Listen 80"
- Then we should run a test to make sure that the changes are valid, and if they are, we can restart Apache2 again:

```
apachectl configtest
systemctl restart apache2
```

- Now in order to run a series of commands, we're going to disable default Apache2 so we can activate both deflate and our website. Then we can reload and restart one more time:

```
a2dissite 000-default
a2enmod deflate
a2ensite bibliolib
systemctl reload apache2
systemctl restart apache2
```

- We can now move to the web installer portion of the set up.
- In the config section of this file, we can find our username and password to login to Koha:

```
nano /etc/koha/sites/bibliolib/koha-conf.xml
```

- Once we have the username and password written down, we can go to our web installer page using our external IP address in place of "IP-ADDRESS" in the following URL:

```
http://IP-ADDRESS:8080
```

- Here is where we'll follow the installation process as per the Koha installation documentation: [Intro to Installing Koha](https://koha-community.org/manual//22.11/en/html/installation.html)
- Now that that is done, we can make the public OPAC available for us to view by following these steps:

1. Click on the "More" dropdown in the navigation bar
2. Select "Administration"
3. Choose "System Preferences"
4. Select OPAC from the nav bar on the left
5. Find the line which says "OPACBaseURL"
6. Enter your external IP address in the format, "http://IP-ADDRESS"
7. Click the yellow "Save all OPAC preferences" button

- All that's left to do now is start adding to the system and testing it out.

![Koha-Patrons](https://github.com/Ethonoris/hello-world/assets/44278023/2942b29f-f706-41b0-b2f1-9a16d3e62468)

![Koha-Items](https://github.com/Ethonoris/hello-world/assets/44278023/b5cb1d62-6a68-4f69-add4-04fb513bda91)

![Koha-Checkout](https://github.com/Ethonoris/hello-world/assets/44278023/42369ee8-f3ea-44e5-9659-9dd12fce1969)

- Looks like it's all set! 

[^1]: The process of running set up for MySQL should otherwise be the same as was covered in a previous week's documentation. 
[^2]: The password displayed in this documentation is a placeholder. 

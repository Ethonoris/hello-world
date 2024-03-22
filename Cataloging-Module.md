## Week 9: 

- This time, we're creating a basic cataloging module.
- We need to change directory and create a new directory first, to make a new index.html page like so: 

```
cd /var/www/html
sudo mkdir cataloging
cd cataloging
sudo nano index.html
```

- In the new index page, we'll add this code to create the input form for the cataloging module:

```
<!DOCTYPE html>
<html>
<head>
    <title>Enter Records</title>
</head>
<body>
    <h1>OPAC Library Administration</h1>

    <p>This is the library administration page for entering records into the OPAC.</p>
    <p>Please do not use this page unless you are an authorized cataloger.</p>

    <form action="insert.php" method="post">
        <label for="author">Author:</label>
        <input type="text" name="author" id="author" required><br><br>

        <label for="title">Book Title:</label>
        <input type="text" name="title" id="title" required><br><br>

        <label for="publisher">Publisher:</label>
        <input type="text" name="publisher" id="publisher" required><br><br>

        <label for="copyright">Copyright:</label>
        <input type="date" id="copyright" name="copyright">

        <input type="submit" value="Submit">
    </form>
</body>
</html>
```

- Next, we now need to create an insert.php page to make sure that the form functions as it's intended:

```
<?php

// Load MySQL credentials
require_once '../login.php';

// Establish connection
$conn = mysqli_connect($db_hostname, $db_username, $db_password) or
  die("Unable to connect");

// Open database
mysqli_select_db($conn, $db_database) or
  die("Could not open database '$db_database'");

// Prepare and bind SQL statement
$stmt = $conn->prepare("INSERT INTO books (author, title, publisher, copyright) VALUES (?, ?, ?, ?)");
$stmt->bind_param("ssss", $author, $title, $publisher, $copyright);

// Set parameters and execute statement
$author = $_POST["author"];
$title = $_POST["title"];
$publisher = $_POST["publisher"];
$copyright = $_POST["copyright"];

if ($stmt->execute() === TRUE) {
    echo "New record created successfully";
} else {
    echo "Error: " . $stmt->error;
}

// Close statement and connection
$stmt->close();
$conn->close();

echo "<p>Return to the cataloging page: <a href='http://11.111.111.111/cataloging/'>http://11.111.111.111/cataloging/</a></p>";
?>
```

- Like before, we have to make sure that the external IP address is replaced with our real counterpart, rather than the stand-in above.
- Now we'll set up basic security authentication for the OPAC by making a user who can sign in to the cataloging module.
- To do that, we first need to make an authentication file:

`sudo htpasswd -c /etc/apache2/.htpasswd libcat`

- Then once we've created that and the password it asked for afterwards, we can open the apache2.conf file to make a change: 

`sudo nano /etc/apache2/apache2.conf`

- Without changing anything else, we need to look for the section that says "AllowOveride None" and change it to "AllowOveride All"
- after we save and exit that file, we then need to change directories and create a file called .htaccess

```
cd /var/www/html/cataloging
sudo nano .htaccess
```

- Inside the .htaccess file, we should add the authentication code:

```
AuthType Basic
AuthName "Authorization Required"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
```

- Then all that's left to do is check the config, and restart Apache2.

```
apachectl configtest
sudo systemctl restart apache2
systemctl status apache2
```

- Now we can go see if it works!

![Cataloging1](https://github.com/Ethonoris/hello-world/assets/44278023/b2c56b2b-3d79-437a-b6ce-16290439cd44)

![Cataloging2](https://github.com/Ethonoris/hello-world/assets/44278023/d8d854df-01ae-43cd-8b2c-b0056849fe6c)

![Cataloging3](https://github.com/Ethonoris/hello-world/assets/44278023/ab7ff955-d859-46e7-9d86-892641582014)

- Perfect! Now we should adjust permissions and ownership of some files and directories.
- changing directories by backing up one from cataloging, we can go:

```
 sudo chown :www-data /var/www/html
 sudo chmod -R g+s /var/www/html
```

- That will make sure that any new files and directories are owned by the www-data group. 

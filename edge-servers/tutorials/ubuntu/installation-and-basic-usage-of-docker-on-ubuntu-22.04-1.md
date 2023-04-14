---
description: >-
  This tutorial walks through the installation of the popular Wordpress content
  management system on your Ubuntu 22.04 Edge Server.
---

# Installation of Wordpress on Ubuntu 22.04

<figure><img src="../../../.gitbook/assets/wordpress.png" alt=""><figcaption></figcaption></figure>

## Introduction <a href="#introduction" id="introduction"></a>

WordPress is an incredibly versatile and user-friendly Content Management System (CMS) that powers millions of websites worldwide. Originally designed as a blogging platform, it has since evolved into a comprehensive solution for creating and managing diverse types of websites, from personal blogs to e-commerce stores and online portfolios. With its intuitive interface, extensive plugin ecosystem, and a vast array of customizable themes, WordPress makes it easy for users with varying technical expertise to build and maintain a professional and functional website. Whether you are a beginner or an experienced web developer, WordPress offers endless possibilities to bring your vision to life on the web.

_Note: This tutorial will probably also work for other versions of ubuntu. It may also work for other linux distributions with slight modifications to the install commands_

### Prerequisites

Before you start, you will need an Ubuntu 22.04 Edge Server with a non-**root** user with `sudo` privileges and a firewall enabled to block non-essential ports.

You can learn how to do this by following our base configuration tutorial for Ubuntu 22.04:

{% content-ref url="base-configuration-for-ubuntu-22.04.md" %}
[base-configuration-for-ubuntu-22.04.md](base-configuration-for-ubuntu-22.04.md)
{% endcontent-ref %}

Once you’re done setting this up, log in as your non-**root** user and proceed to step 1.

## Tutorial

### 1. Install the LAMP Stack

WordPress requires a web server, a database, and PHP. We will install Apache, MySQL, and PHP (LAMP stack) on Ubuntu 22.04.

```
sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql php-curl php-gd php-intl php-mbstring php-soap php-xml php-xmlrpc php-zip
```

### 2. Configure MySQL

Secure the MySQL installation by running:

```
sudo mysql_secure_installation
```

Follow the prompts to set a root password and answer the security questions.

Next, create a database and user for WordPress:

```
sudo mysql -u root -p
```

Enter your MySQL root password, then execute the following commands:

```
CREATE DATABASE wordpress;
CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpressuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

Replace 'your\_password' with a secure password of your choice.

### 3. Download and Configure Wordpress

Download the latest version of WordPress:

```
cd /tmp
wget https://wordpress.org/latest.tar.gz
tar xzvf latest.tar.gz
```

Move the extracted files to the Apache web server's document root:

```
sudo cp -R /tmp/wordpress/* /var/www/html/
```

Set the proper ownership and permissions:

```
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
```

### 4. Configure Wordpress

Create the WordPress configuration file:

```
cd /var/www/html
sudo cp wp-config-sample.php wp-config.php
```

Edit the wp-config.php file to add your database information:

```
sudo nano wp-config.php
```

Find the following lines and replace the placeholders with your database information:

```
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpressuser');
define('DB_PASSWORD', 'your_password');
define('DB_HOST', 'localhost');
```

Save and close the file.

### 5. Enable URL Rewriting

Enable the Apache rewrite module to support permalinks in WordPress:

```
sudo a2enmod rewrite
```

Edit the Apache configuration file:

```
sudo nano /etc/apache2/sites-available/000-default.conf
```

Add the following block of code under the `DocumentRoot /var/www/html` line:

```
<Directory /var/www/html>
    Options Indexes FollowSymLinks MultiViews
    AllowOverride All
    Require all granted
</Directory>
```

Save and close the file.

### 6. Restart Apache

Restart the Apache web server for the changes to take effect:

```
sudo systemctl restart apache2
```

### Conclusion

Now, open your browser and navigate to http://your\_server\_ip or http://your\_domain to complete the WordPress installation through the web interface.

Follow the prompts to enter your site information, create an admin account, and configure your settings.

Congratulations! You have successfully installed WordPress on your Ubuntu 22.04 Edge Server.

You can read more about Wordpress and find out how to tailor it to your needs in the docs and learn sections of the Wordpress site.

{% embed url="https://learn.wordpress.org" %}

{% embed url="https://wordpress.org/documentation/" %}

---
layout: post
title:  "How To Install LAMP Stack On Ubuntu 15.10!"
date:   2016-01-08 15:04:23
categories: mytags update
tags: [mytags]
---
`LAMP` is a combination of operating system and open-source software stack. The acronym LAMP came from the first letters ofLinux, Apache HTTP Server, MySQL or MariaDB database, and PHP/Perl/Python. This tutorial describes how to install LAMP stack on Ubuntu 15.10, however the steps described below should work on previous Ubuntu versions such as Ubuntu 15.04/14.10/14.04/13.10 etc.

### Install LAMP Stack On Ubuntu 15.10

## 1. Install Apache

Apache is an open-source multi-platform web server. It provides a full range of web server features including CGI, SSL and virtual domains.

To install Apache, enter:

{% highlight ruby %}
sudo apt-get install apache2
{% endhighlight %}

Test Apache:

Open your web browser and navigate to http://localhost/ or http://server-ip-address/.

## 2. Install MySQL

`MySQL` is a relational database management system (RDBMS) that runs as a server providing multi-user access to a number of databases, though SQLite probably has more total embedded deployments

{% highlight ruby %}
sudo apt-get install mysql-server mysql-client
{% endhighlight %}

During installation, you’ll be asked to setup the MySQL “root” user password. Enter the password and click Ok.

Re-enter the password.

MySQL is installed now.

You can verify the MySQL server status using command:

## On Ubuntu 15.10/15.04:
{% highlight ruby %}
sudo systemctl status mysql
{% endhighlight %}



## On Ubuntu 14.10 and previous versions:
{% highlight ruby %}
sudo service mysql status
{% endhighlight %}

## 3. Install PHP

PHP (recursive acronym for PHP: Hypertext Preprocessor) is a widely used open-source general purpose scripting language that is especially suited for web development and can be embedded into HTML.

Install PHP with following command:

{% highlight ruby %}
sudo apt-get install php5 php5-mysql libapache2-mod-php5
{% endhighlight %}

To test PHP, create a sample “testphp.php” file in Apache document root folder.

{% highlight ruby %}
sudo nano /var/www/html/testphp.php
{% endhighlight %}

Add the following lines:
{% highlight ruby %}
<?php
phpinfo();
?>
{% endhighlight %}

Restart apache2 service.

On Ubuntu 15.10/15.04:

{% highlight ruby %}
sudo systemctl restart apache2
{% endhighlight %}

On Ubuntu 14.10 and lower versions:

{% highlight ruby %}
sudo service apache2 restart
{% endhighlight %}

Navigate to http://server-ip-address/testphp.php. It will display all the details about php such as version, build date and commands etc.

If you want to install all php modules at once, enter the command sudo apt-get install php* and restart the apache2 service. To verify the modules, open web browser and navigate to http://server-ip-address/testphp.php. You will able to see all installed php modules.

## 4. Manage MySQL Databases (Optional)

Install phpMyAdmin

`phpMyAdmin` is a free open-source web interface tool used to manage your MySQL databases. It is available in the Official Debian repositories. So install it with command:

{% highlight ruby %}
sudo apt-get install phpmyadmin
{% endhighlight %}

Select the Web server that should be automatically configured to run phpMyAdmin. In my case, it is apache2.

The phpMyAdmin must have a database installed and configured before it can be used. This can be optionally handled by dbconfig-common.

Select ‘Yes’ to configure database for phpmyadmin wjth dbconfig-common.

Enter password of the database’s administrative user.

Enter MySQL application password for phpmyadmin:
Re-enter password:

Success! phpMyAdmin installation is installed.

Additional Note: if you followed all steps carefully, phpMyAdmin should work just fine. In case phpMyAdmin is not working, please do the following steps.

Open terminal, and type:

{% highlight ruby %}
sudo nano /etc/apache2/apache2.conf
{% endhighlight %}

Add the following line at the end.

{% highlight ruby %}
Include /etc/phpmyadmin/apache.conf
{% endhighlight %}

Save and Exit. Restart apache service:

## On Ubuntu 15.10/15.04:

{% highlight ruby %}
sudo systemctl restart apache2
{% endhighlight %}

## On Ubuntu 14.10 and lower versions:

{% highlight ruby %}
sudo /etc/init.d/apache2 restart
{% endhighlight %}

## 5. Access phpMyAdmin Web Console

Now, you can access the phpmyadmin console by navigating to http://server-ip-address/phpmyadmin/ from your browser.

Enter your MySQL username and password which you have given in previous steps. In my case its “root” and “ubuntu”.

You will be redirected to PhpMyAdmin main web interface.

From here, you can manage your MySQL databases from phpMyAdmin web interface.

That’s it. Your LAMP stack is ready to use.

Good luck..........

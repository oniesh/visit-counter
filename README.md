https://devzone.zend.com/4/php-101-part-1-down-the-rabbit-hole/ We're not learning PHP just read through this so that you have an idea of what PHP is.

Her is the code for the hit counter that we were using: http://justintadlock.com/web-design/counter

These are the commands that i have used to insatall apache.

sudo apt-get update ,sudo apt-get install apache2,sudo apache2ctl configtest,sudo nano /etc/apache2/apache2.conf,
sudo systemctl restart apache2,sudo ufw app list,sudo ufw app info "Apache Full",sudo ufw allow in "Apache Full".

From the command line i have used the iproute2 tools to get the address by typing this command:

ip addr show | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'.

After finding the address,i took the address and paste it on the browser to get the default Ubuntu 16.04 Apache web page.

These are the steps that i have used to install php:

sudo apt-get install php libapache2-mod-php php-mcrypt php-mysql


To do this, type this command to open the dir.conf file in a text editor with root privileges.

sudo nano /etc/apache2/mods-enabled/dir.conf

It will look like this:

<IfModule mod_dir.c>

      DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
      
</IfModule>

We want to move the PHP index file highlighted above to the first position after the DirectoryIndex specification, like this:

<IfModule mod_dir.c>
      
      DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
    
</IfModule>

When you are finished, save and close the file by pressing Ctrl-X. You'll have to confirm the save by typing Y and then hit Enter to confirm the file save location.

sudo systemctl restart apache2
sudo systemctl status apache2

In Ubuntu 16.04, this directory is located at /var/www/html/.We can create the file at that location by typing:

sudo nano /var/www/html/info.php

This will open a blank file. We want to put the following text, which is valid PHP code, inside the file:

<?php
phpinfo();
?>

When you are finished, save and close the file.

Now we can test whether our web server can correctly display content generated by a PHP script. To try this out, we just have to visit this page in our web browser. 
http://your_server_IP_address/info.php

This is the code that i have used in counter.php
<?php
/* counter */

//opens countlog.txt to read the number of hits
$datei = fopen("/var/www/html/countlog.txt","r");
$count = fgets($datei,1000);
fclose($datei);
$count=$count + 1 ;
echo "$count" ;
echo " hits" ;
echo "\n" ;

// opens countlog.txt to change new hit number
$datei = fopen("/countlog.txt","w");
fwrite($datei, $count);
fclose($datei);

?>

This is the code that i have used for info.php

<?php
phpinfo();
?>

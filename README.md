https://devzone.zend.com/4/php-101-part-1-down-the-rabbit-hole/
We're not learning PHP just read through this so that you have an idea of what PHP is.

Her is the code for the hit counter that we were using: 
http://justintadlock.com/web-design/counter

These are the commands that i have used to insatall apache.
sudo apt-get update
sudo apt-get install apache2
sudo apache2ctl configtest
sudo nano /etc/apache2/apache2.conf
sudo systemctl restart apache2
sudo ufw app list
sudo ufw app info "Apache Full"
sudo ufw allow in "Apache Full"

This is the command that i have used to find the server IP address.
From the command line i have used the iproute2 tools to get the address by typing this command:
ip addr show | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'
After finding the address,i took the address and paste it on the browser to get the default Ubuntu 16.04 Apache web page.

PROJECT 1: LAMP STACK IMPLEMENTATION IN AWS.
- Create an aws account with ubuntu operating system.
- Create a keypair with choice name and download it.
- Select instance, we will be using the free tier mode on the course of this project then set up.
- Launch your EC2 virtual server and connect then open terminal using your previously downloaded key pair and ssh.
<img width="1440" alt="Screenshot 2022-10-13 at 12 01 01 AM" src="https://user-images.githubusercontent.com/115854902/196277466-0bd9b93a-1677-46cf-89d8-fdadbda89ec7.png">

STEP 1: INSTALLING APACHE AND UPDATING THE FIREWALL
The apache web server is one of the most popular web servers in the world, it is well documented which makes it a great default for creating websites in the world.
- Install apache using ubuntu's package manager
- run "sudo apt update"
<img width="1440" alt="Screenshot 2022-10-13 at 12 06 09 AM" src="https://user-images.githubusercontent.com/115854902/196283893-57c33278-1084-49cb-a282-9ce263acf563.png">
- run sudo apt install apache2
<img width="1440" alt="Screenshot 2022-10-13 at 12 08 12 AM" src="https://user-images.githubusercontent.com/115854902/196284837-d642117f-e071-48f7-bdd3-162a31eaa9ee.png">
- verify apache2 is running as a service in our OS
-run sudo systemctl status apache2
<img width="1440" alt="Screenshot 2022-10-13 at 12 08 46 AM" src="https://user-images.githubusercontent.com/115854902/196285767-e82d3a73-da00-4f27-a349-d915e5e18014.png">
Add a rule(inbound connection through port 80) to TCP Port 22 opened by default on our EC2 machine.
Access our running server locally in our buntu shell by running
-curl http://localhost:80
- To test how our apache http server can respound to request from the internet, open a web browser of your choice and try to access the following url
-http://<public IP address>:80
<img width="848" alt="Screenshot 2022-10-13 at 1 33 38 PM" src="https://user-images.githubusercontent.com/115854902/196292009-9a972ce1-d984-4fe5-b070-9df9c85820e8.png"

STEP 2: INSTALLING MYSQL
 MySQL is a popular relational database management system used within PHP environment.
 - To acquire and install MYSQL "sudo apt install mysql-server"
 - sudo mysql
 <img width="1440" alt="Screenshot 2022-10-13 at 12 35 11 AM" src="https://user-images.githubusercontent.com/115854902/196307855-c46ee1ce-788a-44b5-ac8e-1a2a47c336d9.png">
 -start the interactive script by running 
 -sudo mysql_secure_installation
<img width="1440" alt="Screenshot 2022-10-14 at 1 09 43 AM" src="https://user-images.githubusercontent.com/115854902/196306877-37fb01e9-0e4e-454b-b32b-f99dbd011b42.png">
-test if you are able to log into mysql console by typing
- sudo mysql-p
<img width="1440" alt="Screenshot 2022-10-14 at 1 11 33 AM" src="https://user-images.githubusercontent.com/115854902/196307748-6d176f33-52dd-4009-803f-dcfe6bb07ef8.png">
-To exit MYSQL console type
<img width="1440" alt="Screenshot 2022-10-14 at 1 49 27 AM" src="https://user-images.githubusercontent.com/115854902/196308129-a7077bd2-b268-4815-9ffc-878731384569.png">

STEP 3: INSTALLING PHP
There are 3 PHP packages that enables apache to handle PHP files.
- To install this 3 packages at once run sudo apt install php libapache2-mod-php php-mysql
<img width="1440" alt="Screenshot 2022-10-14 at 1 49 27 AM" src="https://user-images.githubusercontent.com/115854902/196309548-2d68db63-89f6-4ecf-9050-bb3e9224a908.png">
<img width="1440" alt="Screenshot 2022-10-14 at 1 51 03 AM" src="https://user-images.githubusercontent.com/115854902/196309606-afd9bec7-027e-4bc5-82d5-04de30ceebfe.png">
- to confirm your PHP version run php -v
<img width="1440" alt="Screenshot 2022-10-14 at 1 52 01 AM" src="https://user-images.githubusercontent.com/115854902/196310016-4f6f66dd-e7b6-4b30-89d2-303b81db8d83.png">

STEP 4: CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE
- Create the directory for 'projectlamp' using the command 'mkdir'
sudo mkdir /var/www/projectlamp
- Next, assign ownership of the directory with your current system user, run
sudo chown -R $USER:$USER /var/www/projectlamp
- create and open a new configuration file in apache's directoty using the vi command
<img width="1440" alt="Screenshot 2022-10-14 at 9 39 46 PM" src="https://user-images.githubusercontent.com/115854902/196311423-7f6cf9c4-22a0-4207-81f0-8928940e953f.png">
-This will create a new blank file. Paste in the following bare-bones configuration by hitting on i on the keyboard to enter the insert mode, and paste the text:
<img width="1440" alt="Screenshot 2022-10-14 at 9 41 20 PM" src="https://user-images.githubusercontent.com/115854902/196313188-f5530572-5319-43c7-b193-4f0b214aaea3.png">
To save and close the file, simply follow the steps below:

Hit the esc button on the keyboard
Type :
Type wq. w for write and q for quit
Hit ENTER to save the file
You can use the ls command to show the new file in the sites-available directory
sudo ls /etc/apache2/sites-available
You will see something like this;
000-default.conf  default-ssl.conf  projectlamp.conf

<img width="1440" alt="Screenshot 2022-10-15 at 12 28 05 AM" src="https://user-images.githubusercontent.com/115854902/196313696-f5acbceb-72af-4578-b3a0-8e6100497e45.png">
- to enable the new virtual host run command 
sudo a2ensite projectlamp
-to disable Apache’s default website use a2dissite command ,type: sudo a2dissite 000-default
-To make sure your configuration file doesn’t contain syntax errors, run:
sudo apache2ctl configtest
-Finally, reload Apache so these changes take effect:
sudo systemctl reload apache2
<img width="1440" alt="Screenshot 2022-10-15 at 3 13 02 AM" src="https://user-images.githubusercontent.com/115854902/196314553-6ebf459d-abd1-4275-9488-05bce906b2e0.png">

Now go to your browser and try to open your website URL using IP address:
http://<Public-IP-Address>:80
<img width="1440" alt="Screenshot 2022-10-15 at 3 13 02 AM" src="https://user-images.githubusercontent.com/115854902/196317335-3f2cd5f4-898e-4d52-85f0-56eb5d2c401e.png">

I forgot to take a screenshot of my browser 

STEP 5: ENABLE PHP ON THE WEBSITE
To create a custom location to host your websites files and folders run the following commands;
sudo vim /etc/apache2/mods-enabled/dir.conf
IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:

        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
After saving and closing the file, you will need to reload Apache so the changes take effect:

sudo systemctl reload apache2

<img width="1440" alt="Screenshot 2022-10-15 at 3 13 02 AM" src="https://user-images.githubusercontent.com/115854902/196316833-26f6d3d4-eae5-4817-ad5a-c7788520ca56.png">


we’ll create a PHP test script to confirm that Apache is able to handle and process requests for PHP files.

Create a new file named index.php inside your custom web root folder:

vim /var/www/projectlamp/index.php
This will open a blank file. Add the following text, which is valid PHP code, inside the file:

<?php
phpinfo();
When you are finished, save and close the file, refresh the page and you will see a page similar to this:
<img width="1440" alt="Screenshot 2022-10-15 at 4 07 16 AM" src="https://user-images.githubusercontent.com/115854902/196318224-7fd5cbef-36bb-47c5-97a9-5c94e84c90ad.png">

This page provides information about your server from the perspective of PHP. It is useful for debugging and to ensure that your settings are being applied correctly.

If you can see this page in your browser, then your PHP installation is working as expected.

After checking the relevant information about your PHP server through that page, it’s best to remove the file you created as it contains sensitive information about your PHP environment -and your Ubuntu server. You can use rm to do so:

sudo rm /var/www/projectlamp/index.php
You can always recreate this page if you need to access the information again later.


<img width="1440" alt="Screenshot 2022-10-15 at 4 07 16 AM" src="https://user-images.githubusercontent.com/115854902/196318711-f8259df8-28d5-4b38-8ad3-f816935007c6.png">

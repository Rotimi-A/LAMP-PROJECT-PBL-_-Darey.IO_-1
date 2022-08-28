## WEB STACK IMPLEMENTATION USING LINUX, APACHE, MYSQL, PHP [LAMP]

#### CREATE AN AWS ACCOUNT AND LAUNCH AN UBUNTU SERVER

![Ubuntu Server 20 05 LTS (HVM), SSD Volume Type](https://user-images.githubusercontent.com/111234300/185796799-12c132ee-bab1-4cd6-aece-e1542e397598.png)

### THE NEXT STEP IS TO CONNECT OUR LOCAL HARDWARE TO THE UBUNTU SERVER ON AWS

#### I USED AN UBUNTU TERMINAL SO THE PROCESS WAS STRAIGHT FORWARD

``` 
DOWNLOAD YOUR SECURITY KEY AND ENSURE YOU DON'T MISPLACE IT OR YOU WON'T BE ABLE TO ACCESS YOUR SERVER

TAKE NOTE OF YOUR CHMOD FILE "CHMOD rTx_01.PEM" & THE PUBLIC DNS IN YOUR SSH CLIENT ON AWS

AS SHOWN IN THE IMAGE BELOW: SSH -i "rTx_01.PEM" ec2-user@ec2-44-202-54-176.comput-1.amazonaws.com

 ```
![CONNECT AND SSH TREMINAL](https://user-images.githubusercontent.com/111234300/185797211-ef8f9022-c404-4800-b56e-b005c12a07c0.png)

#### CHANGE DIRECTORY TO WHERE THE PRIVAKE KEY FILE (.PEM) WAS STORED
#### RUN THE CODE
`sudo chmod 0400 <private-key-name>.pem`

#### SIMPLY CONNECT TO THE INSTANCE BY RUNNING THIS CODE

`ssh -i <private-key-name>.pem ubuntu@<Public-IP-address>`

![screenshot (313) connecting the AWS ec2 server](https://user-images.githubusercontent.com/111234300/187042529-953ada79-4f82-40f5-a97e-f51f785a7a6b.png)

##### visually, the connection will be somthing like this (you are now the client)

![image](https://user-images.githubusercontent.com/111234300/187041464-34b1cc3b-6faa-4059-a702-afc74ce03829.png)


### THE COMPONENTS OF A LAMP STACK ARE:
* LINUX
* APACHE
* MYSQL
* PHP (PHYTON, OR PERL)

### NOW, THE NEXT PHASE OF OUR IMPLEMENTATION IS TO INSTALL APACHE
`#update a list of packages in package manager`

`$ sudo apt update`

`#run apache2 package installation`

`$ sudo apt install apache2`

#### TO VERIFY THAT APACHE2 IS RUNNING AS A SERVICE IN OUR OS, USE THE FOLLOWING COMMAND
`sudo systemctl status apache2`


![Screenshot (338)](https://user-images.githubusercontent.com/111234300/187042001-34879682-c337-4bdb-ab99-87892008f102.png)

#### NOW THAT WE HAVE SUCCESSFULLY LAUNCHED OUR FIRST WEB SERVER IN THE CLOUDS 
##### WE NEED TO OPEN TCP port 80 SO WE CAN RECEIVE ANY TRAFFIC THROUGH OUR WEB SERVER 


![image](https://user-images.githubusercontent.com/111234300/187042253-4735f1be-9a78-4aae-8099-eeb9e7f0763f.png)

#### NOW LET'S ACCESS IT LOCALLY IN OUR UBUNTU SHELL, RUN
`$ curl http://localhost:80`

`$ curl http://127.0.0.1:80`

![Screenshot (324) local host connection on the shell](https://user-images.githubusercontent.com/111234300/187042946-3be7208e-15b4-42ac-9454-62d7a6ad43cf.png)

#### NOW, WE TEST IF OUR APACHE HTTP SERVER CAN RESPOND TO REQUEST CAN RESPOND TO REQUEST FROM THE INTERNET.
##### OPEN A WEB BROWSER OF YOUR CHOICE AND TRY TO ACCESS FOLLOWING URL 

`http://<Public-IP-Address>:80`

![Screenshot (344)](https://user-images.githubusercontent.com/111234300/187043047-13969d49-6c7b-450b-924c-53bb4ebd0e95.png)


### THE THIRD STEP OF THE LAMP STACK IMPLEMETATION IS TO INSTALL OUR DATABASE MANAGEMENT SYSTEM
#### TO BE ABLE TO STORE AND MANAGE DATA FOR OUR SITE, THE RELATIONAL DATABASE MANAGEMENT SYSTEM WE WILL BE USING IS:
## MYSQL

#### AGAIN, USE 'apt' TO ACQUIRE AND INSTALL THIS SOFTWARE:
` $ sudo apt install mysql-server`
![Screenshot (345)](https://user-images.githubusercontent.com/111234300/187043852-f63b7882-13a9-4ce5-b454-a47a8459ed00.png)

#####  WHEN IT IS FINISHED, IT'S RECOMMENDED THAT YOU RUN A SECUIRTY SCRIPT THAT COMES PRE-INSTALLED WITH MySQL
###### THE SCRIPT WILL REMOVE SOME INSECURE DEFAULT SETTINGS AND LOCK DOWN ACCESS TO YOUR DATABASE SYSTEM. START THE INTERACTIVE SCRIPT BY RUNNING:

` $ sudo mysql_secure_installation`

###### WHEN YOU'RE FINISHED, TEST IF YOU'RE ABLE TO LOG IN TO THE MySQL CONSOLE BY TYPING:
` $ sudo mysql`
this will connect to the MySQL server as the adminstrative database user root, which is inferred by the use of sudo when running this command. You should see output like this: 

![Screenshot (346)](https://user-images.githubusercontent.com/111234300/187044207-ef9c6e35-d484-44bd-8ead-49fc20ebb8e7.png)

#### FINAL STEP IS INSTALLING PHP

![Screenshot (347)](https://user-images.githubusercontent.com/111234300/187045173-ff17758d-1f34-439d-bffd-aa8b78b5dc96.png)

#### ONCE THE INSTALLATION IS FINISHED, YOU CAN RUN THE FOLLOWING COMMAND TO CONFIRM YOUR PHP VERSION:

![Screenshot (348)](https://user-images.githubusercontent.com/111234300/187045207-bf1cd8dd-4c53-42b8-81c6-49036c3af470.png)

#### AT THIS POINT, OUR LAMP STACK IS COMPLETELY INSTALLED AND FULLY OPERATIONAL
1. LINUX (Ubuntu)
2. APACHE HHTP SERVER
3. MySQL
4. PHP

#### NOW, IT IS BEST TO SET UP A PROPER APACHE VIRTUAL HOST TO HOLD OUR WEBSITE'S FILES AND FOLDERS.
Virtual host allows us to have mulitple webistes located on a single machine and users of the websites will not even notice it. 

![image](https://user-images.githubusercontent.com/111234300/187045678-f68ee6b3-3e6a-4750-a20d-7b87cac3eb94.png)

Now, we will set up a domain called projectlamp, but you can replace this with any domain of your choice.

Apache on Ubuntu 20.04 has one server block enabled by default that is configured to serve documents from the /var/www/html directory. We will leave this configuration as is and will add our own directory next next to the default one.

Create the directory for projectlamp using ‘mkdir’ command as follows:

`$ sudo mkdir /var/www/projectlamp`
Next, assign ownership of the directory with the $USER environment variable, which will reference your current system user:

`$ sudo chown -R $USER:$USER /var/www/projectlamp`
Then, create and open a new configuration file in Apache’s sites-available directory using your preferred command-line editor. Here, we’ll be using vi or vim (They are the same by the way):

`$ sudo vi /etc/apache2/sites-available/projectlamp.conf`
This will create a new blank file. Paste in the following bare-bones configuration by hitting on i on the keyboard to enter the insert mode, and paste the text:

`VirtualHost *:80

ServerName projectlamp

ServerAlias www.projectlamp 

ServerAdmin webmaster@localhost

DocumentRoot /var/www/projectlamp

ErrorLog ${APACHE_LOG_DIR}/error.log

CustomLog ${APACHE_LOG_DIR}/access.log combined
VirtualHost`

With this VirtualHost configuration, we’re telling Apache to serve projectlamp using /var/www/projectlampl as its web root directory. If you would like to test Apache without a domain name, you can remove or comment out the options ServerName and ServerAlias by adding a # character in the beginning of each option’s lines. Adding the # character there will tell the program to skip processing the instructions on those lines.

You can now use a2ensite command to enable the new virtual host:

`$ sudo a2ensite projectlamp`
You might want to disable the default website that comes installed with Apache. This is required if you’re not using a custom domain name, because in this case Apache’s default configuration would overwrite your virtual host. To disable Apache’s default website use a2dissite command , type:

`$ sudo a2dissite 000-default`
To make sure your configuration file doesn’t contain syntax errors, run:

`$ sudo apache2ctl configtest`
Finally, reload Apache so these changes take effect:

`$ sudo systemctl reload apache2`
Your new website is now active, but the web root /var/www/projectlamp is still empty. Create an index.html file in that location so that we can test that the virtual host works as expected:


###### YOUR NEW WEBSITE IS NOW ACTIVE, BUT THE WEB ROOT /VAR/WWW/PROJECTLAMP IS EMPTY. WE ARE TO CREATE AN IDEX.HTML FILE IN THAT LOCATION SO THAT WE CAN TEST THE VIRTUAL HOST WORKS AS EXPECTED:

`$ sudo echo 'Hello LAMP from hostname' 
$(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`

### FINAL STEP IN THIS PROJECT IS TO ENABLE PHP ON THE WEBSITE
`Index.html` will take precedence over an `index.php` file.

So, to change this behaviour, we will need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive

`sudo vim /etc/apache2/mods-enabled/dir.conf`

`<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>`

After saving and closing the file, you will need to reload Apache so the changes can take effect using this commanc:

` sudo systemctl reload apache2`

Now, we create a PHP script to test that the PHP is correctly installed and configured on our server.
Next, we will create a PHP test script to confirm that Apache is able to handle and process requests for PHP files.

we use this command to create a new file named index.php inside our custom web root folder:
`$ vim /var/www/projectlamp/index.php`

so, we add this text in the blank file that would open:

`<?php

phpinfo();
`
Now, let's refresh our web page and we will have opened a page that looks like this:

![Screenshot (568)](https://user-images.githubusercontent.com/111234300/187077489-291d32d4-0d9e-4ac6-a2b7-cbd77aa0c5f3.png)

After checking the relevant information about your PHP server through that page, it's best to remove the file you created as it contains sensitive information about your PHP environment -and your Ubuntu server. You can use `rm` to do so:

`$ sudo rm/var/www/projectlamp/index.php`

And that's a typical example of how you implement a LAMP STACK.  











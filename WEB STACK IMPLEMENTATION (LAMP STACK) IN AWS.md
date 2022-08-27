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











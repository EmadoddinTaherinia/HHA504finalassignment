
# **HHA504 DATBASE DESIGN FALL 2021 Dr.Hants Williams**
=========================================================

## *Set up a Virtual Machine*

### to start this project first task is to set up an Azure Virtual Machine (VM).
### This process begins with creating a free Microsoft Account via StonyBrook.edu email address.
### Through Azure portal, more services tab -> compute -> virtual machine -> create,
### you are able to create your VM.
### Via sunscriptions menue you are able to add student subscription (Azure for students 12 months free)

### now it is time to define your virtual machine. my VM name : **emadserver**
### Region: useast, Security type : Standard, Availability option (Is a logicall grouping of VMs that allows Azure to understand how your application is build to provide for redundancy and availability [docs.microsoft.com]).
### Authentication type for this instance is password (username, password and IP addresses are provided in an other file).
### To add mysql port (port 3306) navigate to Networking tab -> add inbound security ->rule -> service -> add mysql (port 3306).

## ** SSH to my VM**
===================

### to connect remotly to my Azure VM, first I connect to it via terminal on my machine (ssh command).
### updated my VM  (sedo apt-get update).
### next step is to install mysql on the virtual machine (mysql -server mysql-client.

### To creat dba user with certain passwor I used this code : **'dba'@'%'identifiedby'XXXXXXX'**
### Confirm it  by **select user from mysql.user;**

### Grant all privileges to dba user : *.*to'dba'@'%'with grant option;
### **show grants for dba;**  to confirm.

### Creating e2e database is probably the easiets step: create database e2e;
### The essential code set to pull down h1n1 table and nest it e2e is provided in a separate Google colab notebook.

### To create a *physical back up* (dump): sudo mysqldump e2e>e2e_dump.sql
### and final step is to copy the back up to the local machine: scp emad@VM IP address:/home/emad/e2e_dump.sql ./downloads 

## **h1n1_concern_trigger**

### if new.h1n1_concern > 3 then
	signal sqlstate '45000'
    set message_text = 'H1N1 concern should be a numerical value between 0 and 3. please try again';
  end if;
  end; $$
    delimiter ;

 
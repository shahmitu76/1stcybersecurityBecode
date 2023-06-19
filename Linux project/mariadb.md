

# HTTP+ mariadb (internal website running GLPI)

For this part, we have to install HTTP server first , then MariaDB and finally GLPI.

- Installing apache2 Apache (HTTP) server: 

| sudo apt install apache2 |
| ------------------------ |

-  Installing MariaDB (MySQL) server: 

  | sudo apt install mariadb-server |
  | ------------------------------- |

- Once MariaDB is installed, you can secure the installation by running the following command: 

  | sudo mysql_secure_installation |
  | ------------------------------ |



-  Open up the MariaDB prompt from your terminal: 

  | sudo mariadb |
  | ------------ |



- Create a new account with your **username** with the same capabilities as the **root** account, but configured for password authentication. In my case, username is mitu.

  | GRANT ALL ON *.* TO 'username'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION; |
  | ------------------------------------------------------------ |

- Test it via the command: 

  | sudo mysql -u admin -p; |
  | ----------------------- |

-  Create a new database for GLPI. In the MariaDB shell, run the following commands:

  | CREATE DATABASE glpidb; |
  | ----------------------- |

- | GRANT ALL PRIVILEGES ON glpidb.* TO 'glpiuser1'@'localhost' IDENTIFIED BY 'password'; |
  | ------------------------------------------------------------ |
  | **FLUSH PRIVILEGES;**                                        |
  | **EXIT;**                                                    |

  Here we are creating a glpiuser-glpiuser1 and setting it with password

  ## Installing php

  Run the following commands:

  | sudo apt update          |
  | ------------------------ |
  | **sudo apt install php** |

- Now check the version of php:

  | php -v |
  | ------ |

  You will notice that version 8 of php is installed. We are going to upgrade php ; one of the requirements for GLPI

- | sudo apt update && sudo apt upgrade -y |
  | -------------------------------------- |

- After this, run this command:

  | sudo apt install -y php-curl php-zip php-gd php-intl php-intl php-pear php-imagick php-imap php-memcache php-pspell php-tidy php-xmlrpc php-xsl php-mbstring php-ldap php-ldap php-cas php-apcu libapache2-mod-php php-mysql php-bz2 |
  | ------------------------------------------------------------ |

  This insures all files of php are installed( takes time to type!)

  ## Installing GLPI

- Once this is done, now we will go to firefox web browser.( I have it in my Kali) and type

| https://glpi-project.org/downloads/ |
| ----------------------------------- |

From her, we can download the latest version of 'THE LATEST STABLE GLPI VERSION'. Copy the link of download.

- Go back to your ubuntu server and change the directory 

  | cd /var/www/html/ |
  | ----------------- |

- Type the command:

  | sudo wget https://github.com/glpi-project/glpi/releases/download/10.0.3/glpi-10.0.3.tgz |
  | ------------------------------------------------------------ |

  This is the link which we copied above. We will get an archived file(.tgz). Now we have to recover it.

  | sudo tar -xvf glpi-10.0.3.tgz |
  | ----------------------------- |

  this is the name of the file which you can see when you give the command:

  | ll   |
  | ---- |

- Now after extracting the file, giving the same command ll, you will see the file called glpi/. We require this file.

- Change the mode and ownership of this file

  | sudo chmod 755 -R glpi                   |
  | ---------------------------------------- |
  | **sudo chown -R www-data:www-data glpi** |

- Restart apache webservice:

  | sudo systemctl restart apache2 |
  | ------------------------------ |

  ### Setting  GLPI via web interface

- Check your system's IP address: ip a. For me, its 192.168.0.201

- go to firefox web browser and type the ip address/glpi

- You will see GLPI set up screen. If not you have to allow port 80 connection on your firewall

  | sudo ufw status       |
  | --------------------- |
  | **sudo ufw allow 80** |
  | **sudo ufw status**   |

- It will take through you the installation. At one point, it will ask for :![image-20230619121754810](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230619121754810.png)()

  Give the name of your user database which you created earlier and pwd. In my case, its glpi

- It will show you your database. Select it and proceed till you get the login screen of glpi

- By default its glpi/glpi- its a good idea to change it.

- Last thing, you need to remove install.php file in /var/www/html/glpi/install directory. So go to the terminal of Ubuntu server 

  | cd glpi/                            |
  | ----------------------------------- |
  | cd install/                         |
  | sudo mv install.php install.php.bak |
  | sudo systemctl restart apache2      |

  

- For more help,use this link https://youtu.be/X3jbo6rFntI

And you are done!


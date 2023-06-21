# DHCP (one scope serving the local internal network) isc-dhcp-server

1. Start the ubuntu server in VM. It will ask for the user name and password. Enter the right credentials.

2. Now you need to get your server's IP address, network address ,subnet mask and the interface.

3. Type the command:

   

| ip a |
| ---- |

It will show you the network configuration of your server. For my system;

| IP address | Network address | Subnet mask   | Interface |
| ---------- | --------------- | ------------- | --------- |
| 10.0.2.10  | 10.0.2.0        | 255.255.255.0 | enp0s3    |

![image-20230621162915721](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230621162915721.png)





<img src="C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230621162142891.png" alt="image-20230621162142891"  />

4. To install dhcp server:

   | sudo apt install -y isc-dhcp-server |
   | ----------------------------------- |

   It will ask for the password. after giving right password, hit enter. It will start installing DHCP server. 

   5. Once, it is installed, first we are going to set the static IP address of our server in the file /etc/netplan/00-installer-config.yaml. And also its interface.

      | sudo nano /etc/netplan/00-installer-config.yaml |
      | ----------------------------------------------- |

      

   6. Now, we are going to open configuration file of DHCP server and make some changes in it.

   | sudo nano /etc/default/isc-dhcp-server |
   | -------------------------------------- |
   
   In this file, go at last and put the interfacesv4 as "enp0s3"(in my case) and comment out interfacesv6.
   
   
   
   ![image-20230618213754916](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230618213754916.png)

   Save and exit.

    7.Now to create the pool of dhcp addresses, we will ope another file

   | sudo nano /etc/dhcp/dhcpd.conf |
   | ------------------------------ |
   
   8. Make the changes in the section " Slightly different configuration for an internal subnet", as shown below:
   
   ![image-20230618215652100](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230618215652100.png)

   Use your own network configuration which you noted earlier. Once done, save and exit.

   9. Now, restart your dhcp server:
   
   | sudo systemctl restart isc-dhcp-server |
   | -------------------------------------- |

   10. To check the status of the server whether it is not active:

   | sudo systemctl status isc-dhcp-server |
   | ------------------------------------- |
   
   ![](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230621085510017.png)

   

   As you can see , it is active and running.
   
   11 .Now to allow DHCP server to listen on 67 port:
   
   | sudo ufw allow 67/udp |
   | --------------------- |

   12. Check the status of firewall
   
   | sudo ufw status |
   | --------------- |
   
   
   
   ![image-20230619094711531](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230619094711531.png)

   you can check port 67 is added to the rules of firewall.

   12. Now , in my case, I have to switch off the internet and switch it on again to let my kali machine and linux mint get the right Ip address in my pool of DHCP.  Its working correctly.

   13. Also, type the command on the terminal of ubuntu server:
   
       | dhcp-lease-list |
       | --------------- |
   
       It will give the names of all machines to whom it has leased the address. You can see, its in right DHCP range.
   
   ![](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230621091727740.png)
   
   
   
   That's it. We have configured DHCP server on our machine successfully.
   
   
   
   
# DHCP (one scope serving the local internal network) isc-dhcp-server

1. Start the ubuntu server in VM. It will ask for the user name and password. Enter the right credentials.

2. Now you need to get your server's IP address, network address ,subnet mask and the interface.

3. Type the command:

   

| ip a |
| ---- |

It will show you the network configuration of your server. For my system;

| IP address    | Network address | Subnet mask   | Interface |
| ------------- | --------------- | ------------- | --------- |
| 192.168.0.201 | 192.168.0.0     | 255.255.255.0 | enp0s3    |

![image-20230618212400743](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230618212400743.png)

4. To install dhcp server:

   | sudo apt install -y isc-dhcp-server |
   | ----------------------------------- |

   It will ask for the password. after giving right password, hit enter. It will start installing DHCP server. 

   5. Once , it is installed, we are going to open configuration file of DHCP server and make some changes in it.

      | sudo nano /etc/default/isc-dhcp-server |
      | -------------------------------------- |

      In this file, go at last and put the interfacesv4 as "enp0s3"(in my case) and comment out interfacesv6.

      

      ![image-20230618213754916](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230618213754916.png)

      Save and exit.

      6. Now to create the pool of dhcp addresses, we will ope another file

      | sudo nano /etc/dhcp/dhcpd.conf |
      | ------------------------------ |

      7. Make the changes in the section " Slightly different configuration for an internal subnet", as shown below:

         ![image-20230618215652100](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230618215652100.png)

         Use your own network configuration which you noted earlier. Once done, save and exit.

         8.Now, restart your dhcp server:

         | sudo systemctl restart isc-dhcp-server |
         | -------------------------------------- |

         9. To check the status of the server whether it is not active:

            | sudo systemctl status isc-dhcp-server |
            | ------------------------------------- |

            ![image-20230618220133040](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230618220133040.png)

            As you can see , it is active and running.

            10.Now to allow DHCP server to listen on 67 port:

            | sudo ufw allow 67/udp |
            | --------------------- |

            11. Check the status of firewall

                | sudo ufw status |
                | --------------- |

         

         ![image-20230619094711531](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230619094711531.png)

         you can check port 67 is added to the rules of firewall.

         12. Now , in my case, I have to switch off the internet and switch it on again to let my kali machine and linux mint get the right Ip address in my pool of DHCP.  Its working correctly.

         13. Also, type the command on the terminal of ubuntu server:

             | dhcp-lease-list |
             | --------------- |

             It will give the names of all machines to whom it has leased the address. You can see, its in right DHCP range.

         

         ![image-20230619094541411](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230619094541411.png)

         

         That's it. We have configured DHCP server on our machine successfully.

         

   
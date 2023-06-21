# How to install Ubuntu Server in Oracle Virtual Box

I followed this link. Very easy and fast.

https://youtu.be/YtH9D2SqBqA

Some of the steps which I did:

- Download Ubuntu 22.04 LDS from Ubuntu.com

- It will give you  an iso file. Save it.

- Make sure the system has essential requirements.

- Go to Virtual Box and create new.

- It will ask you various space requirements. Change it.

- Now go to settings in Virtual Box

- Make changes in General,System,Display.

- Then go to Storage. Load your iso file image here.

- Go to Network. Change NAT to Nat network. Select ok

- Click on start.

  It will start installing. Will take some time.

  Steps to follow after that:

  1. Choose Language English and keyboard English

  2. Check the network card. It should get IP address from your router , not from Virtual machine.

  3. Your computer should be in same network as your Ubuntu Server

  4.  Install  Ubuntu on whole disk.

  5. Then create your username and password.

  6. We are going to use SSH. So, select it.

  7. After few things, it will start installing.

  8. At one point, its going to ask whether review the logs or reeboot. Choose reboot.

  9. And you are almost done.

  10. It will ask for login.

  11. You will finally log into server.

  12. Now run these commands:

      sudo apt update; sudo apt upgrade

      

      And you are done!

      This is how you install Ubuntu Server.

      Please refer to above video in case you need any help.

      

      ## Few more steps:

      
      
      - ## On my Virtual box I installed 2 machines, Ubuntu server and client Kali
      
        ## *I set up settings on NAT network on both  machines.*
      
      
      
      - # *Giving static IP address to my Ubuntu Server:*
      
        ​     
      
        >   
        >
        > | sudo nano  /etc/netplan/ 00-installer-config.yaml |
        > | ------------------------------------------------- |
      
      - # *Install Firewall, Harden ssh, Client config, Server config, Test connection:*
      
        ​    **I used documentation: Server_hardening**
  
  
  
  


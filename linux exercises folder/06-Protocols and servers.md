# Protocols and servers

## Goals  

1. HTTP/HTTPS
    - Configure a virtual host
    - Deploy a one pager 
2. SSH 
    - Configure key-based authentication
3. SMB
    - Provide network shares to specific clients
4. TELENET
    - Install and configuration
5. FTP
    - Install and configuration


## HTTP, FTP, SMTP, POP3, IMAP, SMB.

First, please follow tthese pdf :
- http://dma.vgtu.lt/KTA/KTA10_EN.pdf

## Exercises

> Connect to the virtual machine 10.12.181.X with the following credentials:  
> * ip : 10.12.181.X  
> * user : student  
> * password : student  

1.  On your kali (or other) , install ``ngnix`` to have an http server on port 8080. Replace the default page of ngnix by an html page displaying a hello world.
    > No answer required
    >
    > [^How to install nginx on port 8080]: 
    >
    > 
    >
    > 1. Open the Kali machine. Go to root. Command: sudo su root
    >
    > 2. sudo apt update
    >
    > 3. apt install nginx
    >
    > 4. Check the status of nginx: Command: systemctl status nginx
    >
    > 5. for now: it will be inactive
    >
    > 6. Start it. Command: Systemctl start nginx
    >
    > 7. Now go to /etc/nginx/sites-enabled. There will be a file called default
    >
    > 8. open default. Command : nano default
    >
    > 9. Change the server port from 80 to 8080(both places)
    >
    > 10. go down and change "server_name_i" to "server_name "" "
    >
    > 11. Save it.
    >
    >     
    >
    > [^Replace the default page of ngnix by an html page displaying a hello world.]: 
    >
    > 1. go to /var/www/html
    > 2. Change index.html. If there is some other file, delete it.
    > 3. open index.html.  command: nano index.html and change the content to "Hello World" and save it.
    > 4. start the nginx again
    > 5. now go to firefox and write localhost:8080
    > 6. It will give Hello World page
    >
    > 
    
1. What other well-known service could be used instead of nginx? 
    > Your answer : Apache webserver

1. On your student machine, create a temporary http server with python, on port ``5000``. Then on your kali machine, open a browser and go to the address ``10.12.181.X:``.
    > Your command : python -m SimpleHTTPServer 5000 or python3 -m http.server 5000(on kali)
    >
    > to check: go to Kali, open the firefox and give student ip address: 5000. It will show you the listing of all directories in your student machine.
    
1. Let's imagine that a hacker owns the domain name ``g00gle.com``, which tool would allow him to obtain an ssl certificate (https) very easily?
    > Your answer :  
    >
    > 1. Certbot: Certbot is an open-source tool that simplifies the process of obtaining and installing SSL certificates. It supports various certificate authorities, including Let's Encrypt.
    > 2. OpenSSL: OpenSSL is a widely used open-source toolkit that includes a command-line tool for generating certificate signing requests (CSRs) and managing SSL certificates. It provides flexibility and advanced options for certificate management.
    > 3. Commercial Certificate Authorities: Many commercial certificate authorities offer user-friendly tools and services for obtaining SSL certificates. These include providers like DigiCert, Comodo SSL, and GlobalSign. They often provide web-based interfaces or APIs that streamline the certificate issuance process.
    > 4. Web Hosting Control Panels: If you are using a web hosting service, they might provide built-in tools or integrations with SSL certificate providers. Control panels like cPanel, Plesk, and DirectAdmin often include features to request and install SSL certificates with just a few clicks.
    
1. On a linux machine, what tool could you use to have a self-signed SSL certificate on your local machine (localhost) ? 
    > Your answer : On a Linux machine, you can use the OpenSSL tool to generate a self-signed SSL certificate for your local machine (localhost). OpenSSL is a widely used open-source cryptographic library that provides various functionalities, including SSL/TLS certificate generation.

1. On your student machine, install the ftp service and connect from your kali machine.
    > No answer required

1. What is the default port for ftp? 
    > Your answer : Port 21

1. Is the ftp protocol secured?
    > Your answer : no..ftps

1. On your student machine, install the telnet service and connect from your kali machine.
    > No answer required

1. What is the default port for telnet? 
    > Your answer : 23

1. Is the telnet protocol secured?
    > Your anbswer : No
    
1. Create a share file with samba between your Kali machine and your student machine.
    > No answer required






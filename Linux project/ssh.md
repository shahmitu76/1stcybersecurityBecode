# **The server is remotely manageable (SSH)**

- Install the SSH server package (`openssh-server`):

- ```
  
  sudo apt install openssh-server
  ```

- 1. During the installation, you may be prompted to confirm the installation and enter your password.

  2. Once the installation is complete, the SSH server will start automatically. You can check its status with the following command:

     ```
     
     sudo service ssh status
     ```

     If it shows the SSH server as active or running, the installation was successful.

  3. By default, SSH should allow remote access, but it's good to verify that any necessary firewall rules are in place to allow incoming SSH connections. If you are using a firewall, such as `ufw`, you can enable SSH access with the following command:

     ```
     
     sudo ufw allow OpenSSH
     ```

     Adjust the command based on your specific firewall setup.

  4. At this point, the SSH server should be installed and accessible remotely. You can use an SSH client to connect to the server using the server's IP address or hostname.

     Example SSH connection command:

     ```
     
     ssh username@server_ip_address
     ```

     Replace `username` with your actual username on the server, and `server_ip_address` with the IP address or hostname of your server.

- By following these steps, you should have successfully installed the SSH server (`openssh-server`) on your Linux server, allowing you to remotely manage the server via SSH.

  


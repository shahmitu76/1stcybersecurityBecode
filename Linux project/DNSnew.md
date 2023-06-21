# DNS BIND INSTALLATION

## Installing BIND Packages

To get started with BIND DNS, you’ll first need to install the BIND packages on your machine with the apt package manager.

1. Open your terminal and log in to your server.
2. Next, run the `apt update` command below to update and refresh the repository package index. This command ensures that you are installing the latest version of packages.

3. Once updated, run the below `apt install` command to install BIND packages for the Ubuntu server.

The bind9-utils and bind9-dnsutils packages provide additional command-line tools for BIND.

| sudo apt install bind9 bind9-utils bind9-dnsutils -y |
| ---------------------------------------------------- |

4. Lastly, run the `systemctl` command below to verify the BIND service.

The BIND package comes with the service named and is automatically started and enabled during the BIND package installation.

| # Check if named service enabled<br/>sudo systemctl is-enabled named |
| ------------------------------------------------------------ |
| **# Check named service status<br/>sudo systemctl status named** |

Now you should see the BIND named service is enabled with the status as active (running). At this point, the BIND service will run automatically at system startup/boot.

## Configuring BIND DNS Server



All configuration for BIND is available at the */etc/bind/* directory, and configurations for the `named` service at */etc/default/named*.

1. Edit the */etc/default/named* configuration using your preferred editor and add option `-4` on the `OPTIONS` line, as shown below. This option will run the `named` service on IPv4 only.

```powershell
OPTIONS="-4 -u bind"
```

Save the changes you made and close the file.

2. Next, edit the */etc/bind/named.conf.options* file and populate the following configuration below the `directory "/var/cache/bind";` line.

This configuration sets the BIND service to run on default UDP port 53 on the server’s localhost and public IP address (10.0.2.10; server's IP). At the same time, it allows queries from any host to the BIND DNS server using the Cloudflare DNS 1.1.1.1 as the forwarder.

    // listen port and address
    listen-on port 53 { localhost; 172.16.1.10; };
    
    // for public DNS server - allow from any
    allow-query { any; };
    
    // define the forwarder for DNS queries
    forwarders { 1.1.1.1; };
    
    // enable recursion that provides recursive query
    recursion yes;

At the bottom, comment out the listen-on-v6 { any; }; line, as shown below, to disable the named service from running on IPv6.

3. Lastly, run the following command to verify the BIND configuration.

```bash
sudo named-checkconf
```

If there’s no output, the BIND configurations are correct without any error.

## Setting Up DNS Zones

Now, we will create a name server ns1.becodeserver.io

1. Edit the */etc/bind/named.conf.local* file using nano editor.

This configuration defines the forward zone (/etc/bind/zones/forward.becodeserver.io), and the reverse zone (/etc/bind/zones/reverse.becodeserver.io) for the becodeserver.io domain name.

![](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230621100625194.png)

Save the changes and close the file.

2. Next, run the below command to create a new directory (`/etc/bind/zones`) for string DNS zones configurations.

```bash
mkdir -p /etc/bind/zones/
```

3. Run each command below to copy the default forward and reverse zones configuration to the `/etc/bind/zones` directory.

![](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230621101729822.png)

4. Now, edit the forward zone configuration (*/etc/bind/zones/forward.becodeserver.io*) using nano and populate the configuration below.

![](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230621153230293.png)

Save the changes and close the file

5.Like the forward zone, edit the reverse zone configuration file (*/etc/bind/zones/reverse.becodeserver.io*) and populate the following configuration.The reverse zone translates the server IP address to the domain name. 

![](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230621153818034.png)

Save the changes and close the file.

6. Now, run the following commands to check and verify BIND configurations.

| sudo named-checkconf |
| -------------------- |

And these:

![](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230621142749343.png)

7. Lastly, run the `systemctl` command below to restart and verify the `named` service. Doing so applies new changes to the `named` service.

```bash
# Restart named service
sudo systemctl restart named

# Verify named service
sudo systemctl status named
```

You should see them active and running.

## Opening DNS Port with UFW Firewall

 Now run the below command to `allow` the `Bind9` to the UFW firewall.

```bash
sudo ufw allow Bind9
```

Lastly, run the following command to check enabled rules on the UFW firewall.

```bash
sudo ufw status
```

### Testing the DNS configuration in the client

The client needs to be configured to look up the DNS and the domain server name. For that, we need to edit the /etc/resolv.conf file.

**resolv.conf**

The first step in testing BIND9 is to add the nameserver’s IP Address to a host's resolver. The Primary nameserver should be configured as well as another host to double-check things. Refer to DNS client configuration for details on adding nameserver addresses to your network clients. In the end, your nameserver line in /etc/resolv.conf should be pointing at 10.0.2.5 and you should have a search parameter for your domain. Something like this:

```
nameserver  10.0.2.10 search example.org
```

Once this is done, restart the networking service:

`sudo systemctl restart systemd-networkd

![](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230621143541592.png)

 Using these commands, check whether they resolve into an address on a client machine:

- `nslookup becodeserver.io

- `dig 10.0.2.10

  ![](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230621144621820.png)

![](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230621145029951.png)

## That's it. You have successfully configured the DNS.
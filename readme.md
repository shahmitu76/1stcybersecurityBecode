Linux project


Set up the following Linux infrastructure:

1. # One server (no GUI) running the following services:

   I have installed Ubuntu Server 22.04 LDS. Here is the link.

   [Linux project/How to install Ubuntu Server in Oracle Virtual Box.md](Linux project/How to install Ubuntu Server in Oracle Virtual Box.md)

   

   # DHCP (one scope serving the local internal network) isc-dhcp-server

   For DHCP server installation, refer to the link:

   [/linux project/DHCP.md]()

   

   - DNS (resolve internal resources, a redirector is used for external resources) bind

   - # HTTP+ mariadb (internal website running GLPI)[/Linux project/mariadb.md]()

     For this, refer to the above link:

     

     # Weekly backup the configuration files for each service into one single compressed archive & Backups are placed on a partition located on separate disk, this partition must be mounted for the backup, then unmounted

     Refer to this link:[/Linux project/weeklybackup.md]()

     

     # The server is remotely manageable (SSH)

     Refer to this link:[/Linux project/ssh.md]()

     

   # One workstation running a desktop environment and the following apps:

   - LibreOffice
   - Gimp
   - Mullvad browser
   - Required
     1. This workstation uses automatic addressing
     2. The /home folder is located on a separate partition, same disk
   - Optional
     1. Propose and implement a solution to remotely help a user


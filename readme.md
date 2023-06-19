Linux project


Set up the following Linux infrastructure:

1. # One server (no GUI) running the following services:

   I have installed Ubuntu Server 22.04 LDS. Here is the link.

   ["C:\Githubciscopackettraceractivity\cybersecurity1stmonthwork\Linux project\How to install Ubuntu Server in Oracle Virtual Box.md"]()

   ["C:\Githubciscopackettraceractivity\cybersecurity1stmonthwork\Linux project\How to install Ubuntu Server in Oracle Virtual Box.md"]()

   

   

   

   

   - DHCP (one scope serving the local internal network) isc-dhcp-server
   - DNS (resolve internal resources, a redirector is used for external resources) bind
   - HTTP+ mariadb (internal website running GLPI)
   - Required
     1. Weekly backup the configuration files for each service into one single compressed archive
     2. The server is remotely manageable (SSH)
   - Optional
     1. Backups are placed on a partition located on separate disk, this partition must be mounted for the backup, then unmounted

2. One workstation running a desktop environment and the following apps:

   - LibreOffice
   - Gimp
   - Mullvad browser
   - Required
     1. This workstation uses automatic addressing
     2. The /home folder is located on a separate partition, same disk
   - Optional
     1. Propose and implement a solution to remotely help a user

## Performance criteria

The teams must give a sense of confidence to the audience when presenting their demo, the documentation must be clear, structured and must provide all elements of configuration.

## Evaluation methods

- Quality of the documentation and the live demo (5),
- All required items are implemented are working (5),
- Optional items are implemented and working (bonus 5),
- The team demonstrates good organisation and planning (5),
- The team explains and justifies the various choices they made (5),
- Tests were performed to ensure the configuration is working (5),
- The team demonstrate a solid knowledge of the Linux environment when answering questions (5)

## Deliverables

a documentation in word format named LinuxBrief_firstname1_firstname2.docx, a summary in English (at least one page) Live demonstration in front of the group
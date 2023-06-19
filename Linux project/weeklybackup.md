# Weekly backup the configuration files for each service into one single compressed archive

- So, first I checked the time zone of my system. Date was fine, but time was different. So, I set the right time zone.

[](https://www.serverlab.ca/tutorials/linux/administration-linux/how-to-check-and-set-timezone-in-ubuntu-20-04/)use this link to see how to set right time zone.





### How to mount the backup partition



- To mount the backup partition, you need to follow these steps:

- 1. Identify the device and partition of the backup partition. You can use the `lsblk` or `fdisk -l` command to list the available disks and partitions on your system.

  2. Choose a mount point directory where you want to mount the backup partition. For example, you can create a directory called `/mnt/backup` to serve as the mount point.

     ```
     sudo mkdir /mnt/backup
     ```

  3. Use the `mount` command to mount the backup partition. Replace `/dev/sdX1` with the appropriate device and partition identifier for your backup partition, and specify the mount point directory you created in the previous step.

     ```
     sudo mount /dev/sdX1 /mnt/backup
     ```

     The `sudo` command is used to run the `mount` command with administrative privileges. I used sda2.

  4. You can verify that the backup partition is mounted by running the `mount` command without any arguments. The output will list the currently mounted partitions, including the backup partition.

     ```
     lsblk
     ```

     Check if the backup partition is listed, and the mount point matches the one you specified.

      Output:    /dev/sda2 on /mnt/backup

     ​                  sda2             part  /mnt/backup

     Now your backup partition is mounted and ready to use. You can proceed with the script or any other operations you need to perform on the backup partition. Remember to unmount the partition once you're done to ensure the data is safely written and the partition can be safely removed. 

     To unmount the backup partition, use the following command:

- ```
  sudo umount /mnt/backup
  ```

- Replace `/mnt/backup` with the actual mount point you used.

### Weekly back up configuration with error handling



- To fix any issue, you can add some error handling to the script to check if the files were successfully copied before creating the archive. Here's a version of the script with error handling:


```


# Set the backup directory
backup_dir="/path/to/backup/directory"

# Set the archive filename with the current date
archive_file="$backup_dir/config_backup_$(date +%Y%m%d).tar.gz"

# Create a temporary directory
temp_dir=$(mktemp -d)

# Backup DHCP configuration
if cp /etc/dhcp/dhcpd.conf "$temp_dir/dhcpd.conf"; then
    echo "DHCP configuration backup successful"
else
    echo "Failed to backup DHCP configuration"
fi

# Backup DNS configuration
if cp /etc/bind/named.conf.options "$temp_dir/named.conf.options" && cp /etc/bind/named.conf.local "$temp_dir/named.conf.local"; then
    echo "DNS configuration backup successful"
else
    echo "Failed to backup DNS configuration"
fi

# Backup MariaDB configuration
if cp /etc/mysql/mariadb.conf.d/50-server.cnf "$temp_dir/50-server.cnf"; then
    echo "MariaDB configuration backup successful"
else
    echo "Failed to backup MariaDB configuration"
fi

# Create a compressed archive if the directory is not empty
if [[ -n $(find "$temp_dir" -mindepth 1) ]]; then
    tar -czf "$archive_file" -C "$temp_dir" .
    echo "Backup archive created: $archive_file"
else
    echo "No files to backup. Exiting without creating archive."
fi

# Clean up the temporary directory
rm -rf "$temp_dir"
```

- Save the script to a file, for example, `config_backup.sh`, and make it executable:


```

chmod +x config_backup.sh
```

- Create a backup directory where the archive will be stored:


```

mkdir /path/to/backup/directory
```

- Test the script by running it manually:


```

./config_backup.sh
```

This should create a compressed archive in the specified backup directory with the current date as part of the filename.

- Set up a weekly cron job to execute the script automatically:


```

crontab -e
```

- Add the following line to the crontab file to schedule the script to run every Sunday at 2:00 AM (adjust the timing as needed):

```

0 2 * * 0 /path/to/config_backup.sh
```

Save and exit the crontab file.

That's it! The script will now run automatically every week, creating a compressed archive of the configuration files for DHCP, DNS, and MariaDB services in a single file with a timestamped filename in the specified backup directory.









# Linux mint Installation and Partitioning



For downloading Linux Mint:

- Go to Linux Mint.com

- click on Download

- I have downloaded Cinnamon version of Linux Mint 21.1

- Go ahead and click it.

- Click the nearest region from where you want to download. I chose Netherlands.

- Click over it and soon download will begun.

- You will get an iso file. Save it.

  

Installing it in Virtual Machine

- Go to your virtual machine. I have Oracle VM

- Click on new and fill in the fields as shown in the image below

  

![](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230619145607134.png)

- Then follow the installation. After finishing, click ok
- Then go to Settings- System-processor and click on extended feature. enable it
- Go to Settings-Display. Enable 3d acceleration
- Click on start button to start Linux Mint installation
- Select the first option and hit enter
- Search for Display and increase the resolution and hit ok
- Click on Linux Mint installation icon
- Choose language and keyboard as English
- Enable install media codecs. It may take a while.
- To create the partition yourself, choose Something else.

1. During the Linux Mint Cinnamon installation, choose the "Something else" option for partitioning when prompted.
2. You will see a list of available disks. Select the disk you created in VirtualBox (e.g., /dev/sda) and click "New Partition Table" to create a new partition table.
3. Once the new partition table is created, click on the "Free Space" entry and click the "+" button to create a new partition.
4. Configure the partition as follows:
   - Size: Enter the desired size for the /home partition (e.g., 10GB).
   - Type for the new partition: Select "Logical".
   - Location for the new partition: Select "Beginning of this space".
   - Use as: Select "Ext4 journaling file system".
   - Mount point: Select "/home".
5. Click "OK" to create the partition.

[![Pasted image 20230615152346](https://user-images.githubusercontent.com/133368766/246146501-b82575e9-03e6-41da-9e5c-c674bb4634f3.png)](https://user-images.githubusercontent.com/133368766/246146501-b82575e9-03e6-41da-9e5c-c674bb4634f3.png)

1. Select the remaining free space and click the "+" button to create a new partition.
2. Configure the partition as follows:
   - Size: Leave the remaining space as it is to be used for the root partition.
   - Type for the new partition: Select "Logical".
   - Location for the new partition: Select "Beginning of this space".
   - Use as: Select "Ext4 journaling file system".
   - Mount point: Select "/".
3. Click "OK" to create the partition.

[![Pasted image 20230615152611](https://user-images.githubusercontent.com/133368766/246146550-cb5ce2e2-4d5a-4865-9bb7-1bf9b94895b6.png)](https://user-images.githubusercontent.com/133368766/246146550-cb5ce2e2-4d5a-4865-9bb7-1bf9b94895b6.png)

[![Pasted image 20230615152638](https://user-images.githubusercontent.com/133368766/246146589-416dc517-1631-48b8-a86f-21f9d3cae17c.png)](https://user-images.githubusercontent.com/133368766/246146589-416dc517-1631-48b8-a86f-21f9d3cae17c.png)

Verify the Separate /home Partition

1. Open a terminal (Ctrl+Alt+T).
2. Run the command `lsblk` to list the available block devices.
3. Verify that you see two separate partitions, one mounted as "/" and the other mounted as "/home".



![image-20230617172457133](C:\Users\nimes\AppData\Roaming\Typora\typora-user-images\image-20230617172457133.png)



[https://youtu.be/E3295Le1Jvc](https://youtu.be/E3295Le1Jvc)

follow this link










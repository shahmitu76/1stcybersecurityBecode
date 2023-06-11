# Finding Files with Linux- Answer sheet

Connect to the virtual machine 10.12.181.X with the following credentials:

* **ip** : 10.12.181.X
* **user** : student
* **password** : student

## Find, Locate and Which

### Locate 
The locate command allows you to find a file very quickly. Contrary to what you might think, locate does not look for the file in the tree, but in a database containing the list of existing files. As a result, it is possible that when you have just created a file or a directory that it is not in this database, so you need to update the database using the updatedb command.
This is a disadvantage. Note that the system on which you are working takes care of updating this database. The locate function works as follows:

````sh
$ locate filename
````

### Find

The find command, unlike locate, will search for the file within the tree. The syntax is as follows:
```sh
$ find directory -name file_name
```

where directory is the directory in which the file is to be found, if you want to search for a file in the whole tree, which is very long! You can replace directory with ``/``, this means that you search from the root and therefore in the whole tree. To search in the current directory we use the ``.``, as in the following example :

````sh
$ find . -name my-text.txt
````

You can search in a directory:

````sh
$ find /home/user/ -name my-files.txt
````

When searching for a directory we use the following syntax:
````sh
$ find directory -type d -name directory_name
````

Where directory is the directory in which you are looking for the file.
For example, let's look for the directory(ies) beginning with Wor
in the home directory.

````sh
$ find /home/ -type d -name Wor*
````

For the command to work, the directory in which the binary file is located must be specified in the PATH variable

### Which
which command in Linux is a command which is used to locate the **executable** file associated with the given command by searching it in the path environment variable. It has 3 return status as follows:

- 0 : If all specified commands are found and executable.
- 1 : If one or more specified commands is nonexistent or not executable.
- 2 : If an invalid option is specified.

````sh
$ which whoami
> /usr/bin/whoami
````
For the command to work, the directory in which the binary file is located must be specified in the PATH variable

````shell
$ echo $PATH 
> /home/besec/bin:/home/besec/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
````

**...:/usr/bin...**

## Exercises 
1. Create a file named ``my-file.txt`` with the touch command. Then execute the ``locate my-file.txt`` command. Do you find the file? 
    > Your response :I touch my-file.txt. But it will not be updated in the database as it is just created
1. Run the command sudo ``updatedb``. And run the locate my-file.txt command again. Do you find your file ?
    > Your response : yes
    >
    > 
    >
    > 
1. With the command ``which``, find the executable file nc and indicate the path
    > Command: which nc
    >
    > Path :/bin/nc
1. With the command ``which``, find the executable file becode. What is the flag ?
    > Command: which becode
    >
    > Flag :/flag-BC{WH1CH_FL4G_EXECUTLE_FILE}
1. Search with ``find ``command for a file that contains the name "Edgar Allan Poe". What is the flag ?
    > go to the page of ip student address. it will be a blank page. Right click and find page source.
    >
    > Flag :
    >
    > |                    |                                 |
    > | ------------------ | ------------------------------- |
    > | Edgar Allan Poe ## |                                 |
    > |                    | FLAG : BC{3d54r_4ll4n_P03_FL45} |
    > |                    |                                 |
1. Using the ``find`` command, find the file password.txt and specify the flag.
    > find / -type f -name password.txt 
    >
    > /var/www/html/a/b/c/d/e/g/h/i/j/k/l/m/n/o/p/q/r/s/t/u/v/w/x/y/z/password.txt
    >
    > cat /var/www/html/a/b/c/d/e/g/h/i/j/k/l/m/n/o/p/q/r/s/t/u/v/w/x/y/z/password.txt
    >
    > Flag :FLAG: BC{PASSWORD_FILE}
1. With the command ``find``, find a file that starts with ``becode-`` and ends with ``.sh``.
    > command:  find / -type f -name "becode-*.sh" | grep "FLAG"
    >
    > Flag : BC{FLAG_FIND_PARTIAL_PATH}
1. Using the ``find`` command to identify any file (not directory) modified in the last day, NOT owned by the root
   user and execute ls -l on them. **Chaining/piping commands is NOT allowed!**
    > Your command :  find / ! -user root -type f -newermt "0"
1. With the find command, find all the files that have an authorization of ``0777``.
    > Your command: find / -perm 777 -type f | ls -la
1. With the find command, find all the files in the folder ``/home/student/findme/`` that have an authorization of ``0777`` and change the rights of these files to ``0755``
    > Your command : 
    >
    >  find /home/student/findme  -perm 0777 -type f | chmod 0755 /home/student/findme/*
    >
    > then ls -la
    >
    > 




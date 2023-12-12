# RHEL-2-Advanced Lab-2(part_3)

### 11. Login by user3 and try to unmount /boot.

#### Solution:

If `user3` has been granted permission to run the `/bin/umount` command in the sudoers file, they should be able to execute the `umount` command with elevated privileges using `sudo`. Here are the steps `user3` can follow to unmount `/boot`:

1. Open a terminal.

2. Execute the `umount` command with `sudo` to unmount `/boot`:

   ```bash
   sudo umount /boot
   ```

   If prompted, enter the password for `user3`.

If `user3` has the necessary permissions as configured in the sudoers file, this command will unmount the `/boot` directory. However, if `user3` encounters any issues or receives an error message indicating insufficient permissions, it might be due to additional system configurations or restrictions that prevent certain users from performing the unmount operation, despite having sudo privileges.


<hr /> 

### 12. Login by user4 and remount /boot. Also try to view the partition table using fdisk.

#### Solution:

If `user4` has been granted permissions to execute the `/bin/mount` and `/bin/umount` commands in the sudoers file, they should be able to remount `/boot` using `sudo` and also view the partition table using `fdisk`. Here are the steps `user4` can follow:

### Remounting /boot:

1. Open a terminal.

2. Execute the `mount` command with `sudo` to remount `/boot`:

   ```bash
   sudo mount /boot
   ```

   If prompted, enter the password for `user4`.

This command attempts to remount the `/boot` directory. If `user4` has the necessary permissions as configured in the sudoers file, the `/boot` directory will be remounted.

### Viewing the Partition Table Using fdisk:

1. Open a terminal.

2. Execute the `fdisk` command to view the partition table:

   ```bash
   sudo fdisk -l
   ```

   If prompted, enter the password for `user4`.

This command with `sudo` allows `user4` to view the partition table. The `-l` option lists partition information.

If `user4` encounters any issues or receives an error message indicating insufficient permissions while performing these operations, it might be due to additional system configurations or restrictions despite having sudo privileges.


<hr /> 

### 13. Create a directory with permissions rwxrwx---, grant a second group (sales) r-x permissions

#### Solution: 

To create a directory with permissions `rwxrwx---` (770) and grant a second group (`sales`) `r-x` permissions, you can use the following commands:

```bash
# Create the directory with rwxrwx--- permissions
mkdir directory_name
chmod 770 directory_name

# Add the group 'sales' to the directory
sudo groupadd sales

# Set the group ownership of the directory to the 'sales' group
sudo chgrp sales directory_name

# Grant r-x permissions to the 'sales' group
chmod 750 directory_name
```

Explanation:

1. `mkdir directory_name`: Creates a directory named `directory_name`.
2. `chmod 770 directory_name`: Sets the initial permissions of the directory to `rwxrwx---` (770).
3. `sudo groupadd sales`: Creates a new group named `sales`.
4. `sudo chgrp sales directory_name`: Changes the group ownership of the directory to the newly created `sales` group.
5. `chmod 750 directory_name`: Changes the permissions of the directory to `rwxr-x---` (750), granting `r-x` permissions to the group `sales`.

After executing these commands, the directory will have `rwxrwx---` permissions, allowing the owner and group members full access, while the `sales` group will have `r-x` (read and execute) permissions. Adjust the directory and group names as needed.

<hr /> 

### 14.  create a file on that directory and grant read and write to a second group (sales)

#### Solution:

To create a file within the directory and grant read and write permissions to a second group (`sales`), you can follow these steps:

1. Create a file within the directory:

```bash
touch directory_name/file_name
```

Replace `directory_name` with the name of your directory and `file_name` with the desired file name.

2. Grant read and write permissions to the `sales` group for the created file:

```bash
chmod g+rw directory_name/file_name
```

This command (`chmod g+rw`) adds read and write (`rw`) permissions for the group (`g`) to the specified file within the directory. Adjust the file path and name accordingly.

After running these commands, the `sales` group will have read and write permissions for the specified file within the directory while maintaining the initial permissions for the directory itself (`rwxrwx---`).

<hr /> 

Previous links:    
[part 1](README.md)   
[part 2](README_Part2.md)  

Next Links:     
 [part 4](README_Part4.md)   
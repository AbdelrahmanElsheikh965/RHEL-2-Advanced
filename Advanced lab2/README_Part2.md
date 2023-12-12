# RHEL-2-Advanced Lab-2(part_2)

### 6. Using the chgrp command, set the group ownership of each directory to the group with the matching name

#### Solution:

To set the group ownership of each directory (`sales`, `hr`, and `web`) to the respective groups (`sales`, `hr`, and `web`), you can use the `chgrp` command along with the `-R` flag to recursively change the group ownership.

Here are the commands to set the group ownership for each directory:

```bash
sudo chgrp -R sales /depts/sales
sudo chgrp -R hr /depts/hr
sudo chgrp -R web /depts/web
```

Explanation of the commands:
- `sudo chgrp -R sales /depts/sales`: Changes the group ownership of the `sales` directory and all its contents recursively to the `sales` group.
- `sudo chgrp -R hr /depts/hr`: Changes the group ownership of the `hr` directory and all its contents recursively to the `hr` group.
- `sudo chgrp -R web /depts/web`: Changes the group ownership of the `web` directory and all its contents recursively to the `web` group.

After running these commands, the group ownership of each directory and its contents will be set to the corresponding groups (`sales`, `hr`, and `web`). Adjust the commands according to your directory structure and group names if needed.

<hr /> 

### 7. Set the permissions on the /depts directory to 755, and each subdirectory to 770

#### Solution:

To set the permissions on the `/depts` directory to 755 and each subdirectory (`sales`, `hr`, and `web`) to 770, you can use the `chmod` command to change the permissions. 

Here are the commands to achieve this:

```bash
sudo chmod 755 /depts
sudo chmod 770 /depts/sales
sudo chmod 770 /depts/hr
sudo chmod 770 /depts/web
```

Explanation of the commands:
- `sudo chmod 755 /depts`: Sets the permissions of the `/depts` directory to 755, allowing the owner to have read, write, and execute permissions, and others to have read and execute permissions.
- `sudo chmod 770 /depts/sales`, `sudo chmod 770 /depts/hr`, `sudo chmod 770 /depts/web`: Sets the permissions of the `sales`, `hr`, and `web` directories to 770, allowing the owner and group members to have read, write, and execute permissions.

After executing these commands, the permissions on the `/depts` directory will be set to 755, while the permissions on each subdirectory (`sales`, `hr`, and `web`) will be set to 770 as specified. Adjust the permissions as needed based on your requirements.

<hr /> 


### 8. Set the set-gid bit on each departmental directory

#### Solution:

To set the setgid (set group ID) bit on each departmental directory (`sales`, `hr`, and `web`), use the `chmod` command with the numeric mode `g+s`. This ensures that files created within these directories inherit the group ownership of the directory itself.

Here are the commands to set the setgid bit on each directory:

```bash
sudo chmod g+s /depts/sales
sudo chmod g+s /depts/hr
sudo chmod g+s /depts/web
```

Explanation:
- `sudo chmod g+s /depts/sales`: Sets the setgid bit for the `sales` directory.
- `sudo chmod g+s /depts/hr`: Sets the setgid bit for the `hr` directory.
- `sudo chmod g+s /depts/web`: Sets the setgid bit for the `web` directory.

After running these commands, the setgid bit will be set for each departmental directory (`sales`, `hr`, and `web`). Any files created within these directories will inherit the group ownership of the directory, ensuring consistent group ownership for new files. Adjust the commands according to your directory structure as needed.

<hr /> 

### 9. Use the su command to switch to the user2 account and attempt the following commands:   
```
touch /depts/sales/user2.txt    
touch /depts/hr/ user2.txt     
touch /depts/web/ user2.txt    
```
Which of these commands succeeded and which failed? What is the group ownership of the files that were created?

#### Solution:

These commands attempt to create files named `user2.txt` within the `sales`, `hr`, and `web` directories while logged in as `user2`.

Let's analyze the commands:

```bash
touch /depts/sales/user2.txt
touch /depts/hr/ user2.txt
touch /depts/web/ user2.txt
```

The first command attempts to create a file named `user2.txt` within the `sales` directory. Since the `sales` directory has the group ownership set to the `sales` group and the permissions are `770` (rwxrwx---), and `user2` is a member of the `sales` group, this command should succeed.

The second command (`touch /depts/hr/ user2.txt`) seems to have an extra space between `/depts/hr/` and `user2.txt`. This command will likely fail because it will try to create a file named ` user2.txt` in the current directory (not inside `/depts/hr/`). 

The third command (`touch /depts/web/ user2.txt`) also seems to have a space between `/depts/web/` and `user2.txt`, similarly causing the command to fail for the same reason as the second command.

To verify the group ownership of the files that were created successfully, you can use the `ls` command as `user2`:

```bash
ls -l /depts/sales/user2.txt
```

This command will display the file's details, including the ownership and group. The group ownership should be the same as the group ownership of the `sales` directory, which is likely set to the `sales` group.

Regarding the second and third commands, as they have spaces before the filenames, they will not create files within the respective directories (`hr` and `web`). Instead, they might create a file named ` user2.txt` in the current directory (the directory where the `su` command was initially executed as `user2`).


<hr /> 

### 10. Configure sudoers file to allow user3 and user4 to use /bin/mount and /bin/umount commands, while allowing user5 only to use fdisk command.

#### Solution:

To configure the sudoers file to grant specific users (`user3`, `user4`, and `user5`) permissions to execute certain commands (`/bin/mount`, `/bin/umount`, and `fdisk`) with elevated privileges using `sudo`, you can use the `visudo` command to edit the sudoers file (`/etc/sudoers`).

Please ensure you use `visudo` to edit the sudoers file, as it provides syntax checking to prevent errors that could lock you out of sudo access if the file is incorrectly formatted.

Here are the steps to grant the permissions:

1. Open the sudoers file with `visudo`:

   ```bash
   sudo visudo
   ```

2. Add the following lines at the end of the sudoers file to grant permissions:

   ```plaintext
   user3 ALL=(ALL) /bin/mount, /bin/umount
   user4 ALL=(ALL) /bin/mount, /bin/umount
   user5 ALL=(ALL) /sbin/fdisk
   ```

   Explanation of the lines:
   - `user3` and `user4` are allowed to run `/bin/mount` and `/bin/umount` with sudo privileges.
   - `user5` is allowed to run `/sbin/fdisk` with sudo privileges.

3. Save and exit the sudoers file.

After making these changes and saving the sudoers file, `user3` and `user4` will be able to use the `mount` and `umount` commands with sudo privileges, while `user5` will be able to use the `fdisk` command with sudo privileges.

Ensure that granting sudo access is done cautiously, and only to trusted users, as it allows users to perform potentially sensitive operations with elevated privileges. Always double-check the sudoers file syntax to prevent any configuration errors.

<hr /> 


Previous links:    
[part 1](README.md)  

Next Links:   
[part 3](README_Part3.md)    
[part 4](README_Part4.md)    
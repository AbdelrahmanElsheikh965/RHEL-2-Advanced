# RHEL-2-Advanced Lab-2(part_4)

### 15. set the the owning group as the owning group of any newly created file in that directory.

#### Solution:

To set the owning group of any newly created file in a directory to match the owning group of the directory itself, you can use the setgid (set group ID) bit on the directory. This way, any new files created within the directory will inherit the group ownership of the directory.

Here are the steps to achieve this:

1. Navigate to the directory:

```bash
cd directory_name
```

Replace `directory_name` with the name of your directory.

2. Set the setgid bit for the directory:

```bash
chmod g+s .
```

The `.` at the end of the command refers to the current directory.

By setting the setgid bit on the directory, any new files created within it will inherit the group ownership of the directory, ensuring that the owning group of newly created files matches the owning group of the directory.

<hr />

### 16. Grand your colleagues a collective directory called /opt/research, where they can store generated research results. Only members of group profs and grads should be able to create new files in the directory, and new file should have the following properties:    
• the directory should be owned by root   
• new files should be group owned by group grads   
• group profs should automatically have read/write access to new    files   
• group interns should automatically have read only access to new files    
• other users should not be able to access the directory and its contents at all.

#### Solution:

To set up the `/opt/research` directory with specific permissions and access controls, follow these steps:

1. **Create the `/opt/research` directory:**

    ```bash
    sudo mkdir /opt/research
    ```

2. **Set the directory ownership to root:**

    ```bash
    sudo chown root:root /opt/research
    ```

3. **Set permissions and access controls:**

    - Set the permissions to allow only the owner (root) to access the directory:
    
        ```bash
        sudo chmod 700 /opt/research
        ```
    
    - Set the setgid bit on the directory to ensure new files inherit the group ownership:
    
        ```bash
        sudo chmod g+s /opt/research
        ```
    
    - Grant the `profs` and `grads` groups the necessary permissions:
    
        ```bash
        sudo chgrp grads /opt/research
        sudo chmod 770 /opt/research
        ```
    
4. **Set default permissions for new files:**

    - Grant read/write access to the `profs` group for new files:
    
        ```bash
        sudo chmod g+rw /opt/research
        ```
    
    - Grant read-only access to the `interns` group for new files:
    
        ```bash
        sudo setfacl -d -m g:interns:r /opt/research
        ```

These commands set up the `/opt/research` directory with the specified permissions and access controls:

- Only `root` has access to the directory.
- New files created within the directory will be owned by the `root` user and the `grads` group.
- The `profs` group will have read and write access to new files.
- The `interns` group will have read-only access to new files.
- Other users will not have access to the directory and its contents.

Please note that for setting default permissions using `setfacl`, the filesystem needs to support Access Control Lists (ACLs). Adjust the commands according to your specific Linux environment and filesystem capabilities.

<hr />

Previous links:    
[part 1](README.md)   
[part 2](README_Part2.md)  
[part 3](README_Part4.md)
   
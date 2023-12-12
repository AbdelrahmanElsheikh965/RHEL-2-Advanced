# RHEL-2-Advanced Lab-2-(SELinux)

### 1.Change your default SELinux mode to permissive and reboot.

Changing the default SELinux mode to permissive requires modification in the `/etc/selinux/config` file. Please follow these steps:

1. Open the SELinux configuration file using a text editor like `nano` or `vi`:

    ```bash
    sudo nano /etc/selinux/config
    ```

2. Locate the line that starts with `SELINUX=` in the file.

3. Change the value from `enforcing` to `permissive`:

    Before:
    ```
    SELINUX=enforcing
    ```

    After:
    ```
    SELINUX=permissive
    ```

4. Save the changes and exit the text editor.

5. Reboot your system to apply the changes:

    ```bash
    sudo reboot
    ```

After the system reboots, it will start in the permissive mode for SELinux. In this mode, SELinux will log policy violations but will not enforce them, allowing you to monitor and identify potential issues without blocking actions based on SELinux policies.

### 2.After Reboot, Verify SELinux Mode:

To verify the current SELinux mode after the reboot, use the following command:

```bash
sestatus
```

This command will display the SELinux status, including the mode (enforcing, permissive, or disabled).

### 3.Change Default SELinux Mode to Enforcing:

To change the default SELinux mode to enforcing, modify the `/etc/selinux/config` file:

```bash
sudo nano /etc/selinux/config
```

Change the `SELINUX=` value to `enforcing`, save the file, and reboot the system.

### 4.Change Current SELinux Mode to Enforcing:

To change the current SELinux mode to enforcing without rebooting:

```bash
sudo setenforce 1
```

This command changes the SELinux mode to enforcing immediately.

### 5.Copy /etc/resolv.conf to Root's Home Directory:

To copy `/etc/resolv.conf` to root's home directory:

```bash
sudo cp /etc/resolv.conf /root/
```

### 6.Observe SELinux Context of /etc/resolv.conf:

To observe the SELinux context of `/etc/resolv.conf`:

```bash
ls -Z /etc/resolv.conf
```

### 7.Move resolv.conf from Root's Home Directory to /etc/resolv.conf:

To move `resolv.conf` from root's home directory to `/etc/resolv.conf`:

```bash
sudo mv /root/resolv.conf /etc/resolv.conf
```

### 8.Observe SELinux of the Newly Copied /etc/resolv.conf:

```bash
ls -Z /etc/resolv.conf
```

### 9.Restore SELinux Context of Newly Positioned /etc/resolv.conf:

To restore the SELinux context of `/etc/resolv.conf`:

```bash
sudo restorecon /etc/resolv.conf
```

### 10.Observe SELinux Context of Restored /etc/resolv.conf:

```bash
ls -Z /etc/resolv.conf
```

### 11.Configure OpenSSH for Public Key-Based Login:

Modify the SSH server configuration file `/etc/ssh/sshd_config` to allow public key-based login and disable password authentication (PasswordAuthentication no).

### 12.Create an SSH Key Pair:

Use `ssh-keygen` to create an SSH key pair on the client machine:

```bash
ssh-keygen -t rsa -b 4096
```

### 13.Configure Login Without Password:

Use `ssh-copy-id` or manually copy the public key to the server's `~/.ssh/authorized_keys` file for passwordless login.

### 14.Configure SSH to Prevent Root Logins:

In the `/etc/ssh/sshd_config` file, set `PermitRootLogin no` to prevent root logins via SSH.

### 15.Configure Logrotate to Compress Log Files:

Modify logrotate configuration files in `/etc/logrotate.d/` or `/etc/logrotate.conf` to include `compress` directive for log compression during rotation.

Please note, for steps involving SELinux contexts, ensure the SELinux utilities (`ls -Z`, `restorecon`) are available and that the SELinux policies on your system support these operations. Also, carefully edit configuration files as these changes could impact system security.
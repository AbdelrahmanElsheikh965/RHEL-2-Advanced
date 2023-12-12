# RHEL-2-Advanced Lab-2

### 1. Using the useradd command, add accounts for the following users in your system: user1, user2, user3, user4, user5, user6 and user7. Remember to give each user a password.

Firstly
```
sudo useradd user1
sudo useradd user2
sudo useradd user3
sudo useradd user4
sudo useradd user5
sudo useradd user6
sudo useradd user7

```
Then, 
```
sudo passwd user1
sudo passwd user2
sudo passwd user3
sudo passwd user4
sudo passwd user5
sudo passwd user6
sudo passwd user7

```
<hr /> 

### 2. Using the groupadd command, add the following groups to your system.
```
Group			GID    
sales			10000    
hr			    10001     
web			    10002    
```
Why should you set GID in this manner instead of allowing the system to set the GID by default?

#### Solution:

To add groups to your system with specific GIDs (Group IDs) using the `groupadd` command, you can follow these steps:

1. **Add groups with specified GIDs:**

   Use the `groupadd` command to create the groups with the desired GIDs:

   ```bash
   sudo groupadd -g 10000 sales
   sudo groupadd -g 10001 hr
   sudo groupadd -g 10002 web
   ```

   Here, `-g` specifies the GID for the respective group being created.

As for why you might want to set the GIDs manually instead of allowing the system to assign them by default:

1. **Consistency across systems:**
   
   When managing multiple systems or when collaborating across different environments, manually setting GIDs ensures consistency. Assigning specific GIDs allows you to maintain the same GID for a particular group across various systems, which can simplify management in complex environments.

2. **Avoiding conflicts:**
   
   Manually setting GIDs helps avoid potential conflicts or clashes with existing groups. If the default GIDs are already used or if there's a chance of overlap with other systems, setting unique GIDs helps prevent conflicts.

3. **Maintaining organization:**
   
   By defining GIDs in a structured manner (as per your organizational standards or conventions), it becomes easier to identify groups and their purposes based on their assigned GIDs.

When setting GIDs manually, ensure that the assigned GIDs do not conflict with existing group IDs on your system to prevent issues related to overlapping IDs.

<hr /> 

### 3. Using the usermod command to add user1 and user2 to the sales secondary group, user3 and user4 to the hr secondary group. User5 and user6 to web secondary group. And add user7 to all secondary groups  

#### Solution:

To add users to specific secondary groups using the `usermod` command in Linux, you can perform the following steps:

1. **Add users to secondary groups:**

   Use the `usermod` command to add users to the respective secondary groups:

   ```bash
   sudo usermod -aG sales user1
   sudo usermod -aG sales user2

   sudo usermod -aG hr user3
   sudo usermod -aG hr user4

   sudo usermod -aG web user5
   sudo usermod -aG web user6
   ```

   This command adds user1 and user2 to the "sales" group, user3 and user4 to the "hr" group, and user5 and user6 to the "web" group. `-aG` appends the user to the specified groups.

2. **Add user7 to all secondary groups:**

   To add user7 to all three secondary groups (sales, hr, and web), you can run the following commands:

   ```bash
   sudo usermod -aG sales user7
   sudo usermod -aG hr user7
   sudo usermod -aG web user7
   ```

   This will add user7 to the "sales," "hr," and "web" groups, allowing user7 to be part of all three secondary groups.

<hr /> 

### 4.  Login as each user and use id command to verify that they are in the appropriate groups. How else might you verify this information?

#### Solution:

To verify the group membership for each user, you can use the `id` command when logged in as each user. The `id` command displays the user's identification information, including their primary and supplementary group IDs.

Here's how you can verify the group memberships for each user:

1. **Login as each user:**

   Log in as each user (user1, user2, user3, user4, user5, user6, and user7).

2. **Use the `id` command:**

   Run the `id` command to check the group memberships:

   ```bash
   id
   ```

   This will display the user's ID, primary group ID (`gid`), and a list of supplementary groups (`groups`), including the user's membership in different groups.

Alternatively, you can also use the `groups` command to specifically list the groups a user is a member of:

```bash
groups
```

This command will show the groups the current user belongs to.

To verify this information without logging in as each user, you can run the `id` command along with the username while logged in as a privileged user:

```bash
id user1
id user2
id user3
id user4
id user5
id user6
id user7
```

This command will display the group memberships for each specified user without requiring you to log in as each individual user. Adjust the usernames according to the users you want to verify.

Using the `id` or `groups` commands while logged in as the respective users or using `id` with specific usernames while logged in as a privileged user are effective ways to verify group memberships for users in Linux.


<hr /> 

### 5. Create a directory called /depts with a sales, hr, and web directory within the /depts directory.

#### Solution:

To create the directory structure you've described (with sales, hr, and web directories within the /depts directory), you can use the following commands in the terminal:

```bash
sudo mkdir -p /depts/sales
sudo mkdir -p /depts/hr
sudo mkdir -p /depts/web
```

These commands create the `/depts` directory if it doesn't exist (`-p` flag ensures that the parent directories are created if needed) and then create the `sales`, `hr`, and `web` directories within the `/depts` directory.

After executing these commands, you'll have a directory structure with `/depts` as the parent directory containing `sales`, `hr`, and `web` subdirectories.

<hr /> 

For Other Parts Click the following links:

[part 2](README_Part2.md)  
[part 3](README_Part3.md)    
[part 4](README_Part4.md)      
1. Use systemctl to view the status of all the system services.
	systemctl status

2. Change the default run level back to multi-user.target and reboot.
	1)sudo systemctl set-default multi-user.target
	2)reboot

3. Send mail to the root user.
	echo "Your message body" | mail -s "Subject: Your Subject Here" root

4. Verify that you have received this mail.
	mail
	mail -u yourUserName
	
5. Use  systemctl utility to stop postfix service
	sudo systemctl stop postfix

6. Use systemctl utility to start postfix service
	sudo systemctl start postfix

7. Edit in the GRUB2 configuration file and change the timeout variable equal 20 seconds.
	sudo vi /etc/default/grub
	GRUB_TIMEOUT=20
	sudo update-grub
	then, reboot

8.  Edit in the GRUB2 configuration file and change your default operating system

9. You want to know some information about the status of the system every ten minutes today between the hours of  8:00 AM and 5:00 PM.
	to help investigate some performance issues you have been having. You suspect it might be memory related and want to 
	keep an eye on those resources.
	
	1) Create a Bash script:
		#!/bin/bash

		# Append system status information to a log file
		date >> /path/to/log_file.log
		vmstat >> /path/to/log_file.log
		echo "----------------------" >> /path/to/log_file.log
		# Replace /path/to/log_file.log with the actual path and name of the log file where you want to store the system status information.

	2) Schedule the script using cron
		Open the crontab file using the command : crontab -e

	3) Add an entry to schedule the script to run every ten minutes between 8:00 AM and 5:00 PM
		 */10 8-16 * * * /bin/bash /path/to/monitor_resources.sh

	
10. Use mail as the root user to check for e-mail from the cron jobs you have scheduled.
	1) su -
	2) mail
	NOTE) To exit the mail viewer, type q and press Enter.

11. How could you send the output from these cron jobs to another e-mail address (the manager user)?
	1)	crontab -e
	2)	MAILTO=manager@example.com
	3)	*/10 8-16 * * * /path/to/your_script.sh

------------------------------------------------------------------------------------------------------------------------------------------------
Using yum

1. Attempt to run the command gnuplot. You should find that it is not installed.
	sudo yum install gnuplot

2. Search for the plotting packages.
	sudo yum search plotting

3. Find out more information about the gunuplot package.
	sudo yum info gnuplot

4. Install the gnuplot package.
	sudo yum install gnuplot

5. Attempt to remove the gnuplot package, but say no How many packages would be removed
	sudo yum remove gnuplot

6. Attempt to remove the gunplot-common package but say no How many packages would be removed Using rpm
	sudo rpm -e gnuplot-common

7. List all installed packages in your system.
	sudo rpm -qa

8. View the files in the initscripts package
	sudo yum list files initscripts

9. Get general information about bash rpm.
	sudo yum info bash

10. Have the files from the pam package changed since it was installed
	1) Reinstall the pam package 								=> sudo yum reinstall pam
	2) Retrieve the checksums of the files in the pam package 	=> sudo rpm -V pam > original_checksums.txt
	3) After some time or when you suspect changes 				=> sudo rpm -V pam > current_checksums.txt
	4) Compare the checksums 									=> diff original_checksums.txt current_checksums.txt

11. Which installed packages have gnome in their names?
	sudo yum list installed '*gnome*'

12. Install any uninstalled package from RH Enterprise Linux cds
	
	1) Mount the CD or ISO image to a directory. Replace /media/cdrom with the appropriate mount point:
	=> sudo mount /dev/cdrom /media/cdrom
	
	2) Locate the package you want to install - Explore the mounted CD or ISO to identify the package you wish to install.
	
	3) Install the package using yum with the local repository:
	   Use yum with the --disablerepo option to temporarily disable online repositories and only use the local repository (CD):
	   => sudo yum --disablerepo='*' --enablerepo=cdrun install package_name

	3) Replace package_name with the name of the package you want to install. 
	   Ensure you navigate to the correct path within the mounted CD or ISO to find the package.
	   For instance, if the package is located in the Packages directory on the CD or ISO, and its name is example-package.rpm, the command might look like:
            => sudo yum --disablerepo='*' --enablerepo=cdrun install /media/cdrom/Packages/example-package.rpm

	4) This command will install the specified package from the local CD repository.
	    Remember to unmount the CD after installing the package using:
	    => sudo umount /media/cdrom

	Replace /media/cdrom with the actual mount point used for the CD or ISO.

	Ensure that the CD or ISO used as a local repository contains compatible packages for your RHEL system version to avoid compatibility issues. 
	Adjust the paths and package names according to the specific setup and directory structure of your RHEL CDs or ISOs.

	
13. Search for software resemble the Photoshop software other than Gimp and install it.
	sudo yum search krita

14. Create the file /etc/yum.repos.d/cdrom.repo to enable install from the iso from the iso of Red Hat.

	1) Mount the ISO image to a directory. Replace /media/cdrom with the appropriate mount point:
		sudo mount -o loop /path/to/your_rhel.iso /media/cdrom

	2) Create the YUM repository file:
	    Use a text editor like nano, vim, or gedit to create the repository file:
	    sudo nano /etc/yum.repos.d/cdrom.repo

	3) Add content to the cdrom.repo file:
	    Inside the text editor, add the following content to the cdrom.repo file:
	    [cdrom]
	    name=Red Hat Enterprise Linux $releasever - $basearch - DVD
	    baseurl=file:///media/cdrom
	    enabled=1
	    gpgcheck=0

	4) After creating the repository file, unmount the ISO:
		sudo umount /media/cdrom
	
	This repository file (cdrom.repo) sets up a YUM repository named [cdrom] pointing to the mounted Red Hat ISO. 
	It enables YUM to install packages directly from the ISO file. Adjust the baseurl if your mount point differs from /media/cdrom.
	After creating the cdrom.repo file, you can use yum to install packages from the Red Hat ISO as needed. 
	Remember to remount the ISO and update the repository file if you use a different ISO or move the ISO to a different location.





















































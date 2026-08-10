Linux file system hirearchy 

 Directory      One-line Description                                                                               
 -------------  -------------------------------------------------------------------------------------------------- 
 /            Root directory that contains all files, directories, and mounted filesystems in Linux.             
 /home        Stores the personal home directories of regular users.                                             
 /root        Home directory of the root (administrator) user.                                                   
 /etc         Contains system-wide configuration files for the operating system and applications.                
 /boot        Stores the files required to boot the Linux operating system, including the kernel and bootloader. 
 /usr         Contains user applications, libraries, binaries, and documentation installed by the system.        
 /bin         Stores essential user command binaries required for basic system operations.                       
 /sbin        Stores essential system administration commands used mainly by the root user.                      
 /lib         Contains shared libraries and kernel modules required by binaries in /bin and /sbin.           
 /lib64       Stores 64-bit shared libraries required by applications on 64-bit systems.                         
 /var         Contains variable data such as logs, caches, mail, spool files, and databases.                     
 /opt         Stores optional or third-party software installed outside the package manager.                     
 /tmp         Stores temporary files created by users and applications, usually cleared automatically.           
 /mnt         Used as a temporary mount point for additional disks and filesystems.                              
 /media       Automatically mounts removable storage devices such as USB drives and DVDs.                        
 /dev         Contains device files representing hardware and virtual devices.                                   
 /proc        A virtual filesystem that provides information about running processes and the Linux kernel.       
 /sys         A virtual filesystem that exposes kernel, hardware, and device information.                        
 /run         Stores runtime information such as process IDs (PIDs) and sockets since the last boot.             
 /srv         Contains data served by system services such as web, FTP, or file servers.                         
 /lost+found  Stores recovered files after filesystem consistency checks (fsck).                                 

--------------------------
mkdir - for creating the directory 
mv : for moving the file 
cp : for copying the files (to copy all the files in folder use this command "cp -r")
rm -rf : for deleting the files 
top : Displays running processes along with CPU and memory usage in real time. Press c to show the full command line for each process.
df -h : It displays disk space usage of mounted filesystems in a human-readable format (GB, MB, etc.).
du -sh : It shows the disk usage (size) of a file or directory. Example: du -sh /var/log. To check multiple folders: du -sh *
tail -f : Almost correct. The correct syntax is tail -n 100 -f filename or tail -100f filename (older syntax). tail -f continuously follows new lines added to a file, commonly used for live log monitoring.
pwd          : Show current working directory
ls -ltr      : List files with details, sorted by modification time
cd           : Change directory
touch        : Create an empty file
cat          : Display file contents
less         : View file page by page
head         : Show first few lines of a file
grep         : Search for text in files
find         : Find files and directories
ps -ef       : Show running processes
kill         : Terminate a process
free -h      : Show RAM and swap memory usage
uptime       : Show system uptime and load average
uname -a     : Show kernel and system information
hostname     : Display system hostname
whoami       : Show current logged-in user
chmod        : Change file permissions
chown        : Change file ownership
systemctl    : Manage Linux services
journalctl   : View systemd service logs

-----------------------
types of logs : 

 - info : shows the basic info of the logs
 - debug : shows complete details of the logs (best for finding RCAs)
 - error : it only captures the errors generated
 - warn : these captures only the Warnings generated.
 
----------------------------------------------------------------
VIM (Vi Editor)
Vim (Vi Improved) is a command-line text editor used to create, edit, and manage text files in Linux.
                                                 
 vi <filename>  Opens an existing file or creates a new file if it doesnt exist. 
 i              Enters **Insert Mode** to start editing the file.                 
 Esc            Exits Insert Mode and returns to Command Mode.                    
 :w             Saves the changes without exiting the editor.                     
 :q             Quits the editor (only if no changes are pending).                
 :wq            Saves the file and exits the editor.                              
 :x             Saves (if changes exist) and exits the editor.                    
 :q!            Exits without saving any changes.                                 
 dd             Deletes the current line.                                         
 yy             Copies (yanks) the current line.                                  
 p              Pastes the copied or deleted line.                                
 u              Undoes the last change.                                           
 /text          Searches for the specified text in the file.                      
 n              Moves to the next search result.                                  


-------------------------------------
Users and groups : 

User details are stored in /etc/passwd 
eg: like this 
root:x:0:0:root:/root:/bin/bash
subhan:x:1001:1001:Subhan:/home/subhan:/bin/bash

(username : password placeholder : UID : GID : Description : Home directory : Login shell)     << explaination for the above result 

-- passwords are stored in "/etc/shadow" 
   sudo cat /etc/shadow
   
-- for creating users 
   sudo useradd <username> 
-- to switch user use this command "su - <username>" ; for switching to root  user "sudo -"
-- For setting the password to the user : sudo passwd <user-name>
-- for adding users to the group : sudo usermod -aG <group-name> <user-name>   [ a means append, G is group ]

-- for removing users : sudo userdel <user-name>
-- Removing users from group : sudo gpasswd -d <user> <group-name>
-- for providing sudo access to user : sudo usermod -aG sudo <user-name>

--------------------------------
Permissions 

There are 3 permission categories in linux 
1. User (Owner)   --> owner has maximum access
2. Group          --> think like family, will have limited access
3. Others         --> like guests, will have minimum access

3 types of permissions : 1. Read, 2. Write, 3. Execute 
   Read : r : 4  -> only read access 
   Write : w : 2  -> can read and edit,delete, append the file
   Execute : x : 1 -> execute access 
   
 drwxr-xr-x   -> d - directory, rwx means owners has full permissions, r-x means only read and execute to users, r-x means only read and execute to others 
 
 
Number	    Permission
777	        rwxrwxrwx
755	        rwxr-xr-x
700			rwx------
644			rw-r--r--
600			rw-------
775			rwxrwxr-x
555			r-xr-xr-x
444			r--r--r--


commands for chaning permissions 
 chmod +x <file_name>  adding execute permissions 
 chmod -x <file_name>  removing permissions 
 chmod u+x script.sh  -> adding users execute permisson 
 chmod g+x script.sh
 
u = User (Owner)
g = Group
o = Others
a = All

we can use numeric format as well 

 chmod 777 <file_name> 
 chmod 755 <file_name>
 
 chmod -R 755 project/  -> for chaning the permissions recursively  (i.e: it will applies the same permissons to the sub folders as well ) 
 
 --- for chanign ownership -----
 chown user:group <filename>   eg: chown chandu:sre shellscript.sh 
 chown -R user:group <file_name>  -> for applying the ownership to the sub folders as well.
 
------------------------
package managers

What is a Package?

Think of your mobile phone.

If you want to install WhatsApp, you don't manually download every file required for WhatsApp.
You simply open the Play Store, click Install, and everything is downloaded automatically.

Linux works the same way.
Instead of apps, Linux installs software packages.
Examples of packages: Git,Docker,Java,Python,Nginx,Apache,MySQL

A package contains:

Application files
Configuration files
Libraries (dependencies)
Documentation
Installation scripts

What is a Package Manager?

A Package Manager is a tool that helps you:Install software,Remove software,Update software,Search for software,Manage software dependencies
 Example: Suppose you want to install Google Chrome.
  Without a package manager: Download the installer,Download required libraries,Configure everything manually,Fix errors yourself

  With a package manager:
     sudo apt install git
	 Done! It downloads and installs everything automatically.

  Real World Example

    Imagine a supermarket.
    The supermarket is the Repository.
    The cashier is the Package Manager.
    The products are Packages.
    You tell the cashier: "I want milk."
   The cashier finds it, bills it, and gives it to you.

  Similarly, Linux package managers:
	Find the software
	Download it
	Install dependencies
	Configure it
	Install it
	
Why Do We Need Package Managers?

	Without package managers:
		Download software manually
		Find compatible versions
		Install required libraries manually
		Resolve dependency issues yourself

	With package managers:
      Everything happens automatically.

Popular Package Managers
Linux Distribution	Package Manager
Ubuntu	apt
Debian	apt
CentOS 7	yum
RHEL 7	yum
RHEL 8/9	dnf
Fedora	dnf
SUSE	zypper
Arch Linux	pacman

  #########################
		- APT Package Manager (Ubuntu/Debian)
         APT stands for: Advanced Package Tool
		Used in: Ubuntu,Debian, Linux Mint, Update Package List, sudo apt update

		What happens?
		Linux downloads the latest package information.
		Think of it as refreshing the Play Store.
		Upgrade Installed Packages
		
		- sudo apt upgrade :Updates all installed software to the latest available version.
		- sudo apt install git : Install Software (Example: Install Git)   "sudo apt install <software_name>
		- sudo apt remove git  : Removes the software, configurations file may remain 
        - sudo apt purge git : Remove Completely (Removes: Software, Configuration files)
		- sudo apt search nginx : Searches available packages.
		- sudo apt show git : Displays:	 Version, Description, Dependencies
		- sudo apt list --installed : List Installed Packages
		- sudo apt clean : Clean Downloaded Packages
        - sudo apt autoremove : Removes downloaded package cache,Useful to free disk space.
		
--------------------------
wget -> used for downloading the files from internet 
 eg: wget <url> 
 
-------------------------------------
shell scripting :
files ends with .sh format 
- starting the shellscript we write "#!/bin/bash" represents the bournshell 
- shell script file is nothing, but a set of commands executed one by one in a format, instead of doing them manually 
to execute the shellscript file we use these commands : 
  ./<file_name>.sh or bash ./<file_name>.sh 

-----------------

Cron jobs: this is a schedule task, which can be executed at particular interval of time or at required time 
 crontab -l -> displays current cronjobs 
 crontab -e -> for editing or setting up the cron jobs 
  eg: 0 2 * * * /home/ubuntu/backup.sh   -> cron expression <file name with complete path > 

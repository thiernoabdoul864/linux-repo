Sequence #: 1
name:  Install packages
Example:  
#yum install samba samba-client samba-common cifs-utils

sudo systemctl enable smb
sudo systemctl enable nmb
sudo systemctl start smb
sudo systemctl start nmb  // enable and start samba services 
comments: the above command installs the required packages to configure samba in a linux machine. CIFS  stands for Common Internet File System

Sequence #: 2
name: Create the samba share directory
Example:   mkdir /common 
 chmod  -R 777 /common 
 echo "test file" > /common/testfile
comments: The above comment creates a directory name common inside the /  directory. then we give it full access permission and create a file inside it named testfile using echo and redirect
Sequence #: 3
name: Edit the  /etc/samba/smb.conf file using vim 
Example:  
	vim /etc/samba/smb.conf


[common]
        comment = This is my samba share file
        path = /common
        public = no
        valid users = smb_user
        writable = yes
        printable = no
        browsable = yes
        create mask = 0765
        read only = no


NB: See /etc/samba/smb.conf.example for configuration hints 

comments:  This is going to land us inside the samba configuration file. the first red line is the name of our samba shared directory. the second line is the path of our directory mentioned above. the third is just for a comment, and the last two lines are for the read and write permissions. 
After that, we can test if everything is set up correctly by hitting:
 testparm then enter 
Sequence #: 4 
name: Add samba to firewall, set SELinux context for samba and the setsebool for samba
Example:  
firewall-cmd –add-service=samba  – permanent 
firewall-cmd –reload   // always remember to reload the firewall so changes take effect. 
semanage fcontext -at samba_share_t  “/common(/.*)?”  // setting SELinux context 
restorecon  -Rv  /common   // restoring selinux after making changes - always rember to do that 
getsebool -a | grep samba_export   // checking samba boolean values
getsebool -a | grep samba_share    // checking samba boolean values
setsebool samba_export_all_rw on -P
 setsebool samba_export_all_ro on -P
 setsebool samba_share_nfs on -P
	
comments: In the above lines, we set up the firewall, the SELinux fcontext, and boolean values. 

Sequence #: 5
name:  Create samba user enable it and test it 
Example:  
useradd  smb_user
smbpasswd -a smb_user
sudo smbpasswd -e smb_user 
smbclient -L //localhost -U smb_user   // verify samba share locally 

comments:  This is the end of the server-side samba configuration




------Client Side Configuration ----------
1-/ Install the required packages
# yum install samba-client cifs-utils
2-/ Create user1 with the same uid and gid as in the server
 #useradd -u 1005 smb_user
#passwd smb_user
3-/Connect to server using smbclient
#smbclient -L //192.168.1.50/common -U smb_user
4-/Create a mount point
#mkdir /mnt/samba
5-/ Mount the share temporary
6-/ Create a credential file and mount samba permanently
 a-/ credential
#vim /root/smb.cred 
#chmod 600 /root/smb.cred 
username=smb_user
password=samba 
 b-/ Mount
# vim /etc/fstab

//server_name/common   /mnt/samba cifs  credentials=/root/smb.cred  0 0

------AutoMount for Samba ---------
a-/ Install the required packages
# yum install autofs cifs-utils
b-/ Create a master map file
# vim /etc/auto.master.d/auto.share
/common	/etc/auto.share
c-/Edit the map file
# vim /etc/auto.share
work -fstype=cifs,credentials=/etc/creds.txt	://server1/common

To access the Samba share from Windows Explorer, start typing the IP address to our share in the search area. I am using the hostname of the Samba server. In my case, it is centos . You can also access the share by using the IP address of the Samba server.





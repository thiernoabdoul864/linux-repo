SAMBA

1- Install packages
# yum install samba samba-client samba-common cifs-utils
CIFS (Common Internet File System)
2-/ Create the samba share directory
 # mkdir /myshare
 #chmod 777 /myshare
 #echo "test file" > /myshare/testfile.txt
2- edits the Samba configuration file, located at /etc/samba/smb.conf
# vim smb.conf
[myshare]
 comment = This is our test share
 path = /myshare
 writeable = yes
 browseable = yes
3- Test the configuration file
#testparm
4-/ Open up the firewall ports
#firewall-cmd --permanent --add-service=samba
#firewall-cmd --reload
5-/ Set up selinux context for samba
#semanage fcontext -at samba_share_t "/myshare(/.*)?"
# restorecon -Rv /myshare
6-/ Check on samba boolean values
#getsebool -a | grep samba_export
#getsebool -a | grep samba_share
# setsebool samba_export_all_rw on -P
# setsebool samba_export_all_ro on -P
# setsebool samba_share_nfs on -P
7-/Create a samba user
#useradd user1
# smbpasswd -a user1
8-/ Start and enable smb service (Server Message Block) protocol
# systemctl enable --now smb
9-/ Verify samba share localy 
#smbclient -L //localhost -U user1 

------Client Configuration ----------
1-/ Install the require packages
# yum install samba-client cifs-utils
2-/ Create user1 with the same uid and gid as in the server
#useradd -u 1005 -g1008 user1
#passwd user1
3-/Connect to server using smbclient
#smbclient -L //serverIP/myshare -U user1
4-/Create a mount point
#mkdir /mnt/share
5-/ Mount the share temporary
mount -t cifs //serverIP/myshare /mnt/share -o username=user1,pass
word=school1,uid=1004,gid=1004
6-/ Create a credential file and mount samba permanently
 a-/ credential
#vim /etc/creds.txt
#chmod 600 /etc/creds.txt
user = user1
password = online1
 b-/ Mount
# vim /etc/fstab
//IP/myshare /mnt/share cifs rw,credentials=/etc/creds.txt 0 0


------AutoMount for Samba ---------
a-/ Install the require packages
# yum install autofs cifs-utils
b-/ Create a master map file
# vim /etc/auto.master.d/auto.share
/myshare	/etc/auto.share
c-/Edit the map file
# vim /etc/auto.share
work -fstype=cifs,credentials=/etc/creds.txt	://server1/myshare

To access the Samba share from Windows Explorer, start typing the IP address to our share in the search area. I am using the hostname of the Samba server. In my case, it is centos . You can also access the share by using the IP address of the Samba server.


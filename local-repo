#### How to configure local repo in rhel 8
## Yum install httpd createrepo yum-utils -y 
## Cd /var/www/html && mkdir repos 
## Systemctl enable - - now httpd 
## Firewall-cmd –permanent –add-port=80/tcp && firewall-cmd –reload 
## yum repolist   //Note: base os and app stream repo id’s 
## yum reposync -g -m –repoid=rhel-8-x86_64-appstream-rpms  
## –newest-only –download-metadata –download-path=/var/www/html/repos
#above command synchronize http repositories 
## yum reposync -g -m –repoid=rhel-8-for-x86_64-baseos-rpms 
## –newest-only –download-metadata –download-path=/var/www/html/repos
## createrepo  /var/www/html    // turning directory into a repository 

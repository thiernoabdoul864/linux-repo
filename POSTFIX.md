# Introduction to Mail Server

A mail server is used to send and receive mails between the systems in a network. Configuring your own Linux mail server is reliable and also one of the importants tasks, system administrator should know. Among the other agents, POSTFIX is considered to be the most easy and reliable option available. POSTFIX is an open source Mail Transfer Agent(MTA) responsible for sending and receiving mails over a network. Hence, it is mandatory that POSTFIX must be present in a system that has to server as a Mail server.

# Basic information about Postfix

`Package: postfix `
`Daemon: postfix`                                                    `Document root: /etc/postfix`
`Configuration file: /etc/postfix/main.cf`

# Configuring Postfix
Follow the below steps to conifgure a Postfix mail server in your Linux system.

# Step 1: Install the package
"postfix" package has to be installed in the server using yum.

## `yum install -y postfix`
# Step 2: Start and enable the service
Start and enable the "postfix" service.

## `systemctl start postfix`
## `systemctl enable postfix`
# Step 3: Edit the configuration file
The configuration file of postfix in `/etc/postfix/main.cf`. There are a list of changes that have to be done in the configuration file.

# i) Edit the hostname of the mail server at Line.no 75.

## `myhostname = nameserver.example.com`
# ii) Uncomment and add the domain name of the mail server at Line.no 83

## `mydomain = example.com`
# iii) Uncomment Line.no 99 and 113

## `myorigin = $mydomain` --> Line.no99
## i`net_interfaces = all` --> Line.no113
# iv) Edit the Line.no 119 as follows:

## `inet_protocols = all`
# v) Comment Line.no 164

## `mydestination = $myhostname, localhost.$mydomain, localhost`
# vi) Uncomment Line.no 264 and the IP Network Address.

## `mynetworks = 192.168.10.0/24, 127.0.0.0/8`
# vii) Uncomment Line.no 419

## `home_mailbox = Maildir/`
Once these changes are done, save and quit the file.

# Step 4: Start and enable the service
Start and enable the Postfix service.

## `systemctl start postfix`
## `systemctl enable postfix`

# Step 5: Check the status
Check the status of the postfix service to ensure it is running.

## `systemctl status postfix`
# Step 6: Send a mail
Now, you can send mail to any users of the machines in the network. The following  command send a mail to user "Akshat" in client1.infy.com.

##  `echo "Hi Akshat!" | mail -s "Greeting" akshat@client1.example.com`
The mail can be checked in the inbox of th user, which is /var/spool/mail/akshat where the bit after /mail is the name of the user.
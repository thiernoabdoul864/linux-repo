# Setting up Secondary DNS or Slave DNS Servers

**NB:** Let us assume to have a master DNS server and two Slave DNS servers set up as follows:

### Master DNS Server Information:
- **Name:** www
- **DNS Domain:** homelab.local
- **IP Address:** 192.168.1.8

### Slave DNS Servers:
#### Server1:
- **Name:** rhel8-cli1
- **IP Address:** 192.168.1.18

#### Server2:
- **Name:** rhel8-cli2
- **IP Address:** 192.168.1.28

---

1. **Assuming that the master DNS server is already set up, let us make a small change in the master main config file to allow it to work with slaves.**

2. **In the master machine, `vim` into `/etc/named.conf` and inside the forward zone, add the following line:**
    ```conf
    allow-transfer { 192.168.1.18;  192.168.1.28; };
    ```
    **Those are the IP addresses of the two slave DNS servers. Note the spaces around and between IP addresses. Omitting them will prevent it from working properly.**

3. **After saving the changes, restart the named daemon. Now move to the slave DNS servers.**

4. **Now we are in the first slave DNS server. Ensure it is connected to the internet and that it is configured to install packages.**

5. **Using the below command, install the required packages as follows:**
    ```bash
    yum install bind bind-utils -y
    ```

6. **Then enable the named daemon:**
    ```bash
    systemctl enable named
    ```

7. **Then, `vim` into `/etc/named.conf` file and in the options section, on top of the file add/modify the below lines as follows:**
    ```conf
    listen-on port 53 { 127.0.0.1; 192.168.1.18; };
    allow-query { localhost; 192.168.1.0/24; };
    ```
    **Note that the `192.168.1.0/24` is the network address.**

8. **In the forward zone section, at the bottom of the file, add the below code:**
    ```conf
    zone "homelab.local" {
        type slave;
        file "/slaves/forward.db";
        masters { 192.168.1.8; };
    };
    ```

9. **When done, restart named and check if it has worked by `cd` inside `/var/named/slaves`. The `forward.db` file will be automatically copied.**

10. **Do the same on the second slave DNS server, and if there is a third one, the process is the same.**

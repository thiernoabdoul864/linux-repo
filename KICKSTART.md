#How to automatically build a server Using kickstart and httpd server 
1.configure httpd server 2.Mount the / dev / sr0 device permanently into / mnt
and create a soft link inside / var / www / html called dvd
and pointing to / mnt - changer permissions to both items inside / var / www / html to rw - r --r-- 
2.copy the anaconda file inside the / var / www / html / kickstart.cfg 3.
modify that copy by adding the below lines - url --url=http://ip_address_of_current_machine/dvd 
    - eula --agreed
    - firstboot --disable
    - reboot 5.Make sure http is added to firewall
    and verify that items are accessible
from an external browser using http: // ip_address / item 6.crete the client machine
    and perform the basic settings,
    then start the mahine.7.At machine startup,
    hit tab
    and enter: inst.ks = http: // ip_add / kickstart.cfg then hit enter.8.If everything works fine,
    no more manual intervention till server is ready.Below is an example of a ready edited kickstart file ! [Alt text](image.png)
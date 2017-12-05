# System-Integration2

**A client/server system will be setup with the following installed:**

DNS server
DHCP server
NFS server
FTP server

**Configuration is as follows:**

**DHCP Server:**

On the server, install the DHCP server by running the command "sudo apt-get install isc-dhcp-server".
Once this is installed edit the files "/etc/default/isc-dhcp-server" and "/etc/dhcp/dhcpd.conf" with the relevent information on youre machines.
On the client side, edit the "/etc/network/interfaces" file and change ethernet port 1 (eth1) to dhcp from static

**FTP Server:**

On the server, install FTP using the command "sudo apt-get install vsftpd".
On the client, install FTP using the command "sudo apt-get install ftp".
Edit the "/etc/vsftpd.conf" file and add a link to the clients IP so the client can access directories on the server.
Add or edit these lines to be equal to this in the above file:
anonymous_enable=YES
no_anon_password=YES
anon_root=/home/FTP/

**NFS:**

Install nfs on the client and server by running the commands "sudo apt-get install nfs-kernel-server" and "sudo apt-get install nfs-common".
Create an NFS directory on the server.
In the file "/etc/exports" on the server add the line "/home 192.168.1.150(rw,sync,no_root_squash,no_subtree_check)" to allow the IP address of the client to access the directories on the server.
Run the command "sudo exportfs -a" and restart the NFS service with: "sudo service nfs-kernel-server start".
Moving the client we need to mount the server with the following commands; "sudo mount 1.2.3.4:/home /mnt/nfs/home" and "sudo mount 1.2.3.4:/var/nfs /mnt/nfs/var/nfs".

**DNS:**

On the server, install bind9 with: "sudo apt-get install bind9".
Open the file "/etc/bind/named.conf.options" and add the lines "8.8.8.8" and "8.8.4.4" to the forwarders.
Restart bind with the command: "sudo service bind9 restart".
In the file "/etc/resolv.conf" change the first nameserver line to the IP of your server machine.
Use the dig command with the site "www.example.lan" as in the command "dig www.example.lan".
Run this command a second time and ensure that the query time drops as this shows it's coming locally.
Edit the files "/etc/bind/db.example.lan" and "/etc/bind/db.192" with the relevent server information for your server machine.
Restart the service using the command "sudo service bind9 restart".
Test the lookup with the command "nslookup www.example.lan".
The command should return with relevant information about the DNS server

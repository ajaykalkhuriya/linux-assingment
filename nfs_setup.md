

///Setting up the host server

Install NFS Kernel Server

$ sudo apt-get update

$ sudo apt install nfs-kernel-server

///Create the Export Directory

$ sudo mkdir -p /mnt/sharedfolder


all clients to access the directory, we will remove restrictive permissions 

$ sudo chown nobody:nogroup /mnt/sharedfolder


$ sudo chmod 777 /mnt/sharedfolder

Assign server access to client(s) through NFS export file

$ sudo nano /etc/exports

you have opened the file, you can allow access to:

A single client by adding the following line in the file:
/mnt/sharedfolder clientIP(rw,sync,no_subtree_check)

Multiple clients by adding the following lines in the file:
/mnt/sharedfolder client1IP(rw,sync,no_subtree_check)
/mnt/sharedfolder client2IP(rw,sync,no_subtree_check)

Multiple clients, by specifying an entire subnet that the clients belong to:
/mnt/sharedfolder subnetIP/24(rw,sync,no_subtree_check)


 Export the shared directory:

 $ sudo exportfs -a

 restart nfs kernal server

 $sudo systemctl restart nfs-kernel-server

 if firewall active the allow firewall for client ip otherwise leave it if firewall is inactive

 $ sudo ufw allow from [clientIP or clientSubnetIP] to any port nfs

check firewall status

$ sudo ufw status




Configuring the Client Machine-----

insatll nfs common

$ sudo apt-get install nfs-common

Create a mount point for the NFS host’s shared folder


$ sudo mkdir -p /mnt/sharedfolder_client

Mount the shared directory on the client


$ sudo mount serverIP:/exportFolder_server /mnt/mountfolder_client


done!

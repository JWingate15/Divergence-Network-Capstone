# Stage 5 Overview & Topology

In Stage 5, we added a new win2012r2 server, 1) prepared the win2012r2 server, and 2) installed file transfer protocol (FTP) service. 

**1) Preparing win2012r2 server**

    hostname: ftp
    ip address: 10.128.10.21
    subnet mask: 255.255.255.0
    default gateway: 10.128.10.1
    DNS1: 10.128.0.10
    DNS2: 10.128.10.1
    NTP sync with: dc.widgets.localdomain

After all of the above, join to the widgets domain.

**2) Install FTP service**

We followed the following guide : https://learn.microsoft.com/en-us/archive/technet-wiki/12364.windows-server-2012-ftp-installation

**Stage 5 Starting Topology**
![Stage 4 Topology](https://github.com/JWingate15/Divergence-Network-Capstone/blob/main/Stage%204%20Overview%20%26%20Topology/Stage%204%20Topology.drawio.png)


**Stage 5 Ending Topology**
![Stage 5 Topology](https://github.com/JWingate15/Divergence-Network-Capstone/blob/main/Stage%205%20Overview%20%26%20Topology/Stage%205%20Topology.drawio.png)

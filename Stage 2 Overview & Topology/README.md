# **Stage 2 Overview and Topology**

During this stage, we built a Windows domain for the client's small business environment by conducting the following: 1) preparing a Win2012r2 server for Active Directory Domain services role, 2) installing the Active Directory Domain Services server role, 3) creating new Active Directory user accounts, 4) joining Win10 to widgets.localdomain domain, and 5) setting the desktop background on Win10 with group policy from the domain controller (dc). 

**1) Preparing a Win2012r2 server for the Active Directory Domain Services server role**

Active Directory (AD) is a directory service (ds) that runs on Microsoft Windows Server and is used for identity and access management. AD DS stores and organizes information about the people, devices, and services connected to a network. AD DS serves as a locator service for those objects and as a way for organizations to have a central point of administration for all activity on the corporate network.

After logging into the server as the administrator, we went to *Windows Server Manager > Local Server > Ethernet Instance 0 > Properties* and established a static IP address by inputting the following settings:

    ip address: 10.XXX.X.X
    subnet mask: 255.XXX.XXX.0
    default gateway: 10.XXX.X.X
    DNS1: 127.X.X.X
    DNS2: 10.XXX.X.X

Next, we tested networking connectivity by pinging LAN, WAN, and DNS.

    LAN - 10.128.0.1
    WAN - 8.8.8.8
    DNS - google.com
    
Lastly, we configured the network time protol (NTP) and changed the host name of the server to dc.

**2) Install the Active Directory Domain Services server role**

First, we downloaded and installed Windows updates for the server before installing the Directory Services role by accessing *Server Manager > Local Server > Manage > then Add Roles and Features*. We checked off "Active Directory Domain Services" in the Server Roles option to install the AD binaries before clicking "Promote this server to a domain controller" link. 

**3) Create new AD user accounts**

Utilizing the Active Directory we just established, we created admin and user accounts for each team member ut following this example format:

    example user: Ashley Williams
    user account: u-awilliams
    admin account: a-awilliams

Each team member's admin account was added to the group 'Domain Admins'. 

**4) Join Win10 to the widgets.localdomain domain**

We papred the Win10 workstation to join the domain by implementing the following changes:

    Change the hostname to win10, then reboot.
    Change the primary DNS server to the IP for the DC.
    Set NTP to sync with dc.widgets.localdomain

To join the Win10 computer to the widgets.localdomain, we did the following steps:

    On the Desktop, click the Start button, type Control Panel, and then press ENTER.
    Navigate to System and Security, and then click System.
    Under Computer name, domain, and workgroup settings, click Change settings.
    Under the Computer Name tab, click Change.
    Under Member of, click Domain, type the name of the domain that you wish this computer to join, and then click OK.
    Click OK in the Computer Name/Domain Changes dialog box, and then restart the computer.

**5) setting the desktop background on Win10 with group policy from the dc**

We edited the default domain policy by completing the following:

    On the dc, login and open the Group Policy Management Console, edit the Default Domain Policy.
    Set the desktop image to:
    c:\windows\web\wallpaper\windows\img0.jpg
    Close the Group Policy Management Editor when you are done.

**Stage 2 Beginning Topology**

![Stage 1 Topology](https://github.com/JWingate15/Divergence-Network-Capstone/blob/main/Stage%201%20Overview%20%26%20Topology/Stage%201%20Topology.drawio.png)

**Stage 2 Ending Topology**

![Stage 2 Topology](https://github.com/JWingate15/Divergence-Network-Capstone/blob/main/Stage%202%20Overview%20%26%20Topology/Stage%202%20Topology.drawio.png)


    


# Stage 3 Overview and Topology

During this stage, 1) we built an Internet Information Services (IIS) server and prepared it to join the domain, 2) installed the IIS server role, and 3) added a test webapge to verify access over the LAN network.

**1) Preparing an IIS to join the domain**

We prepared the IIS server utilizing the following information:

    hostname: iis
    ip address: 10.XXX.X.XX
    subnet mask: 255.XXX.XXX.X
    default gateway: 10.XXX.X.X
    DNS1: 10.XXX.X.XX
    DNS2: 10.XXX.X.X
    NTP sync with: dc.widgets.localdomain
    
    After all of the above, join to the widgets domain.

**2) Install IIS server role**

We installed the server following Microsoft's guide for installing IIS 8.5 on Win2012r2 server (link below). 

https://learn.microsoft.com/en-us/iis/install/installing-iis-85/installing-iis-85-on-windows-server-2012-r2#install-iis-85-for-the-first-time-in-the-server-manager


After you've setup IIS, open Internet Explorer and add http://localhost/ [http://localhost/] to the Trusted Sites list. You should be able to verify the site is working after that.

**3) Add a test webpage, and verify access over the LAN network**

We created a test webpage on IIS by completing the following steps:

    Open notepad and add the following text:
    <html>
    <head>
    <title> IIS test validation website</title>
    </head>
    <body>
    <p>test website validation completed</p>
    </body>
    </html>
    
    Save the file to your documents folder:
    filename: test.html
    
    Copy the file from your documents folder to:
    c:\inetpub\wwwroot\test.html
    
    Test in the local browser on IIS.
    http://localhost/test.html


**Stage 3 Starting Topology**

![Stage 2 Topology](https://github.com/JWingate15/Divergence-Network-Capstone/blob/main/Stage%202%20Overview%20%26%20Topology/Stage%202%20Topology.drawio.png)

**Stage 3 Ending Topology**

![Stage 3 Topology](https://github.com/JWingate15/Divergence-Network-Capstone/blob/main/Stage%203%20Overview%20%26%20Topology/Stage%203%20Topology.drawio.png)



    


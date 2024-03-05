# Stage 4 Overview & Topology

During Stage 4, we 1) added and configured an Unbuntu Linux + Apache + MySQL + PHP/Perl/Python (LAMP) server, 2) installed DokuWiki, 3) configured DokuWiki and 4) established a virtual IP (VIP) for the public side of the LAMP server on the the firewall.  

**1) Configuring the Ubuntu LAMP server**

*Start Ubuntu*
    username = gns3
    password = gns3

*Configure the network settings*

    ip = 10.XXX.XX.XX
    netmask = 255.XXX.XXX.0
    gateway = 10.XXX.XX.X
    dns = 10.XXX.X.XX,10.XXX.XX.X

*Update the hosts file*

    127.X.X.X localhost.localdomain localhost
    10.XXX.XX.XX www.widgets.localdomain www

*Set hostname with hostnamectl*

    hostnamectl set-hostname www
    hostnamectl

*Update the packages on the server*

    apt update -y
    apt upgrade -y
    apt dist-upgrade -y
    apt autoremove -y
    apt autoclean -y
    systemctl reboot

**2) Install DokuWiki**

*Install DokuWiki*

    apt install php php-gd php-xml php-json -y
    systemctl enable --now apache2
    ufw allow Apache
    wget https://download.dokuwiki.org/src/dokuwiki/dokuwiki-stable.tgz
    mkdir /var/www/html/dokuwiki
    tar xzf dokuwiki-stable.tgz -C /var/www/html/dokuwiki/ --strip-components=1

*Create the config file for the DokuWiki*

    nano /etc/apache2/sites-available/dokuwiki.conf

*Add the following, keep the tabbed spacing*

    <VirtualHost *:80>
            ServerName www.widgets.localdomain
            DocumentRoot /var/www/html/dokuwiki

            <Directory ~ "/var/www/html/dokuwiki/(bin/|conf/|data/|inc/)">
               <IfModule mod_authz_core.c>
                  AllowOverride All
                  Require all denied
               </IfModule>
               <IfModule !mod_authz_core.c>
                   Order allow,deny
                   Deny from all
               </IfModule>
            </Directory>

            ErrorLog /var/log/apache2/dokuwiki_error.log
            CustomLog /var/log/apache2/dokuwiki_access.log combined
    </VirtualHost>


Save and exit

*Finish the config*

    cp /var/www/html/dokuwiki/.htaccess{.dist,}
    chown -R www-data:www-data /var/www/html/dokuwiki
    apache2ctl -t
    a2dissite 000-default.conf
    a2ensite dokuwiki.conf
    systemctl reload apache2

*Verify access to the installer*

***Create a host (A) record in DNS on the DC***

Log onto the DC

Open DNS Manager

Under the Forward Lookup Zones, add a new host (A) record to the widgets.localdomain domain

    name = www
    ip address = 10.128.10.80
    create associated pointer (PTR) record = unchecked
    add host

***From win10, open the dokuwiki installer url in the browser:***

    http://www.widgets.localdomain/install.php

**3) Configure DokuWiki

*From win10, open the dokuwiki installer url in the browser:*

     http://www.widgets.localdomain/install.php
     wiki name = Widgets Network Documentation Wiki
     superuser = wikiadmin
     real name = service account
     e-mail = wikiadmin@widgets.localdomain
     password = XXXXXXX
     initial ACL policy = Public Wiki

*Rename the install on www*

    mv /var/www/html/dokuwiki/install.php /var/www/html/dokuwiki/install.php.removed

*Login to the Wiki*

    On Win10, open the wiki url and login.
    http://www.widgets.localdomain/
    user = wikiadmin
    password = XXXXXXXX

*Document the network*

    ====== Welcome to the widgets.localdomain Wiki! ======
    This wiki will be used to document the network resources for the Widgets environment.\\
    firewall
    hostname = firewall
    FQDN = firewall.widgets.localdomain (needs to be created on dc)
    a-record created = not yet
    network info:
      wan is port1 on dhcp from cloud, connected to WAN-SWITCH
      lan is port2 on 10.XXX.XX.X/XX, connected to LAN-SWITCH
      dmz is port4 on 10.XXX.XX.X/XX, connected to DMZ-SWITCH
      guest is port3 on 10.XXX.XX.X/XX, not connected
    win10
      hostname = win10
      FQDN = win10.widgets.localdomain
      a-record created = dynamically on dc.widgets.localdomain
      network info: dhcp, LAN network
    dc
      hostname = dc
      FQDN = dc.widgets.localdomain
      a-record created = automatically on dc.widgets.localdomain
      network info: static, 10.XXX.XX.X/XX, LAN network
      services: AD and DNS services
    iis
      hostname = iis
      FQDN = iis.widgets.localdomain (needs to be created on dc)
      a-record created = not yet
      network info: static, 10.XXX.XX.X/XX, LAN network
      services: webserver
    www
      hostname = www
      stage4-instructions-configure-docuwiki [ntt-wiki] 1/25/24, 7:53 PM
      http://ntt-wiki.dvg.local/doku.php?id=stage4-instructions-configure-docuwiki Page 6 of 6
      FQDN = www.widgets.localdomain
      a-record created = static on dc.widgets.localdomain
      network info: static, 10.XXX.XX.X/XX, DMZ network
      services: webserver, wiki

**4) Create a VIP on the firewall**

Go to Policy & Objects > Virtual IPs > Create New Virtual IP

    name = www_tcp_80
    interface = WAN
    mapped IP = 10.XXX.XX.XX
    port forwarding = enabled
    external service port = 80
    map to port = 80

**Stage 4 Starting Topology**
![Stage 3 Topology](https://github.com/JWingate15/Divergence-Network-Capstone/blob/main/Stage%203%20Overview%20%26%20Topology/Stage%203%20Topology.drawio.png)

**Stage 4 Ending Topology**
![Stage 4 Topology](https://github.com/JWingate15/Divergence-Network-Capstone/blob/main/Stage%204%20Overview%20%26%20Topology/Stage%204%20Topology.drawio.png)


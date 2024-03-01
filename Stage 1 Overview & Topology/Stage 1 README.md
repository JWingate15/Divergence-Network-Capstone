### Stage 1 Overview & Topology

During stage 1, the "client" requested for our team to add a local area network (LAN),a demilitarized zone (DMZ), and a Win10 workstation to their existing network. These networks were built utilizing a FortiNet firewall. After the completion of Stage 1, we added a FortiNet firewall, two Ethernet switches (LAN and DMZ), and a Wind10 workstation to the lab space.

**LAN Configuration**
The client requested LAN was configured through the command line interface (CLI) of the FortiNet firewall console. 
The LAN was configured utilizing the following commands:

      conf sys int 

         edit port2

         set allowaccess ping http https ssh

         set ip 10.XXX.X.X/XX 
      end

**DHCP Configuration**
Dynamic host configuration protocol (DHCP) is a network management protocol used on Internet Protocol networks for automatically assigning IP addresses to devices connected to the network using a client–server architecture.

The DHCP server was configured utilizing the following commands:

conf sys dhcp server 
    
        edit 1
       
        set default-gateway 10.XXX.X.X 
        
        set netmask 255.XXX.XXX.X
       
        set interface port2
        
        config ip-range
             
             edit 1
                
                 set start-ip 10.XXX.X.XXX 
                 
                 set end-ip 10.XXX.X.XXX
            
             next 
         
         end

**Windows10 Workstation Configuration**
Next, we validated the Win10 workstation had leased a DHCP address from the LAN network with the following commands:

valid IP range: 10.XXX.X.[XXX-XXX]/XX 

gateway: 10.XXX.X.X

DHCP server: 10.XXX.X.X

*We then tested network connectivity by pinging LAN, WAN, and DNS with the following commands:*

LAN - 10.XXX.X.X 

WAN - 8.8.8.8 

DNS - google.com


**Complete Network Setup through firewall graphical user interface (GUI)**
During this step, we accomplished the following tasks: 1) we backed up the firewall config, 2) configured network interfaces (DMZ, guest, LAN, & WAN), 3) enabled DNS, 4) configured the firewall system DNS, 5) configured DNS for network interfaces (DMZ, guest, and LAN), 6) created service objects for LAN & DMZ services, 7) configured firewall rules (LAN-to-WAN policy, DMZ-to-WAN policy, LAN-to-DMZ policy, DMZ-to-LAN policy, & WAN-to-DMZ policy), and 8) backed up the firewall configuration an additional time. 

2)***Network interfaces were configured as the following utilizing the following commands:***

**port1 WAN**

    edit port1
          alias = WAN
          role = WAN
      #APPLY-THE-CHANGES

**port2 LAN**

*10.XXX.X.X/24 as the LAN network* 

     edit port2
             alias = LAN
             role = LAN
             create address object matching subnet = enabled
             administrative access = https, http, ping, ssh
             dns server = same as interface IP
             expand advanced
                 ntp server = local
      #APPLY-THE-CHANGES

**port3 Guest**

*10.XXX.XX.X/24 as the GUEST network* 
 
    edit port3
          alias = GUEST
          role = LAN
          ip/network mask = 10.128.99.1/24
          create address object matching subnet = enabled
          administrative access = ping, ssh
          dhcp server = enabled
          dns server = same as interface IP
          expand advanced
              ntp server = local
      #APPLY-THE-CHANGES

**port4 DMZ**

*10.XXX.XX.X/24 as the DMZ network*

      edit port4
          alias = DMZ
          role = DMZ
          ip/network mask = 10.128.10.1/24
          create address object matching subnet = enabled
          administrative access = ping
      #APPLY-THE-CHANGES

3) *DNS was enabled via the following:*
Enable DNS under: System > Feature Visibility
dns database = enabled
  #APPLY-THE-CHANGES

4) *Configure the firewall system DNS*
Configure DNS settings under: Network > DNS
dns servers = specify
  primary dns server = 8.8.8.8
  secondary dns server = 1.1.1.1
  #APPLY-THE-CHANGES

5) *Configure Network DNS*




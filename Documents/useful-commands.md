Cisco Network Troubleshooting & Configuration Guide
📌 Troubleshooting Commands
Interface & IP Information
show ip interface brief – Display interface designations, IP addresses, and status.

show vlan brief – Show VLANs, names, and assigned ports.

show ip route – Display the routing table.

show ip route connected – Show routing table entries for directly connected networks.

show ip route static – Show static route entries.

show ip route ospf – Show OSPF-learned routes.

show ip route eigrp – Show EIGRP-learned routes.

CDP & Neighbor Discovery
show cdp neighbors – Display directly connected Cisco devices.

show cdp neighbors detail – Includes IP address of the other end.

show cdp interface – Show interfaces running CDP.

VLAN & Trunking
show interface trunk – Display trunking ports, native VLAN, and allowed VLANs.

show mac-address-table – Display MAC address table.

Configuration & Version Info
show running-config – Display the active running configuration.

show startup-config – Display the saved startup configuration.

show version – Show IOS version, capabilities, memory, and configuration-register.

show flash – List files and directories in Flash memory.

Debugging & Monitoring
debug ??? – Enable real-time debugging (Use cautiously).

debug all – Enable all debugging (VERY resource-intensive!).

undebug all – Turn off all debugging commands.

show processes – Display active router processes.

show process cpu – Display CPU statistics.

show memory – Show memory allocation.

🎯 Essential Port Numbers
Protocol	Port
FTP (Control)	TCP 21
FTP (Data)	TCP 20
SSH	TCP 22
Telnet	TCP 23
SMTP	TCP 25
DNS	TCP/UDP 53
DHCP (Client to Server)	UDP 67
DHCP (Server to Client)	UDP 68
HTTP	TCP 80
POP3	TCP 110
NTP	UDP 123
SNMP	UDP 161
HTTPS	TCP 443
🔧 Basic Router & Switch Configuration
Reset to Factory Defaults
delete vlan.dat – Reset VLAN configuration (Switch Only).

erase startup-config – Erase saved configuration.

reload – Restart the device.

Basic Setup
configure terminal
hostname Router1
service password-encryption
no ip domain-lookup
banner motd "Authorized Users Only!"
line console 0
password cisco
login
logging synchronous
exec-timeout 0 0
Assign IP Address (Router Interface)
interface GigabitEthernet0/0
ip address 192.168.1.1 255.255.255.0
description Link to LAN
no shutdown
🌐 VLANs, Trunking & Inter-VLAN Routing
Create & Assign VLAN
vlan 10
name Management
interface FastEthernet0/1
switchport mode access
switchport access vlan 10
Configure Trunk Port
interface GigabitEthernet0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,99
switchport trunk native vlan 99
Router-on-a-Stick (Inter-VLAN Routing)
interface GigabitEthernet0/0
no ip address
interface GigabitEthernet0/0.10
encapsulation dot1q 10
ip address 192.168.10.1 255.255.255.0
interface GigabitEthernet0/0.20
encapsulation dot1q 20
ip address 192.168.20.1 255.255.255.0
🔄 Routing Protocols
Static Routing
ip route 0.0.0.0 0.0.0.0 192.168.1.254
OSPF Configuration
router ospf 1
network 192.168.1.0 0.0.0.255 area 0
router-id 1.1.1.1
default-information originate
EIGRP Configuration
router eigrp 100
network 192.168.1.0 0.0.0.255
no auto-summary
🏠 DHCP & NAT
Configure DHCP
ip dhcp pool LAN
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
dns-server 8.8.8.8
lease 7
Configure NAT
interface GigabitEthernet0/0
ip nat inside
interface Serial0/0/0
ip nat outside
ip nat inside source list 1 interface Serial0/0/0 overload
access-list 1 permit 192.168.1.0 0.0.0.255
🔒 Security Configurations
Enable SSH
hostname Router1
ip domain-name example.com
crypto key generate rsa
ip ssh version 2
line vty 0 4
transport input ssh
login local
Port Security
interface FastEthernet0/1
switchport mode access
switchport port-security
switchport port-security maximum 5
switchport port-security violation restrict
ACL Example
ip access-list standard BLOCK_HOST
deny 192.168.1.100
permit any
interface GigabitEthernet0/1
ip access-group BLOCK_HOST in
📡 Spanning Tree & HSRP
Spanning Tree Configuration
spanning-tree mode rapid-pvst
spanning-tree vlan 10 root primary
HSRP Configuration
interface GigabitEthernet0/1
standby 1 ip 192.168.1.254
standby 1 priority 110
standby 1 preempt
🛠 This guide provides fundamental troubleshooting and configuration commands for Cisco routers and switches.


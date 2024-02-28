```bash
# FIREWALL SETTINGS EXAMPLE
# Enable all pings
set firewall all-ping 'enable'
# Disable broadcast pings
set firewall broadcast-ping 'disable'
# Disable SNMP config trap
set firewall config-trap 'disable'
# Disable IPv6 redirects
set firewall ipv6-receive-redirects 'disable'
set firewall ipv6-src-route 'disable'
# Disable IP source routing
set firewall ip-src-route 'disable'
# Log Martian packets
set firewall log-martians 'enable'
# Default actions for named firewall policies
set firewall name all-all default-action 'accept'
set firewall name lan-loc default-action 'accept'
set firewall name lan-wan default-action 'accept'
set firewall name loc-lan default-action 'accept'
set firewall name loc-wan default-action 'accept'
set firewall name wan-lan default-action 'reject'
set firewall name wan-loc default-action 'reject'
# Firewall rules for LAN-WAN traffic
set firewall name lan-wan rule 100 action 'accept'
set firewall name lan-wan rule 100 protocol 'icmp'
set firewall name lan-wan rule 200 action 'accept'
set firewall name lan-wan rule 200 description 'IPSEC Access'
set firewall name lan-wan rule 200 destination address '10.0.0.0/21'
set firewall name lan-wan rule 300 action 'accept'
set firewall name lan-wan rule 300 protocol 'tcp'
set firewall name lan-wan rule 300 source port '179'
# Firewall rules for WAN-LAN traffic
set firewall name wan-lan rule 200 action 'accept'
set firewall name wan-lan rule 200 description 'IPSEC Access'
set firewall name wan-lan rule 200 protocol 'tcp'
set firewall name wan-lan rule 200 source address '10.0.0.0/21'
set firewall name wan-lan rule 300 action 'accept'
set firewall name wan-lan rule 300 protocol 'tcp'
set firewall name wan-lan rule 300 source port '179'
# Firewall rules for WAN-LOC traffic
set firewall name wan-loc rule 100 action 'accept'
set firewall name wan-loc rule 100 destination port '2222'
set firewall name wan-loc rule 100 protocol 'tcp'
set firewall name wan-loc rule 110 action 'accept'
set firewall name wan-loc rule 110 protocol 'icmp'
set firewall name wan-loc rule 200 action 'accept'
set firewall name wan-loc rule 200 destination port '179'
set firewall name wan-loc rule 200 protocol 'tcp'
# General firewall settings
set firewall receive-redirects 'disable'
set firewall send-redirects 'enable'
set firewall source-validation 'disable'
set firewall state-policy established action 'accept'
set firewall state-policy invalid action 'reject'
set firewall state-policy related action 'accept'
set firewall syn-cookies 'enable'
set firewall twa-hazards-protection 'disable'

# INTERFACE SETTINGS
# Configure Ethernet interfaces and their addresses
set interfaces ethernet eth0 address '172.16.7.254/21'
set interfaces ethernet eth0 description 'LAN'
set interfaces ethernet eth0 hw-id '0c:53:d4:98:00:00'
set interfaces ethernet eth0 vif 2 address '10.0.0.254/24'
set interfaces ethernet eth0 vif 3 address '10.0.1.254/24'
set interfaces ethernet eth0 vif 4 address '10.0.2.254/24'
set interfaces ethernet eth1 address '172.17.0.254/16'
set interfaces ethernet eth1 description 'WAN'
set interfaces ethernet eth1 hw-id '0c:53:d4:98:00:01'
# Other Ethernet interface hardware IDs
set interfaces ethernet eth2 hw-id '0c:53:d4:98:00:02'
set interfaces ethernet eth3 hw-id '0c:53:d4:98:00:03'
set interfaces ethernet eth4 hw-id '0c:53:d4:98:00:04'
set interfaces ethernet eth5 hw-id '0c:53:d4:98:00:05'
# Loopback interface
set interfaces loopback lo

# NAT SETTINGS
# NAT rules to masquerade private addresses
set nat source rule 100 description 'Interent Access'
set nat source rule 100 outbound-interface 'eth1'
set nat source rule 100 source address '172.16.0.0/21'
set nat source rule 100 translation address 'masquerade'
set nat source rule 110 outbound-interface 'eth1'
set nat source rule 110 source address '10.0.0.0/24'
set nat source rule 110 translation address 'masquerade'
set nat source rule 120 outbound-interface 'eth1'
set nat source rule 120 source address '10.0.1.0/24'
set nat source rule 120 translation address 'masquerade'
set nat source rule 130 outbound-interface 'eth1'
set nat source rule 130 source address '10.0.2.0/24'
set nat source rule 130 translation address 'masquerade'

# ROUTING SETTINGS
# BGP configuration and static routes
set protocols bgp 65002 address-family ipv4-unicast network 172.16.0.0/21
set protocols bgp 65002 neighbor 192.168.122.51 remote-as '65001'
set protocols bgp 65002 neighbor 192.168.122.51 update-source 'eth1'
set protocols static interface-route 10.0.0.0/24 next-hop-interface eth1
set protocols static interface-route 10.0.1.0/24 next-hop-interface eth1
set protocols static interface-route 10.0.2.0/24 next-hop-interface eth1
set protocols static route 0.0.0.0/0 next-hop 172.17.0.1
set protocols static route 10.0.1.0/24 next-hop 172.17.0.254

# DNS SETTINGS
# DNS forwarding configuration
set service dns forwarding allow-from '10.0.0.0/21'
set service dns forwarding listen-address '172.16.7.254'
set service dns forwarding name-server '9.9.9.9'
set service dns forwarding name-server '1.1.1.1'
set service dns forwarding name-server '1.0.0.1'
set service dns forwarding name-server '8.8.8.8'
set service dns forwarding name-server '8.8.4.4'

# SYSTEM SETTINGS
# SSH, hostname, user, NTP, syslog settings and more
set service ssh port '2222'
set system config-management commit-revisions '100'
set system console device ttyS0 speed '115200'
set system host-name 'company1'
set system login user vyos authentication encrypted-password '$6$QRzeE/jvRdB$FZ5DwnVwr3QAlBhtN3MnMRC5iwkw.gDAX38CV8gINQ0XApMuC8vW/I

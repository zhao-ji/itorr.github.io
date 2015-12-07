Ethernet                Frame Description
ether host <MAC>        MAC address
ether src host <MAC>    Source MAC address
ether dst host <MAC>    Destination MAC address
ether[12:2]             Ethertype

IPv4 Header             Description
ip[0] & 0xf0            IP version (4 for IPv4 and 6 for IPv6)
ip[0] & 0x0f            Header Length ( in 4 byte words)
ip[1]                   Differentiated Services Code Point and Explicit Congestion Notification
ip[2:2]                 Total Lenth
ip[4:2]                 Identification
ip[6] & 0x80 Flags - Reserved
ip[6] & 0x40 Flags - Don't Fragment
ip[6] & 0x20 Flags - More Fragment
ip[6:2] & 0x1fff Fragment Offset
ip[8] Time To Live
ip[9] Protocol
ip[10:2] Header CHecksum
ip[12:4] Source IP Address
ip[16:4] Destination IP address
ip[20: ... ] Options (If present)
ip host IP Address
ip src host Source IP Address
ip dst host Destination IP Address
ip net Network (with CIDR)
IPv6 Header Description
ip6[0] & 0xF0 Version
ip6[0:2] & 0x0FF0 Traffic Class
ip6[1] & 0x0F and ip[2:2] Flow Label
ip6[4:2] Payload Length
ip6[6] Next Header
ip6[7] Hop Limit
ip6 src <ip6 address> IPv6 Source Address
ip6 dst <ip6 address> IPv6 Destination Address
ip6 host IPv6 Address
TCP Header Description
tcp[0:2] Source Port
tcp[2:2] Destination Port
tcp[4:4] Sequence Number
tcp[8:4] Acknowledgement Number
tcp[12] & 0xF0 Header Length (Data Offset)
tcp[12] & 0x0E Reserved Bits
tcp[12] & 0x01 FLAG - NS
tcp[13] & 0x80 FLAG - CWR
tcp[13] & 0x40 FLAG - ECE
tcp[13] & 0x20 FLAG - Urgent
tcp[13] & 0x10 FLAG - Acknowledgement
tcp[13] & 0x08 FLAG - Push
tcp[13] & 0x04 FLAG - Reset
tcp[13] & 0x02 FLAG - Syn
tcp[13] & 0x01 FLAG - Fin
tcp[14:2] Windows Size
tcp[16:2] Checksum
tcp[18:2] Urgent Pointer
tcp[20: ... ] Options (If present)
tcp port TCP Port
tcp src port TCP Source Port
tcp dst port TCP Destination Port
tcp[13] & 0x12 Flags involved in a TCP 3-Way Handshake
UDP Header Description
udp[0:2] Source Port
udp[2:2] Destination Port
udp[4:2] Length
udp[6:2] Checksum
udp port UDP Port
udp src port UDP Source Port
udp dst port UDP Destination Port
ICMP Header Description
icmp[0] Type
icmp[1] Code
icmp[2:2] Checksum
icmp[4: ... ] Message specific information
ARP Header Description
arp[0:2] Hardware Type
arp[2:2] Protocol Type
arp[4] Hardware Address Length
arp[5] Protocol Address Length
arp[6:2] Operation
arp[8:4] and arp[12:2] Sender Hardware Address
arp14:4] Sender IP address
arp[18:4] and arp[22:2] Target Hardware Address
arp[24:4] Target IP Address
﻿802.1q Ethernet Header﻿ Description
ether src host <MAC> Source MAC address
ether dst host <MAC> Destination MAC address
ether[12:2] Tag Protocol ID (0x8100)
ether[13] & 0xE0 User Priority
ether[13] & 0x10 Canonical Format Indicator
ether[13:2] & 0x0FFF VLAN ID

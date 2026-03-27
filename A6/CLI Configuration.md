# **CLI Configuration Diff**

## **DC1**

### **VPN Phase 1**

config vpn ipsec phase1-interface\
edit \"DC1-DC2\"\
set interface \"port1\"\
set peertype any\
set net-device disable\
set proposal des-md5 des-sha1\
set comments \"VPN: DC1-DC2 (Created by VPN wizard)\"\
set remote-gw 100.64.0.3\
set psksecret\
next\
edit \"DC1-HO\"\
set interface \"port1\"\
set peertype any\
set net-device disable\
set proposal des-md5 des-sha1\
set comments \"VPN: DC1-HO (Created by VPN wizard)\"\
set remote-gw 100.64.0.4\
set psksecret \<REDACTED\>\
next\
edit \"DC1-LOCAL\"\
set interface \"port1\"\
set peertype any\
set net-device disable\
set proposal des-md5 des-sha1\
set comments \"VPN: DC1-LOCAL (Created by VPN wizard)\"\
set remote-gw 100.64.0.5\
set psksecret \<REDACTED\>\
next\
end

### **VPN Phase 2**

config vpn ipsec phase2-interface\
edit \"DC1-DC2\"\
set phase1name \"DC1-DC2\"\
set proposal des-md5 des-sha1\
set comments \"VPN: DC1-DC2 (Created by VPN wizard)\"\
set src-addr-type name\
set dst-addr-type name\
set src-name \"DC1-DC2_local\"\
set dst-name \"DC1-DC2_remote\"\
next\
edit \"DC1-HO\"\
set phase1name \"DC1-HO\"\
set proposal des-md5 des-sha1\
set comments \"VPN: DC1-HO (Created by VPN wizard)\"\
set src-addr-type name\
set dst-addr-type name\
set src-name \"DC1-HO_local_subnet_1\"\
set dst-name \"DC1-HO_remote_subnet_1\"\
next\
edit \"DC1-LOCAL\"\
set phase1name \"DC1-LOCAL\"\
set proposal des-md5 des-sha1\
set comments \"VPN: DC1-LOCAL (Created by VPN wizard)\"\
set src-addr-type name\
set dst-addr-type name\
set src-name \"DC1-LOCAL_local\"\
set dst-name \"DC1-LOCAL_remote\"\
next\
end

### 

### **VPN Address Objects**

config firewall address\
edit \"DC1-DC2_local_subnet_1\"\
set allow-routing enable\
set subnet 10.10.10.0 255.255.255.0\
next\
edit \"DC1-DC2_remote_subnet_1\"\
set allow-routing enable\
set subnet 10.20.20.0 255.255.255.0\
next\
edit \"DC1-HO_local_subnet_1\"\
set allow-routing enable\
set subnet 10.10.10.0 255.255.255.0\
next\
edit \"DC1-HO_remote_subnet_1\"\
set allow-routing enable\
set subnet 10.30.30.0 255.255.255.0\
next\
edit \"DC1-LOCAL_local_subnet_1\"\
set allow-routing enable\
set subnet 10.10.10.0 255.255.255.0\
next\
edit \"DC1-LOCAL_remote_subnet_1\"\
set allow-routing enable\
set subnet 10.40.40.0 255.255.255.0\
next\
end

### **Static Routes**

config router static\
edit 10\
set dst 10.20.20.0 255.255.255.0\
set device \"DC1-DC2\"\
next\
edit 20\
set dst 10.30.30.0 255.255.255.0\
set device \"DC1-HO\"\
next\
edit 30\
set dst 10.40.40.0 255.255.255.0\
set device \"DC1-LOCAL\"\
next\
end

### **Firewall Policies**

config firewall policy\
edit 0\
set name \"DC1-LAN-to-DC2\"\
set srcintf \"port2\"\
set dstintf \"DC1-DC2\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"DC2-to-DC1-LAN\"\
set srcintf \"DC1-DC2\"\
set dstintf \"port2\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"DC1-LAN-to-HO\"\
set srcintf \"port2\"\
set dstintf \"DC1-HO\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"HO-to-DC1-LAN\"\
set srcintf \"DC1-HO\"\
set dstintf \"port2\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"DC1-LAN-to-LOCAL\"\
set srcintf \"port2\"\
set dstintf \"DC1-LOCAL\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"LOCAL-to-DC1-LAN\"\
set srcintf \"DC1-LOCAL\"\
set dstintf \"port2\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
end

### **Interfaces**

config system interface\
edit \"port2\"\
set ip 10.10.10.1 255.255.255.0\
next\
edit \"port4\"\
set ip 192.168.122.100 255.255.255.0\
set allowaccess ping https ssh\
next\
end

### **DMZ**

config system interface\
edit \"port3\"\
set ip 172.16.1.1 255.255.255.0\
next\
end

## **DC2**

### **VPN Phase 1**

config vpn ipsec phase1-interface\
edit \"DC2-DC1\"\
set interface \"port1\"\
set keylife 28800\
set peertype any\
set net-device disable\
set proposal des-md5 des-sha1\
set dhgrp 14\
set remote-gw 100.64.0.2\
set psksecret \<REDACTED\>\
next\
edit \"DC2-HO\"\
set interface \"port1\"\
set peertype any\
set net-device disable\
set proposal des-md5 des-sha1\
set comments \"VPN: DC2-HO (Created by VPN wizard)\"\
set wizard-type static-fortigate\
set remote-gw 100.64.0.4\
set psksecret \<REDACTED\>\
next\
edit \"DC2-LOCAL\"\
set interface \"port1\"\
set peertype any\
set net-device disable\
set proposal des-md5 des-sha1\
set comments \"VPN: DC2-LOCAL (Created by VPN wizard)\"\
set wizard-type static-fortigate\
set remote-gw 100.64.0.5\
set psksecret \<REDACTED\>\
next\
end

### **VPN Phase 2**

config vpn ipsec phase2-interface\
edit \"DC2-DC1\"\
set phase1name \"DC2-DC1\"\
set proposal des-md5 des-sha1\
set src-addr-type name\
set dst-addr-type name\
set src-name \"DC2-DC1_local\"\
set dst-name \"DC2-DC1_remote\"\
next\
edit \"DC2-HO\"\
set phase1name \"DC2-HO\"\
set proposal des-md5 des-sha1\
set comments \"VPN: DC2-HO (Created by VPN wizard)\"\
set src-addr-type name\
set dst-addr-type name\
set src-name \"DC2-HO_local\"\
set dst-name \"DC2-HO_remote\"\
next\
edit \"DC2-LOCAL\"\
set phase1name \"DC2-LOCAL\"\
set proposal des-md5 des-sha1\
set comments \"VPN: DC2-LOCAL (Created by VPN wizard)\"\
set src-addr-type name\
set dst-addr-type name\
set src-name \"DC2-LOCAL_local_subnet_1\"\
set dst-name \"DC2-LOCAL_remote_subnet_1\"\
next\
end

### **VPN Address Objects**

config firewall address\
edit \"DC2-DC1_local\"\
set subnet 10.20.20.0 255.255.255.0\
next\
edit \"DC2-DC1_remote\"\
set subnet 10.10.10.0 255.255.255.0\
next\
edit \"DC2-HO_local_subnet_1\"\
set allow-routing enable\
set subnet 10.20.20.0 255.255.255.0\
next\
edit \"DC2-HO_remote_subnet_1\"\
set allow-routing enable\
set subnet 10.30.30.0 255.255.255.0\
next\
edit \"DC2-LOCAL_local_subnet_1\"\
set allow-routing enable\
set subnet 10.20.20.0 255.255.255.0\
next\
edit \"DC2-LOCAL_remote_subnet_1\"\
set allow-routing enable\
set subnet 10.40.40.0 255.255.255.0\
next\
end

### **Static Routes**

config router static\
edit 10\
set dst 10.10.10.0 255.255.255.0\
set device \"DC2-DC1\"\
next\
edit 20\
set dst 10.30.30.0 255.255.255.0\
set device \"DC2-HO\"\
next\
edit 30\
set dst 10.40.40.0 255.255.255.0\
set device \"DC2-LOCAL\"\
next\
end

### **Firewall Policies**

config firewall policy\
edit 0\
set name \"DC2-to-DC1\"\
set srcintf \"port2\"\
set dstintf \"DC2-DC1\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"DC1-to-DC2\"\
set srcintf \"DC2-DC1\"\
set dstintf \"port2\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"DC2-to-HO\"\
set srcintf \"port2\"\
set dstintf \"DC2-HO\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"HO-to-DC2\"\
set srcintf \"DC2-HO\"\
set dstintf \"port2\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"DC2-to-LOCAL\"\
set srcintf \"port2\"\
set dstintf \"DC2-LOCAL\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"LOCAL-to-DC2\"\
set srcintf \"DC2-LOCAL\"\
set dstintf \"port2\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
end

### **Interfaces**

config system interface\
edit \"port2\"\
set ip 10.20.20.1 255.255.255.0\
next\
edit \"port4\"\
set ip 192.168.122.200 255.255.255.0\
set allowaccess ping https ssh\
next\
end

### **DMZ**

config system interface\
edit \"port3\"\
set ip 172.16.2.1 255.255.255.0\
next\
end

## **Head Office**

### **VPN Phase 1**

config vpn ipsec phase1-interface\
edit \"HO-DC1\"\
set interface \"port1\"\
set peertype any\
set net-device disable\
set proposal des-md5 des-sha1\
set remote-gw 100.64.0.2\
set psksecret \<REDACTED\>\
next\
edit \"HO-DC2\"\
set interface \"port1\"\
set peertype any\
set net-device disable\
set proposal des-md5 des-sha1\
set comments \"VPN: HO-DC2 (Created by VPN wizard)\"\
set wizard-type static-fortigate\
set remote-gw 100.64.0.3\
set psksecret \<REDACTED\>\
next\
end

### **VPN Phase 2**

config vpn ipsec phase2-interface\
edit \"HO-DC1\"\
set phase1name \"HO-DC1\"\
set proposal des-md5 des-sha1\
set src-addr-type name\
set dst-addr-type name\
set src-name \"HO-DC1_local\"\
set dst-name \"HO-DC1_remote\"\
next\
edit \"HO-DC2\"\
set phase1name \"HO-DC2\"\
set proposal des-md5 des-sha1\
set comments \"VPN: HO-DC2 (Created by VPN wizard)\"\
set src-addr-type name\
set dst-addr-type name\
set src-name \"HO-DC2_local_subnet_1\"\
set dst-name \"HO-DC2_remote_subnet_1\"\
next\
end

### **VPN Address Objects**

config firewall address\
edit \"HO-DC1_local\"\
set subnet 10.30.30.0 255.255.255.0\
next\
edit \"HO-DC1_remote\"\
set subnet 10.10.10.0 255.255.255.0\
next\
edit \"HO-DC2_local_subnet_1\"\
set allow-routing enable\
set subnet 10.30.30.0 255.255.255.0\
next\
edit \"HO-DC2_remote_subnet_1\"\
set allow-routing enable\
set subnet 10.20.20.0 255.255.255.0\
next\
end

### **Static Routes**

config router static\
edit 20\
set dst 10.10.10.0 255.255.255.0\
set device \"HO-DC1\"\
next\
edit 50\
set dst 10.20.20.0 255.255.255.0\
set device \"HO-DC2\"\
next\
end

### **Firewall Policies**

config firewall policy\
edit 0\
set name \"HO-to-DC1\"\
set srcintf \"port2\"\
set dstintf \"HO-DC1\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"DC1-to-HO\"\
set srcintf \"HO-DC1\"\
set dstintf \"port2\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"HO-to-DC2\"\
set srcintf \"port2\"\
set dstintf \"HO-DC2\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"DC2-to-HO\"\
set srcintf \"HO-DC2\"\
set dstintf \"port2\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
end

### **Interfaces**

config system interface\
edit \"port2\"\
set ip 10.30.30.1 255.255.255.0\
next\
edit \"port4\"\
set ip 192.168.122.150 255.255.255.0\
set allowaccess ping https ssh\
next\
end

### **DMZ**

config system interface\
edit \"port3\"\
set ip 172.16.3.1 255.255.255.0\
next\
end

## **Local Site**

### **VPN Phase 1**

config vpn ipsec phase1-interface\
edit \"LOCAL-DC1\"\
set interface \"port1\"\
set peertype any\
set net-device disable\
set proposal des-md5 des-sha1\
set remote-gw 100.64.0.2\
set psksecret \<REDACTED\>\
next\
edit \"LOCAL-DC2\"\
set interface \"port1\"\
set peertype any\
set net-device disable\
set proposal des-md5 des-sha1\
set dhgrp 14\
set comments \"VPN: LOCAL-DC2 (Created by VPN wizard)\"\
set wizard-type static-fortigate\
set remote-gw 100.64.0.3\
set psksecret \<REDACTED\>\
next\
end

### **VPN Phase 2**

config vpn ipsec phase2-interface\
edit \"LOCAL-DC1\"\
set phase1name \"LOCAL-DC1\"\
set proposal des-md5 des-sha1\
set src-addr-type name\
set dst-addr-type name\
set src-name \"LOCAL-DC1_local\"\
set dst-name \"LOCAL-DC1_remote\"\
next\
edit \"LOCAL-DC2\"\
set phase1name \"LOCAL-DC2\"\
set proposal des-md5 des-sha1\
set src-subnet 10.40.40.0 255.255.255.0\
set dst-subnet 10.20.20.0 255.255.255.0\
next\
end

### **VPN Address Objects**

config firewall address\
edit \"LOCAL-DC1_local\"\
set subnet 10.40.40.0 255.255.255.0\
next\
edit \"LOCAL-DC1_remote\"\
set subnet 10.10.10.0 255.255.255.0\
next\
edit \"LOCAL-DC2_local_subnet_1\"\
set allow-routing enable\
set subnet 10.40.40.0 255.255.255.0\
next\
edit \"LOCAL-DC2_remote_subnet_1\"\
set allow-routing enable\
set subnet 10.20.20.0 255.255.255.0\
next\
end

### **Static Routes**

config router static\
edit 10\
set dst 10.10.10.0 255.255.255.0\
set device \"LOCAL-DC1\"\
next\
edit 20\
set dst 10.20.20.0 255.255.255.0\
set device \"LOCAL-DC2\"\
next\
end

### **Firewall Policies**

config firewall policy\
edit 0\
set name \"LOCAL-to-DC1\"\
set srcintf \"port2\"\
set dstintf \"LOCAL-DC1\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"DC1-to-LOCAL\"\
set srcintf \"LOCAL-DC1\"\
set dstintf \"port2\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"LOCAL-to-DC2\"\
set srcintf \"port2\"\
set dstintf \"LOCAL-DC2\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
edit 0\
set name \"DC2-to-LOCAL\"\
set srcintf \"LOCAL-DC2\"\
set dstintf \"port2\"\
set srcaddr \"all\"\
set dstaddr \"all\"\
set action accept\
set schedule \"always\"\
set service \"ALL\"\
set nat disable\
next\
end

### **Interfaces**

config system interface\
edit \"port2\"\
set ip 10.40.40.1 255.255.255.0\
next\
edit \"port4\"\
set ip 192.168.122.160 255.255.255.0\
set allowaccess ping https ssh\
next\
end

### **DMZ**

config system interface\
edit \"port3\"\
set ip 172.16.4.1 255.255.255.0\
next\
end

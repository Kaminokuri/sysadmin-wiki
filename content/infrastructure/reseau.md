---
title: "Architecture Réseau"
description: "Conception et mise en œuvre d'architectures réseau d'entreprise"
category: "Infrastructure"
tags: ["Réseau", "Cisco", "Switching", "Routing", "Network Design"]
level: "Avancé"
reading_time: "35 min"
last_updated: "31 juillet 2025"
author: "Mathéo Fauvel"
---

# 🌐 Architecture Réseau

## Vue d'ensemble

L'architecture réseau d'entreprise définit la structure, les protocoles et les technologies permettant la communication entre tous les éléments de l'infrastructure IT.

## 🏗️ Modèles d'Architecture

### Modèle Hiérarchique à 3 Couches
```
┌─────────────────┐
│   Core Layer    │ ← Haute disponibilité, routage rapide
├─────────────────┤
│ Distribution    │ ← Politiques, agrégation, routage
├─────────────────┤
│  Access Layer   │ ← Connexion utilisateurs finaux
└─────────────────┘
```

### Spine-Leaf (Data Center)
```
   Spine 1    Spine 2
      │╲    ╱│
      │ ╲  ╱ │
      │  ╲╱  │
      │  ╱╲  │
      │ ╱  ╲ │
      │╱    ╲│
   Leaf 1    Leaf 2
```

## 🔌 Technologies de Commutation

### VLANs et Trunking
```bash
# Configuration VLAN Cisco
vlan 10
 name USERS
vlan 20
 name SERVERS

# Configuration trunk
interface GigabitEthernet0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20
```

### Spanning Tree Protocol
```bash
# Configuration PVST+
spanning-tree mode pvst
spanning-tree vlan 10 root primary
spanning-tree vlan 20 root secondary

# RSTP (802.1w)
spanning-tree mode rapid-pvst
```

### Link Aggregation (LACP)
```bash
# EtherChannel configuration
interface range GigabitEthernet0/1-2
 channel-group 1 mode active
 
interface port-channel 1
 switchport mode trunk
```

## 🗺️ Routage et Protocoles

### OSPF Configuration
```bash
# OSPF Process
router ospf 1
 router-id 1.1.1.1
 network 192.168.1.0 0.0.0.255 area 0
 network 10.0.0.0 0.255.255.255 area 1
 
# Interface OSPF
interface GigabitEthernet0/0
 ip ospf cost 10
 ip ospf hello-interval 5
```

### BGP pour WAN
```bash
# eBGP configuration
router bgp 65001
 bgp router-id 1.1.1.1
 neighbor 203.0.113.1 remote-as 65002
 network 192.168.0.0 mask 255.255.0.0
```

### HSRP/VRRP (High Availability)
```bash
# HSRP Configuration
interface Vlan10
 ip address 192.168.10.2 255.255.255.0
 standby 1 ip 192.168.10.1
 standby 1 priority 110
 standby 1 preempt
```

## 🛡️ Sécurité Réseau

### ACLs (Access Control Lists)
```bash
# Standard ACL
access-list 10 permit 192.168.1.0 0.0.0.255
access-list 10 deny any

# Extended ACL
ip access-list extended WEB_FILTER
 permit tcp 192.168.1.0 0.0.0.255 any eq 80
 permit tcp 192.168.1.0 0.0.0.255 any eq 443
 deny ip any any
```

### Port Security
```bash
# Port security configuration
interface FastEthernet0/1
 switchport mode access
 switchport port-security
 switchport port-security maximum 2
 switchport port-security violation restrict
 switchport port-security mac-address sticky
```

### 802.1X Authentication
```bash
# 802.1X global configuration
aaa new-model
aaa authentication dot1x default group radius
radius-server host 192.168.1.100 key secret123

# Interface configuration
interface range FastEthernet0/1-24
 authentication host-mode multi-auth
 authentication port-control auto
 dot1x pae authenticator
```

## 📡 Technologies WAN

### MPLS Configuration
```bash
# MPLS setup
mpls ldp router-id Loopback0
mpls label protocol ldp

interface GigabitEthernet0/0
 mpls ip
 
# VRF for customer separation
ip vrf CUSTOMER_A
 rd 65001:100
 route-target export 65001:100
 route-target import 65001:100
```

### SD-WAN Architecture
- **Centralized Policy** : vManage
- **Control Plane** : vSmart Controllers  
- **Data Plane** : vEdge Routers
- **Orchestration** : Zero-touch provisioning

## ☁️ Cloud Networking

### AWS Networking
```yaml
# VPC CloudFormation
VPC:
  Type: AWS::EC2::VPC
  Properties:
    CidrBlock: 10.0.0.0/16
    EnableDnsHostnames: true
    
PublicSubnet:
  Type: AWS::EC2::Subnet
  Properties:
    VpcId: !Ref VPC
    CidrBlock: 10.0.1.0/24
    AvailabilityZone: !Select [0, !GetAZs '']
```

### Azure Virtual Networks
```json
{
  "type": "Microsoft.Network/virtualNetworks",
  "apiVersion": "2021-02-01",
  "name": "myVNet",
  "location": "East US",
  "properties": {
    "addressSpace": {
      "addressPrefixes": ["10.0.0.0/16"]
    },
    "subnets": [
      {
        "name": "subnet1",
        "properties": {
          "addressPrefix": "10.0.1.0/24"
        }
      }
    ]
  }
}
```

## 📊 QoS (Quality of Service)

### Classification et Marking
```bash
# Class-map for voice traffic
class-map match-all VOICE
 match dscp ef

# Policy-map for QoS
policy-map WAN_QOS
 class VOICE
  priority percent 30
 class class-default
  fair-queue
```

### Traffic Shaping
```bash
# Traffic shaping configuration
policy-map SHAPE_10M
 class class-default
  shape average 10000000
  
interface Serial0/0
 service-policy output SHAPE_10M
```

## 🔍 Monitoring et Troubleshooting

### SNMP Configuration
```bash
# SNMP v3 setup
snmp-server group ADMIN v3 priv
snmp-server user admin1 ADMIN v3 auth sha myauthkey priv aes 128 myprivkey
snmp-server host 192.168.1.100 version 3 priv admin1
```

### NetFlow/sFlow
```bash
# NetFlow configuration
ip flow-export destination 192.168.1.100 9996
ip flow-export version 9

interface GigabitEthernet0/0
 ip flow ingress
 ip flow egress
```

### Network Monitoring Tools
- **SolarWinds NPM**
- **PRTG Network Monitor**
- **Nagios**
- **LibreNMS**
- **Observium**

## 🛠️ Automatisation Réseau

### Python pour l'Automatisation
```python
# Netmiko example
from netmiko import ConnectHandler

device = {
    'device_type': 'cisco_ios',
    'host': '192.168.1.1',
    'username': 'admin',
    'password': 'secret'
}

connection = ConnectHandler(**device)
output = connection.send_command('show ip interface brief')
print(output)
```

### Ansible pour le Réseau
```yaml
---
- name: Configure VLAN
  hosts: switches
  tasks:
    - name: Create VLAN 10
      ios_vlan:
        vlan_id: 10
        name: USERS
        state: present
```

### NETCONF/YANG
```xml
<!-- NETCONF example -->
<config>
  <interfaces xmlns="urn:ietf:params:xml:ns:yang:ietf-interfaces">
    <interface>
      <name>GigabitEthernet0/0/1</name>
      <description>Link to Core Switch</description>
      <enabled>true</enabled>
    </interface>
  </interfaces>
</config>
```

## 📐 Design Best Practices

### Sizing et Dimensionnement
- **Oversubscription ratios**
  - Access: 20:1
  - Distribution: 4:1  
  - Core: 1:1

### Redondance
- **Dual-homed connections**
- **Multiple ISPs**
- **Equipment redundancy**
- **Geographic diversity**

### Scalabilité
- **Modular design**
- **Future growth planning**
- **Technology refresh cycles**
- **Performance monitoring**

## 🔧 Troubleshooting Méthodologies

### Approche Structurée
1. **Identifier le problème**
2. **Établir théories probables**
3. **Tester théories**
4. **Établir plan d'action**
5. **Implémenter solution**
6. **Vérifier fonctionnalité**
7. **Documenter**

### Outils de Diagnostic
```bash
# Cisco IOS troubleshooting
show ip route
show interfaces
show mac address-table
debug ip packet
traceroute 8.8.8.8
```

### Packet Capture
```bash
# tcpdump
tcpdump -i eth0 -w capture.pcap host 192.168.1.1

# Wireshark filters
tcp.port == 443
icmp.type == 8
http.request.method == "GET"
```

## 📈 Performance Optimization

### Bandwidth Management
- **Traffic prioritization**
- **Bandwidth allocation**
- **Congestion control**
- **Load balancing**

### Latency Reduction
- **Optimal path selection**
- **Buffer tuning**
- **Protocol optimization**
- **Caching strategies**

---

🚀 **Pro Tip** : Une architecture réseau bien conçue est évolutive, sécurisée et maintient les performances même en cas de croissance.
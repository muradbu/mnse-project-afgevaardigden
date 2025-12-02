- We're creating an Ansible Playbook for our school project
- Use the Cisco ios documentation: https://docs.ansible.com/projects/ansible/latest/collections/cisco/ios/index.html
    - Use the provided modules
- See NetwerktekeningBackbone.drawio.png
- We're configuring 3 routers in the server room: `aggregate-dc`, `aggregate-noord`, `aggregate-zuid`
- They're Cisco routers
- Make logical router-id's per router
- They need to speak BGP with each other
    - `aggregate-dc` connects `aggregate-noord` and `aggregate-zuid`
- `aggregate-dc` info:
    - AS 65501
    - GigabitEthernet0/0/0.455 10.255.0.49 255.255.255.252 (p2p to `aggregate-noord`)
    - Tunnel1 10.255.0.45 255.255.255.252 (p2p to `aggregate-zuid`)
    - Management IP for SSH: 10.99.2.51
    - Has a switch with multiple routers attached per province, see below.
- `aggregate-noord` info:
    - AS 65503
    - GigabitEthernet0/0/0.455 10.255.0.50 255.255.255.252 (p2p to `aggregate-dc`)
    - Management IP for SSH: 10.99.2.50
    - Has multiple routers attached with provinces, see below.
- `aggregate-zuid` info:
    - AS 65502
    - Tunnel1 10.255.0.46 255.255.255.252 (p2p to `aggregate-dc`)
    - Management IP for SSH: 10.4.0.5
    - Has multiple routers attached with provinces, see below.

OSPF areas (all router-on-a-stick P2P connections connected to the aggregate routers):
 
aggregate-zuid (client routers):
 
Limburg: 
  vlan: 101
  P2P subnet (/30): 172.24.255.0
 
N Brabant:
  vlan: 102
  P2P subnet (/30): 172.25.255.0
 
Gelderland:
  vlan: 103
  P2P subnet (/30): 172.26.255.0
 
Zeeland:
  vlan: 104
  P2P subnet (/30): 172.27.255.0
 
Z Holland:
  vlan: 105
  P2P subnet (/30): 172.28.255.0
 
ABC:
  vlan: 106
  P2P subnet (/30): 172.29.255.0
 
 
 
aggregate-noord (client routers p2p):
 
Groningen:
  vlan: 111
  P2P subnet (/30): 172.19.255.0 
 
Friesland:
  vlan: 112
  P2P subnet (/30): 172.23.255.0 
 
Drenthe:
  vlan: 113
  P2P subnet (/30): 172.17.255.0 
 
Overijssel:
  vlan: 114
  P2P subnet (/30): 172.21.255.0 
 
 
 
aggregate-dc (server routers):
 
Limburg: 
  vlan: 400
  P2P subnet (/30): 
 
N Brabant:
  vlan: 405
  P2P subnet (/30): 172.25.255.252
 
Gelderland:
  vlan: 410
  P2P subnet (/30): 172.26.255.252
 
Zeeland:
  vlan: 415
  P2P subnet (/30): 172.27.255.252
 
Z Holland:
  vlan: 460
  P2P subnet (/30): 172.28.255.252
 
ABC:
  vlan: 465
  P2P subnet (/30): 172.29.255.252
 
Groningen:
  vlan: 430
  P2P subnet (/30): 172.19.255.252 
 
Friesland:
  vlan: 435
  P2P subnet (/30): 172.23.255.252
 
Drenthe:
  vlan: 440
  P2P subnet (/30): 172.17.255.252
 
Overijssel:
  vlan: 445
  P2P subnet (/30): 172.21.255.252

# VLAN Configuration (CCNA Lab)

## Objective
Configure VLANs and assign ports on a Cisco switch.

## Topology
- 1 Switch (2960)
- 2 PCs
- PC0 on VLAN 10 (HR)
- PC1 on VLAN 20 (IT)

## Switch Commands
Switch> enable
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# name HR
Switch(config)# vlan 20
Switch(config-vlan)# name IT
...


## PC IPs
- PC0: 192.168.10.1 /24  
- PC1: 192.168.20.1 /24

## Expected Result
- PCs cannot ping each other (VLAN isolation)

# VLAN Configuration (CCNA Lab)

## Objective
Configure VLANs and assign ports on a Cisco switch.

## Topology
- 1 Switch (2960)
- 2 PCs
- PC0 on VLAN 10 (HR)
- PC1 on VLAN 20 (IT)

## Switch Commands
```
Switch> enable 
Switch# configure terminal 
  ! Create VLAN 10 and name it HR
Switch(config)# vlan 10 
Switch(config-vlan)# name HR 
Switch(config-vlan)# exit 
  ! Create VLAN 20 and name it IT 
Switch(config)# vlan 20
Switch(config-vlan)# name IT 
Switch(config-vlan)# exit 
  ! Assign FastEthernet 0/1 to VLAN 10 
Switch(config)# interface fastEthernet 0/1
Switch(config-if)# switchport mode access 
Switch(config-if)# switchport access vlan 10 
Switch(config-if)# exit 
  ! Assign FastEthernet 0/2 to VLAN 20 
Switch(config)# interface fastEthernet 0/2 
Switch(config-if)# switchport mode access 
Switch(config-if)# switchport access vlan 20 
Switch(config-if)# exit 
  ! Save the configuration 
Switch(config)# end 
Switch# write memory
```


## PC IPs
- PC0: 192.168.10.1 /24  
- PC1: 192.168.20.1 /24

## Expected Result
- PCs cannot ping each other (VLAN isolation)


📦 [Download the Packet Tracer Lab File](./VLAN_Basics.pkt)

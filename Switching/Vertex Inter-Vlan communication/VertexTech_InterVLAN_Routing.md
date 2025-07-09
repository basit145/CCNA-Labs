# VertexTech Peshawar – Phase 2: Inter-VLAN Routing (Router-on-a-Stick)

## 🏢 Scenario

After implementing VLANs at **VertexTech Solutions – Peshawar**, the HR and IT departments now need to communicate. You are assigned to upgrade the network using **Router-on-a-Stick** configuration to enable **Inter-VLAN Routing**.

---

## 🎯 Objective

- Reuse VLAN 10 (HR) and VLAN 20 (IT) from the previous lab
- Configure a router with subinterfaces to enable routing between VLANs
- Verify connectivity between PCs in different VLANs

---

## 📦 Network Overview

- VLANs already configured on switch:
  - HR → VLAN 10 → 192.168.10.0/24
  - IT → VLAN 20 → 192.168.20.0/24
- Trunk link between switch and router
- Subinterfaces configured on router for inter-VLAN routing

---

## 🧰 Devices Required

- 1 × Cisco 2960 Switch  
- 1 × Cisco Router (e.g., 1841 or 2911)  
- 2 × PCs  
- Copper Straight-Through Cables

---

## 🧱 Topology
```
PC0 (HR) → Fa0/1 -----+
|
Switch ---- G0/1 (Trunk) ---- Router G0/0
|
PC2 (IT) → Fa0/3 -----+
```

---

## 💻 IP Addressing Plan

```text
PC0 (HR) → 192.168.10.10 /24 → Gateway: 192.168.10.1
PC1 (IT) → 192.168.20.10 /24 → Gateway: 192.168.20.1
```

## Switch configuration
```
Switch> enable
Switch# configure terminal

! Trunk port to router
interface G0/1
 switchport mode trunk

end
write memory
```

## 🔧 Router Configuration (Router-on-a-Stick)
```
Router> enable
Router# configure terminal

! Subinterface for VLAN 10 (HR)
interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

! Subinterface for VLAN 20 (IT)
interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0

! Enable physical interface
interface g0/0
 no shutdown

end
write memory
```
## ✅ Verification Steps
```
! On Router:
show ip interface brief
ping 192.168.10.10
ping 192.168.20.10

! On PCs:
ping from PC0 → 192.168.20.10 (PC0)
ping from PC2 → 192.168.10.10 (PC2)
```
✅ If both pings work → Inter-VLAN routing is successful.

## ❌ Troubleshooting Tips
```
- If ping fails:
  → Check trunk port on switch (g0/1)
  → Verify subinterface IDs match VLANs
  → Confirm PC IPs & gateways are correct
  → Ensure no shutdown is applied on G0/0
```
## Notes
- Inter-VLAN Routing enables Layer 3 communication between separate VLANs
- Each subinterface on the router handles one VLAN
- dot1Q encapsulation tags traffic with VLAN ID
- This method saves hardware by using only one physical router interface

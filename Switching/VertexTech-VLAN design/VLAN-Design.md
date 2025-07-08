# VLAN Configuration for VertexTech Solutions – Peshawar

## 🏢 Scenario
You are hired as a network engineer by **VertexTech Solutions – Peshawar Branch** to segment the internal network using VLANs. Each department must be isolated on its own VLAN.

---

## 🎯 Objective
Configure VLANs for 5 departments and assign switch ports. Devices in the same department should communicate; devices in different departments should not.

---

## 🖥️ Departments & VLAN Plan

| Department      | VLAN Name | VLAN ID | Subnet           | Ports     |
|----------------|-----------|---------|------------------|-----------|
| HR             | HR        | 10      | 192.168.10.0/24  | Fa0/1–2   |
| IT             | IT        | 20      | 192.168.20.0/24  | Fa0/3–4   |
| Accounts       | ACC       | 30      | 192.168.30.0/24  | Fa0/5–6   |
| Management     | MGMT      | 40      | 192.168.40.0/24  | Fa0/7–8   |
| Security/CCTV  | SEC       | 50      | 192.168.50.0/24  | Fa0/9–10  |

---

## 🧰 Devices Used
- 1 × Cisco 2960 Switch  
- 10 × PCs (2 per department)  
- Copper Straight-Through cables

---

## 🔧 Switch Configuration

```bash
Switch> enable
Switch# configure terminal

! VLAN creation
vlan 10
 name HR
vlan 20
 name IT
vlan 30
 name ACC
vlan 40
 name MGMT
vlan 50
 name SEC

! Assign ports to VLANs
interface range fa0/1 - 2
 switchport mode access
 switchport access vlan 10

interface range fa0/3 - 4
 switchport mode access
 switchport access vlan 20

interface range fa0/5 - 6
 switchport mode access
 switchport access vlan 30

interface range fa0/7 - 8
 switchport mode access
 switchport access vlan 40

interface range fa0/9 - 10
 switchport mode access
 switchport access vlan 50

! Save configuration
end
write memory
```
## PC IP ADDRESSING
PC0  - VLAN 10 (HR)      - 192.168.10.10 /24
PC1  - VLAN 10 (HR)      - 192.168.10.11 /24

PC2  - VLAN 20 (IT)      - 192.168.20.10 /24
PC3  - VLAN 20 (IT)      - 192.168.20.11 /24

PC4  - VLAN 30 (Accounts)- 192.168.30.10 /24
PC5  - VLAN 30 (Accounts)- 192.168.30.11 /24

PC6  - VLAN 40 (MGMT)    - 192.168.40.10 /24
PC7  - VLAN 40 (MGMT)    - 192.168.40.11 /24

PC8  - VLAN 50 (Security)- 192.168.50.10 /24
PC9  - VLAN 50 (Security)- 192.168.50.11 /24

## ✅ Verification Commands
```
Switch# show vlan brief
Switch# show running-config
```

## ❌ Ping Test
✅ Same VLANs:
PC0 ↔ PC1  → Ping success (VLAN 10)
PC2 ↔ PC3  → Ping success (VLAN 20)

❌ Different VLANs:
PC0 → PC2  → Ping fail
PC4 → PC7  → Ping fail

## Notes
- VLANs separate devices into isolated broadcast domains at Layer 2.
- Devices in different VLANs cannot communicate without routing (e.g. Router-on-a-Stick).
- Helps improve network security, scalability, and performance.



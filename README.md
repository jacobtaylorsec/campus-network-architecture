# Campus Network Architecture – Redundant Enterprise Design

This project demonstrates the design, implementation, and validation of a redundant enterprise-style campus network using dual-core Layer 3 switches, dynamic routing, Layer 2 resiliency mechanisms, and structured security segmentation.

The objective of this project was not just to configure devices, but to validate control-plane and data-plane behavior under failure conditions using structured testing and documented results.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Technologies Implemented](#technologies-implemented)
- [Architecture Highlights](#architecture-highlights)
- [Repository Structure](#repository-structure)
- [Documentation](#documentation)
- [Resiliency Validation Summary](#resiliency-validation-summary)

---

## Project Overview

This campus network follows a hierarchical model:

- Access Layer (Departmental Switches)
- Distribution Layer
- Dual Core Layer (Layer 3 Switching)
- Dual Edge Routers (OSPF Upstream Connectivity)

The design eliminates single points of failure across:

- Default gateway services
- Layer 2 uplinks
- Edge routing
- Upstream connectivity

All redundancy mechanisms were validated using controlled failure testing.

---

## Technologies Implemented

- VLAN Segmentation
- Inter-VLAN Routing (SVIs)
- HSRP (Gateway Redundancy)
- EtherChannel (Link Aggregation)
- Spanning Tree Protocol (Loop Prevention)
- OSPF (Dynamic Routing)
- Extended ACLs (Inter-VLAN Security)
- DHCP Relay (ip helper-address)
- Static Server Infrastructure (DNS, DHCP, Web, File)

---

## Architecture Highlights

- Dual-core Layer 3 design
- HSRP load balancing across VLANs
- Deterministic STP root placement
- Dynamic routing at edge (OSPF)
- ACL-based lateral movement control
- Structured IP addressing plan (`10.10.<VLAN>.0/24`)

---

## Repository Structure

```
campus-network-architecture/
│
├── README.md
├── campus_network_final.pkt
│
├── docs/
│ ├── network-overview.md
│ ├── redundancy-design.md
│ ├── security-policy.md
│ └── resiliency-tests.md
│
└── images/
├── (HSRP screenshots)
├── (OSPF screenshots)
├── (STP screenshots)
└── (EtherChannel screenshots)
```


---

## Documentation

Detailed design and validation documentation for this project is organized as follows:

| Document | Description | Link |
|----------|------------|------|
| Network Overview | Topology diagram, VLAN structure, and IP addressing plan | [View](docs/network-overview.md) |
| Redundancy Design | Dual-core architecture, HSRP load balancing, EtherChannel, and OSPF edge routing strategy | [View](docs/redundancy-design.md) |
| Security Policy | Inter-VLAN segmentation model and ACL enforcement approach | [View](docs/security-policy.md) |
| Resiliency Tests | Structured failover validation for HSRP, EtherChannel, STP, and OSPF | [View](docs/resiliency-tests.md) |

---

## Lab File

The full Cisco Packet Tracer implementation is included:

- `campus_network_architecture.pkt`

This file contains all device configurations, VLAN segmentation, routing, ACL policies, and resiliency mechanisms documented in this repository.

---

## Resiliency Validation Summary

The following failure scenarios were tested and documented:

- Core switch failure (HSRP takeover)
- Edge router failure (OSPF reconvergence)
- Layer 2 root port failure (STP alternate path activation)
- EtherChannel member link failure
- End-to-end client connectivity during each event

Each scenario includes:

- Baseline state
- Failure injection
- Reconvergence behavior
- Connectivity validation
- Recovery state

This confirms proper implementation of redundant design principles and predictable convergence behavior.

---

## Project Intent

This project was built to demonstrate:

- Practical understanding of enterprise network architecture
- Ability to design for failure
- Structured validation methodology
- Clear technical documentation suitable for professional review

## Cybersecurity Focus

Although this project is infrastructure-focused, it was intentionally designed and documented with a cybersecurity perspective in mind.

### Network Segmentation

VLAN-based segmentation and extended ACLs were implemented to:

- Prevent lateral movement between user groups
- Restrict student and dorm networks from accessing administrative systems
- Enforce controlled access to infrastructure services
- Maintain a dedicated IT management VLAN

This reflects real-world enterprise segmentation strategy used to reduce blast radius during compromise.

---

### Resiliency and Incident Stability

Redundant design mechanisms (HSRP, OSPF, STP, EtherChannel) were validated under failure conditions to ensure:

- No unexpected traffic blackholes
- No broadcast storms
- Predictable convergence behavior
- Stable control-plane operation during disruptions

From a cybersecurity perspective, this is critical during:

- DDoS conditions
- Link failures
- Upstream instability
- Hardware compromise events

A resilient network limits cascading failures during active incidents.

---

### Traffic Path Awareness

Understanding:

- Default gateway behavior
- Route selection logic
- Control-plane convergence
- VLAN boundary enforcement

is essential when analyzing:

- Suspicious lateral movement
- Rogue DHCP activity
- Routing manipulation
- Unexpected east-west traffic flows

This project reinforces the importance of architectural awareness when performing network-based threat analysis.

---

### SOC Relevance

For a SOC or cybersecurity analyst, knowledge of:

- How routing changes during failure
- How segmentation is enforced
- Where inter-VLAN boundaries exist
- How control protocols behave under stress

directly improves:

- Incident triage accuracy
- Log interpretation
- False-positive reduction
- Escalation precision

Infrastructure knowledge strengthens defensive analysis.

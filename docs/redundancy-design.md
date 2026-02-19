# Redundancy Design

This architecture was intentionally designed to eliminate single points of failure at both Layer 2 and Layer 3.

---

## Dual Core Layer

Two Layer 3 core switches provide:

- Redundant default gateways (HSRP)
- Redundant uplinks from distribution
- Inter-VLAN routing resilience

If one core fails, the second immediately assumes gateway responsibility.

---

## HSRP Load Balancing

HSRP was configured with split active roles across VLANs to:

- Distribute Layer 3 gateway load
- Prevent a single core from carrying all traffic
- Improve resource utilization

This ensures active/active gateway behavior rather than idle standby.

---

## EtherChannel

Link aggregation was implemented between distribution and core to:

- Increase bandwidth
- Provide link-level redundancy
- Reduce STP blocked paths

Loss of a single physical member does not disrupt traffic.

---

## Spanning Tree Design

STP ensures:

- Loop prevention
- Deterministic root placement
- Alternate path activation during failure

Root bridge priority was explicitly configured for control.

---

## OSPF at the Edge

Dynamic routing was implemented between the core and edge routers using OSPF.

This provides:

- Automatic route propagation
- Fast adjacency failure detection
- Redundant upstream path selection

Static routing was intentionally avoided to maintain dynamic failover behavior.

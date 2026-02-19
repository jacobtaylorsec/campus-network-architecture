# Security Policy

Inter-VLAN access was intentionally restricted using extended ACLs applied at the core SVIs.

---

## Segmentation Policy

| Source VLAN | Destination VLAN | Allowed |
|------------|------------------|----------|
| Students (30) | Admin (10) | ❌ Denied |
| Dorms (40) | Admin (10) | ❌ Denied |
| IT (99) | All VLANs | ✅ Allowed |
| All VLANs | Servers (50) | ✅ Allowed |

---

## Implementation Approach

Extended ACLs were applied inbound on VLAN SVIs to:

- Prevent lateral movement
- Restrict student and dorm access to administrative systems
- Allow controlled access to infrastructure services

The IT management VLAN maintains full access for operational purposes.

This segmentation reflects a realistic enterprise access control model.

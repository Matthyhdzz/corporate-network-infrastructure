# Security Policy

This document describes the security controls implemented in the corporate network.

## Department Segmentation

The network is divided into separate VLANs.

| VLAN | Department | Purpose |
|---:|---|---|
| 10 | ADMIN | Administration users |
| 20 | DEVELOPMENT | Development users |
| 30 | IT-SUPPORT | IT administration and technical support |
| 99 | MANAGEMENT | Network device management |
| 999 | UNUSED-PORTS | Isolated and disabled switch ports |

## Inter-VLAN Access Control

Development users are not allowed to access the Administration network.

| Source | Destination | Action |
|---|---|---|
| 10.10.20.0/24 | 10.10.10.0/24 | Deny |

All other traffic is currently permitted unless restricted by another policy.

## Secure Remote Administration

Remote administration uses SSH version 2.

Only devices located in the IT Support network are authorized to access the router and switch through SSH.

| Setting | Value |
|---|---|
| Authorized network | 10.10.30.0/24 |
| Protocol | SSH version 2 |
| Telnet | Disabled |
| Authentication | Local user database |

Administrative access from the Administration and Development networks is denied.

## Switch Port Security

Active user ports use Port Security with the following settings:

- Maximum of one MAC address per access port.
- Sticky MAC address learning.
- Restrict mode for security violations.
- Unauthorized traffic is discarded.
- The affected port remains operational in restrict mode.

## Unused Ports

Unused switch ports are:

- Assigned to VLAN 999.
- Configured as access ports.
- Administratively disabled.
- Separated from all production VLANs.

This reduces the possibility of unauthorized devices connecting to the corporate network.

## Management Network

Network devices are managed through VLAN 99.

| Device | Management IP |
|---|---|
| R1-EDGE | 10.10.99.1 |
| SW-ACCESS-01 | 10.10.99.2 |

Access to management services is restricted to the IT Support network.

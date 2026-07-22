# Addressing Plan

This document defines the IPv4 addressing scheme used in the corporate network.

## VLAN Addressing

| VLAN | Name | Network | Default Gateway | Address Assignment |
|---:|---|---|---|---|
| 10 | ADMIN | 10.10.10.0/24 | 10.10.10.1 | DHCP |
| 20 | DEVELOPMENT | 10.10.20.0/24 | 10.10.20.1 | DHCP |
| 30 | IT-SUPPORT | 10.10.30.0/24 | 10.10.30.1 | DHCP |
| 99 | MANAGEMENT | 10.10.99.0/24 | 10.10.99.1 | Static |
| 999 | UNUSED-PORTS | No IP network | None | Not applicable |

## Infrastructure Addresses

| Device | Interface | IP Address | Purpose |
|---|---|---|---|
| R1-EDGE | G0/0.10 | 10.10.10.1/24 | ADMIN gateway |
| R1-EDGE | G0/0.20 | 10.10.20.1/24 | DEVELOPMENT gateway |
| R1-EDGE | G0/0.30 | 10.10.30.1/24 | IT-SUPPORT gateway |
| R1-EDGE | G0/0.99 | 10.10.99.1/24 | MANAGEMENT gateway |
| SW-ACCESS-01 | VLAN 99 | 10.10.99.2/24 | Switch management |

## DHCP Address Allocation

The first twenty addresses of each user network are excluded from DHCP.

- `.1` is assigned to the default gateway.
- `.2` through `.20` are reserved for infrastructure and future services.
- DHCP clients receive addresses starting from `.21`.

| VLAN | DHCP Address Range |
|---:|---|
| 10 | 10.10.10.21 - 10.10.10.254 |
| 20 | 10.10.20.21 - 10.10.20.254 |
| 30 | 10.10.30.21 - 10.10.30.254 |

## Subnet Mask

All current networks use the following subnet mask:

`255.255.255.0`

Equivalent CIDR notation:

`/24`

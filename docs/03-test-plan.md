# Test Plan

This document describes the validation tests performed on the corporate network.

## Connectivity Tests

| Test | Source | Destination | Expected Result |
|---|---|---|---|
| ADMIN local connectivity | PC-ADMIN-01 | PC-ADMIN-02 | Allowed |
| DEVELOPMENT local connectivity | PC-DEV-01 | PC-DEV-02 | Allowed |
| IT gateway connectivity | PC-IT-01 | 10.10.30.1 | Allowed |
| IT to ADMIN connectivity | PC-IT-01 | PC-ADMIN-01 | Allowed |
| DEVELOPMENT to ADMIN connectivity | PC-DEV-01 | PC-ADMIN-01 | Blocked |
| IT to management network | PC-IT-01 | 10.10.99.2 | Allowed |

## DHCP Tests

Each user device must receive:

- An IP address from its corresponding VLAN.
- The correct subnet mask.
- The correct default gateway.

| VLAN | Expected DHCP Range | Expected Gateway |
|---:|---|---|
| 10 | 10.10.10.21 - 10.10.10.254 | 10.10.10.1 |
| 20 | 10.10.20.21 - 10.10.20.254 | 10.10.20.1 |
| 30 | 10.10.30.21 - 10.10.30.254 | 10.10.30.1 |

## SSH Tests

| Source | Destination | Expected Result |
|---|---|---|
| PC-IT-01 | R1-EDGE | Allowed |
| PC-IT-01 | SW-ACCESS-01 | Allowed |
| PC-ADMIN-01 | R1-EDGE | Blocked |
| PC-ADMIN-01 | SW-ACCESS-01 | Blocked |
| PC-DEV-01 | R1-EDGE | Blocked |
| PC-DEV-01 | SW-ACCESS-01 | Blocked |

## Port Security Tests

Each active access port must:

- Learn one sticky MAC address.
- Accept traffic from the authorized device.
- Reject traffic from additional unauthorized MAC addresses.
- Remain operational when using restrict mode.

## Unused Port Tests

Ports assigned to VLAN 999 must:

- Appear as administratively disabled.
- Be separated from production VLANs.
- Reject connections from newly attached devices.

## Verification Commands

The following Cisco IOS commands were used to validate the implementation:

- `show vlan brief`
- `show interfaces trunk`
- `show ip interface brief`
- `show ip dhcp binding`
- `show access-lists`
- `show port-security`
- `show port-security address`
- `show interfaces status`

## Validation Result

All planned network, security, DHCP, SSH, and switch hardening tests were completed successfully.

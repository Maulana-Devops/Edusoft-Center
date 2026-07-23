# Day 4 - DNS Server Configuration

**Date:** 22 July 2026

## Objective

Configure a local DNS Server using BIND9 on Debian 13 as part of the System Administration learning path.

---

## Activities

- Installed BIND9 and supporting packages.
- Created Forward Zone for `pkl.local`.
- Created Reverse Zone for `1.168.192.in-addr.arpa`.
- Configured DNS records (A, NS, PTR).
- Validated the configuration using:
  - `named-checkconf`
  - `named-checkzone`
- Restarted the BIND9 service.
- Tested Forward Lookup using:
  - `dig`
  - `nslookup`
- Tested Reverse Lookup using `dig`.
- Verified that Windows client successfully resolved `server.pkl.local`.

---

## Output

- DNS Server running successfully.
- Forward Lookup operational.
- Reverse Lookup operational.
- Windows client configured to use the Debian DNS Server.
- Domain `server.pkl.local` successfully resolved to `192.168.1.19`.

---

## Skills Learned

- BIND9 Installation
- DNS Configuration
- Forward Zone
- Reverse Zone
- DNS Validation
- DNS Troubleshooting
- Linux Networking

---

## Notes

During the configuration process, several issues were encountered:

- Incorrect reverse zone name (`in-addr-arpa` instead of `in-addr.arpa`).
- Incorrect file path for the reverse zone configuration.
- Differences between BIND9 on Debian 12 and Debian 13 regarding default zone files.

All issues were successfully resolved through troubleshooting and configuration validation.

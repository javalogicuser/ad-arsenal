# AD Arsenal

An interactive Active Directory attack reference and mind map built from real penetration testing engagements, HTB labs, Vulnlab, TryHackMe, CWL, and CPTS exam preparation.

---<img width="1872" height="942" alt="ad_mindmap_view" src="https://github.com/user-attachments/assets/59ee4919-0a55-4abc-9777-9abf3c6cda0a" />

<img width="1519" height="930" alt="ad_arsenal_view" src="https://github.com/user-attachments/assets/62ecbff4-1dac-405d-a977-4407c9c684f0" />

## Overview

Two companion tools in a single repository:

**`ad_mindmap.html`** — A full-screen radial mind map of Active Directory attack techniques. Click any node to jump directly to the corresponding reference card. Branches are colour-coded by category. Supports zoom, pan, search, and branch collapse.

**`ad_arsenal.html`** — A standalone reference document covering the full AD attack chain from unauthenticated enumeration through cross-trust exploitation. Every technique has a copy-able command block, tool list, severity rating, and operational gotchas pulled from real engagement experience.

---

## Coverage

The current version covers twelve attack categories:

- Unauthenticated Enumeration — LDAP anon bind, SMB null sessions, RPC, Kerbrute user enumeration, LLMNR/NBT-NS poisoning
- Initial Access — Password spraying, AS-REP roasting, Kerberoasting
- Authenticated Enumeration — BloodHound collection and Cypher queries, PowerView, NetExec, share hunting, LDAP targeted queries
- ACL Abuse — GenericAll, GenericWrite, WriteDACL, WriteOwner, ForceChangePassword, group membership, DS-Replication
- Delegation — Unconstrained, constrained (S4U2Self/Proxy), RBCD
- Coercion and Relay — Responder, ntlmrelayx, PetitPotam, PrinterBug, Coercer, WebDAV coercion
- ADCS — ESC1, ESC2, ESC3, ESC4, ESC6, ESC7, ESC8, ESC16
- Credential Dumping — DCSync, NTDS.dit via VSS, LSASS, SAM/LSA, GPP passwords, DPAPI
- Lateral Movement — Pass-the-Hash, Pass-the-Ticket, Overpass-the-Hash, WMI, WinRM, RDP
- Ticket Attacks — Golden Ticket, Silver Ticket, Diamond Ticket, Shadow Credentials
- Persistence — AdminSDHolder, DSRM account, SID history injection, DCSync rights, Skeleton Key
- Cross-Trust — ExtraSids child-to-parent, trust key abuse, foreign group membership, SID filtering

---

## Usage

Both files are self-contained single-page HTML with no server or build step required.

**Open locally:**
```
# Clone the repo
git clone https://github.com/ethicalsoup/ad-arsenal.git

# Open in browser
open ad_mindmap.html
```

**Using GitHub Pages:**

Enable Pages on the repository (Settings -> Pages -> Deploy from branch -> main). The files will be served at:
```
https://ethicalsoup.github.io/ad-arsenal/ad_mindmap.html
https://ethicalsoup.github.io/ad-arsenal/ad_arsenal.html
```

---

## Mind Map Controls

| Input | Action |
|---|---|
| Scroll | Zoom in / out |
| Click and drag | Pan |
| Click branch node | Collapse or expand that branch |
| Click leaf node | Scroll to reference card |
| Search box | Filter and highlight matching nodes |
| Legend hover | Isolate a category on the map |
| Legend click | Jump to that category in the reference |
| Reset button (bottom right) | Restore initial zoom and position |

---

## Design Principles

Commands are tested or drawn directly from engagement notes and lab walkthroughs. Each technique card includes:

- The exact tool invocation, not pseudo-code
- Gotcha boxes for common failure points and edge cases
- Tip boxes for opsec considerations and efficiency notes
- Severity ratings based on operational impact

Techniques are marked with the lab or engagement context where they were validated. Patterns from strict lockout environments (three-attempt thresholds, immediate client notification requirements) are noted where relevant.

---

## Living Document

This repository grows with each completed lab and engagement. Planned additions include attack vectors from:

- HTB Pro Labs (POO, Offshore, RastaLabs, Dante, Cybernetics)
- HTB individual machines (ongoing)
- Vulnlab chains and standalone machines
- TryHackMe learning paths and red team rooms
- CWL (CyberWarFare Labs) AD-focused labs
- Real-world engagement patterns (sanitised and generalised)

More obscure and less-documented techniques will be added as they are encountered and validated in labs, including niche delegation abuse paths, lesser-known ADCS escalation conditions, cross-trust edge cases, and Windows-native living-off-the-land tradecraft for high-security environments.

If you find a technique that is wrong, outdated, or missing a critical gotcha, open an issue.

---

## Tools Referenced

The commands in this reference assume the following tools are available:

```
Impacket suite       secretsdump, GetNPUsers, GetUserSPNs, ticketer,
                     psexec, wmiexec, smbexec, addcomputer, rbcd, getST

Certipy              certipy-ad (v4+ for ESC16 --account flag)
NetExec / nxc        cme-compatible, all protocols
evil-winrm           WinRM shell with hash support
BloodHound           bloodhound-python (Linux), SharpHound (Windows)
Rubeus               Kerberos ticket operations (Windows)
Responder            LLMNR/NBT-NS poisoning
coercer              Multi-protocol authentication coercion
PetitPotam           MS-EFSR coercion
pywhisker            msDS-KeyCredentialLink manipulation
PKINITtools          gettgtpkinit, getnthash
kerbrute             Kerberos-based user enumeration and spray
hashcat              GPU cracking (RTX 4080, rockyou2021, rockyou-30000 rules)
PowerView            AD enumeration and ACL manipulation (Windows)
```

---

## Operational Notes

Password spraying in three-attempt lockout environments carries significant risk. This reference consistently recommends offline attacks (Kerberoasting, AS-REP roasting) as the first-choice credential approach in unknown or strict lockout environments. The password policy retrieval step is listed as a prerequisite to any credential attack for this reason.

Commands involving DPAPI, PSCredential decryption, and context-sensitive operations include explicit notes about execution context requirements.

---

*Built by @ethicalsoup. For authorised security testing only.*

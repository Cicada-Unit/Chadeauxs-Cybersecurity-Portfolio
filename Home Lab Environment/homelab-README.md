<div align="center">

# Personal & Family Homelab
### A self-hosted, privacy-minded home infrastructure platform

**One small rack. Three Raspberry Pi nodes. A detached control laptop. A network of services built to make everyday technology more private, reliable, and accessible.**

`SELF-HOSTED` · `DOCKER` · `PORTAINER` · `RASPBERRY PI` · `NETWORKING`

</div>

---

## Overview

This homelab is a personally designed and maintained platform for my household and family. It brings together network storage, device backups, media streaming, DNS filtering, a central service dashboard, and an internal IT help desk.

The goal is to provide a more controlled and approachable alternative to relying entirely on third-party cloud services. Family members can access the services they need through a familiar, easy-to-use interface, while accounts and permissions help keep each person's files and activity appropriately separated.

The physical centerpiece is a **custom-designed 10-inch network rack**. A detached laptop acts as the main administration and control station, while Docker and individual Portainer instances provide a consistent way to manage containerized services across the environment.

## Architecture at a Glance

```text
                         Detached Laptop
                    Primary Administration Station
                                |
                    Portainer / Docker Management
                                |
                 Custom 10-inch Network Rack
                                |
                     Managed PoE Network Switch
                       /          |          \
                      /           |           \
                 Raspberry Pi  Pi 4B       Raspberry Pi 4B
                   5 / NAS     Node 2         Node 3
                      |           |              |
                Storage &      Dashboard      Help Desk
                Backups        DNS Filtering  DNS Filtering
                      |
                Secondary Unmanaged Switch
                      |
              NAS Network Connectivity

        Addressable Power Bar supplies power to the higher-load NAS node
```

*Conceptual overview; this is a service and connectivity map, not a precise wiring diagram.*

## Physical Infrastructure

### Custom 10-inch rack

The rack is a self-designed compact installation intended to keep core network and self-hosted services organized in a small footprint.

- **Managed PoE switch:** provides network connectivity and Power over Ethernet to compatible Raspberry Pi nodes.
- **Secondary unmanaged switch:** extends wired connectivity to the NAS node.
- **Addressable power bar:** supplies power to the more power-demanding NAS hardware.
- **Detached laptop:** serves as the primary administrative workstation and central control point.
- **Raspberry Pi cluster:** three nodes with separate service responsibilities, reducing the need to place every workload on one device.

This layout balances space, power, connectivity, and separation of responsibilities in a compact home-lab environment.

## Node 1 — Raspberry Pi 5
### NAS, shared storage, and family backups

The Raspberry Pi 5 is the storage-focused node. It provides shared household storage and a central destination for family device backups.

**Core services**

- **OpenMediaVault (OMV):** storage administration, disk and filesystem management, and Samba/SMB network shares.
- **RAID 6 storage array:** configured for dual-drive parity, allowing the array to tolerate up to two drive failures within the array under normal RAID 6 assumptions.
- **Image-backup container:** provides a shared destination for full-device image backups, so family members can maintain backups of their computers and other supported devices.
- **Role-based share access:** users are preconfigured with appropriate permissions, helping prevent one family member from casually accessing another person's private files.
- **SMB file sharing:** makes shared and personal storage accessible to authorized devices on the local network.

**Design intent:** provide a household-controlled storage and backup destination, with personal files separated by account and permissions rather than treating the whole NAS as one open shared folder.

**Important resilience note:** RAID is not a backup by itself. It helps with drive-failure tolerance, but does not protect against accidental deletion, malware, theft, fire, controller failure, or other catastrophic loss. A separate offline or off-site backup is still recommended. The actual array protection depends on the drives, filesystem, and configuration in use.

## Node 2 — Raspberry Pi 4B
### Household dashboard and primary DNS filtering

This node provides the household's front door to the homelab, along with network-level filtering.

#### Homepage — service portal

Homepage runs as a Dockerized, browser-based dashboard. It presents hosted services and useful household information in a clear, approachable layout.

- Acts as a shared, clickable bookmark page for the services and programs hosted on the network.
- Organizes service links so family members can find what they need without remembering individual ports or URLs.
- Includes two separate weather API integrations to provide useful weather information and cross-check or supplement displayed conditions.
- Uses a stylized, user-friendly layout with quality-of-life integrations intended to make self-hosted services feel approachable to non-technical users.

#### Pi-hole — primary DNS sinkhole

Pi-hole provides DNS-based filtering for devices using the configured network DNS resolver.

- Filters requests matching configured ad, tracking, and malicious-domain blocklists.
- Uses regularly maintained lists and domain data to reduce exposure to known advertising, tracking, spyware-related, and other unwanted domains.
- Offers network-wide filtering for supported devices without requiring each device to install its own filtering software.

DNS filtering is a useful layer, not a guarantee: it cannot block every ad or threat, and encrypted DNS, VPNs, hard-coded resolvers, or mobile networks may bypass local filtering unless separately managed.

## Node 3 — Raspberry Pi 4B
### IT help desk and secondary DNS filtering

The third node supports issue reporting and adds redundancy for DNS filtering.

#### Zammad — internal IT help desk

Zammad is an open-source help-desk and ticketing platform available to household users for reporting questions, issues, and requests.

- Provides a structured way to submit support tickets, questions, bugs, and service requests.
- Helps organize and prioritize issues instead of relying on informal conversations alone.
- Makes it easier to track requests that have not yet been encountered or diagnosed by the administrator.
- Creates a shared record of reported problems and their resolution.

This turns a family homelab into a small, user-oriented IT environment: household members have a clear place to ask for help, and recurring problems can be documented and triaged.

#### Pi-hole — secondary DNS filtering instance

A second Pi-hole instance provides an additional DNS-filtering endpoint.

- Uses a different subset of blocklists from the primary instance.
- Can distribute DNS requests across configured resolvers when client or network settings are designed to use both.
- Offers another filtering service if one node is unavailable, provided clients are configured to fail over appropriately.

**Configuration note:** a second Pi-hole does not automatically share configuration or guarantee failover. For resilience, clients or DHCP settings must point to both resolvers, and the instances' lists, allowlists, blocklists, and local DNS records should be managed deliberately.

## Service Inventory

| Node | Service | Purpose |
|---|---|---|
| Raspberry Pi 5 | OpenMediaVault | NAS administration and storage management |
| Raspberry Pi 5 | RAID 6 array | Redundant shared storage |
| Raspberry Pi 5 | Image-backup container | Full-device backup destination for family devices |
| Raspberry Pi 5 | Samba / SMB shares | Network file sharing with account-based access |
| Raspberry Pi 4B — Node 2 | Homepage | Central dashboard and service directory |
| Raspberry Pi 4B — Node 2 | Pi-hole | Primary DNS filtering |
| Raspberry Pi 4B — Node 3 | Zammad | Internal support tickets and issue triage |
| Raspberry Pi 4B — Node 3 | Pi-hole | Secondary DNS filtering endpoint |
| Detached laptop | Docker / Portainer administration | Main control and management workstation |
| Managed switch | PoE and network connectivity | Connects and powers compatible nodes |
| Unmanaged switch | Network expansion | Connects the NAS node |
| Addressable power bar | Power delivery | Supplies the higher-load NAS node |

## Management & Operations

### Docker and Portainer

Docker is the common deployment layer for containerized services. Portainer instances provide a visual management interface for the relevant Docker environments.

This approach helps keep service deployment and maintenance consistent across multiple small computers. It also makes it easier to inspect container status, review logs, manage updates, and troubleshoot services without needing to administer every workload in exactly the same way.

### Administration workflow

A typical maintenance cycle includes:

1. Check the status of containers and critical services.
2. Review logs when a service behaves unexpectedly.
3. Apply updates deliberately and confirm that important services return successfully.
4. Verify DNS resolution, shared-file access, backups, and media playback.
5. Keep service configuration and recovery information documented.
6. Test restoration procedures rather than assuming a successful backup job guarantees recoverability.

## Privacy, Access Control & Household Usability

The homelab is designed for personal and family use, so usability and separation of users are core requirements.

- **Individual accounts:** supported services use per-user accounts where available.
- **Role-based access:** file shares are configured to limit access to the appropriate user or group.
- **Central service directory:** Homepage makes services easier to discover and reduces the need to memorize addresses.
- **Local network filtering:** Pi-hole applies DNS policies to devices using the configured resolvers.
- **Structured support:** Zammad provides a predictable route for reporting issues and requests.
- **Self-hosted services:** keeps more household data and service administration under local control.

Self-hosting also creates responsibility. Strong passwords, timely updates, least-privilege permissions, secure remote-access practices, and tested backups remain important. Services should not be exposed directly to the public internet without a deliberate security design.

## What This Homelab Demonstrates

This environment is a practical example of combining several disciplines into one working system:

- Linux-based administration and troubleshooting
- Containerized service deployment and management
- Network switching, PoE, and multi-node connectivity
- NAS configuration, file sharing, and storage redundancy
- User and role-based access control
- Backup infrastructure and recovery planning
- DNS-based security and content filtering
- Self-hosted media and household service delivery
- Help-desk workflow design and issue triage
- Service monitoring, log review, and iterative troubleshooting
- Designing infrastructure around real users—not just technical convenience

## Future Improvements & Ongoing Considerations

Areas worth evaluating as the environment grows:

- Add an independent offline or off-site backup target and periodically test restores.
- Document storage health checks, RAID status, and SMART monitoring.
- Monitor container health, disk capacity, temperatures, and power events.
- Maintain versioned configuration backups and a recovery checklist.
- Review DNS blocklists and false positives periodically.
- Confirm secondary DNS behavior during primary-node outages.
- Keep administrative interfaces on trusted network segments and restrict access where practical.
- Document the network topology, IP assignments, ports, and service dependencies.

---

<div align="center">

**Built for the household. Managed with intention. Improved one service at a time.**

*Personal homelab · Family infrastructure · Self-hosted services*

</div>

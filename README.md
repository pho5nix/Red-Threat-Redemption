# Red-Threat-Redemption SIEM

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)  

## Overview
Red-Threat-Redemption is a comprehensive, open-source SIEM (Security Information and Event Management) stack inspired by the rugged vigilance of *Red Dead Redemption*. Built on Debian 13 in a Proxmox VM, it integrates Elasticsearch, Kibana, Vector (for log processing), Wazuh Manager (for endpoint security monitoring), Zeek (for network analysis on PCI passthrough secondary NIC), and pfSense log ingestion (syslog and Suricata EVE JSON).  

This repo provides step-by-step guides to deploy a high-performance SIEM for threat detection, log aggregation, and visualization. Optimized for 32GB RAM, 8 cores, and secure configurations—no plaintext passwords, minimal footprint, and best practices for efficiency.

### Key Features
- **Minimal Debian 13 Base**: Hardened OS setup with LVM partitioning for flexible storage.  
- **ELK Stack with Vector**: Elasticsearch for storage/search, Kibana for visualization, Vector for lightweight log pipelines (replaces Logstash).  
- **Wazuh Integration**: Security monitoring with alerts ingested into Elasticsearch.  
- **Zeek Network Monitoring**: Passive analysis on PCI passthrough NIC.  
- **pfSense Logs**: System syslog and Suricata EVE JSON.  
- **Security Focus**: TLS, keystores for secrets, no swap, high file limits.  
- **RDR2-Inspired Naming**: Fun, thematic puns for a memorable repo.

## Prerequisites
- Proxmox VE hypervisor with IOMMU enabled.  
- pfSense firewall configured for log forwarding.  
- Basic Linux knowledge; root/sudo access.  
- Hardware: 32GB RAM, 8 cores, ≥220GB storage, 2 NICs (one for PCI passthrough).

## Installation Guides
Follow these guides in sequence. Each is self-contained but builds on the previous.

### 1. Debian 13 Installation and Configuration
[Debian Guide](./docs/debian-install.md)  
- VM setup in Proxmox.  
- Minimal netinst install with LVM partitioning.  
- Hardening, tuning, and SSH security.

### 2. ELK Stack & Wazuh Setup
[ELK & Wazuh Guide](./docs/elk-wazuh.md)  
- Install Elasticsearch, Kibana, Vector, Wazuh Manager.  
- Secure configurations (TLS, keystores for passwords).  
- Vector pipeline for Wazuh alerts.  
- Kibana data views.

### 3. Zeek Integration (PCI Passthrough NIC)
[Zeek Guide](./docs/zeek-integration.md)  
- Add and verify PCI NIC.  
- Install and configure Zeek.  
- Vector pipeline for Zeek logs.  
- Kibana data view for Zeek events.

### 4. pfSense Logs Integration
[pfSense Guide](./docs/pfsense-logs.md)  
- Configure pfSense: Syslog for system logs, syslog-ng for Suricata EVE JSON.  
- Vector pipelines for ingestion and parsing.  
- Kibana data views for pfSense and Suricata.

## Usage
1. Clone the repo:  
   ```
   git clone https://github.com/yourusername/red-threat-redemption.git
   ```
2. Follow the guides sequentially.  
3. Access Kibana (use elastic credentials).  
4. Monitor dashboards in Kibana for Wazuh alerts, Zeek events, and pfSense logs.  
5. Tune Vector configs in `/etc/vector/vector.yaml` for additional sources.

### Verification
After setup, use the checklists in each guide. Example:  
- Elasticsearch: Check connectivity.  
- Vector: Inspect logs.  
- Indices: Check in Kibana Discover.

## Troubleshooting
Common issues across guides:  
- **Connection Failures**: Verify TLS certs and secrets.  
- **Log Ingestion**: Check firewalls and configurations.  
- **Performance**: Monitor RAM; adjust ES heap if needed.  
- **Errors in Vector**: Inspect service logs for parse issues.  

Refer to individual guides for tool-specific troubleshooting.

## Contributing
Contributions welcome! Fork the repo, create a feature branch, and submit a PR. Follow the code of conduct.

## License
MIT License. See [LICENSE](./LICENSE) for details.

## Acknowledgments
- Inspired by *Red Dead Redemption 2* for thematic naming.  
- Thanks to Elastic, Wazuh, Vector, Zeek, and pfSense communities.  
- Built for cybersecurity enthusiasts.

Happy hunting threats!

# Red-Threat-Redemption SIEM

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)  

## Overview
Red-Threat-Redemption is a comprehensive, open-source SIEM (Security Information and Event Management) stack inspired by *Red Dead Redemption 2*. Built on Debian 13 in a Proxmox VM, it integrates Elasticsearch, Kibana, Vector (for log processing), Wazuh Manager (for endpoints security), Zeek (for network analysis on a secondary SPAN/Port-based NIC), and pfSense logs ingestion(System Logs and Suricata EVE JSON) sending from Syslog-ng pfSense packege.  

This repo provides step-by-step guides to deploy a high-performance SIEM for threat detection, log aggregation, and visualization. Optimized for 32GB RAM, 4 cores, and secure configurations—no plaintext passwords, minimal footprint, and best practices for efficiency.

### Key Features
- **Minimal Debian 13 Base**: Hardened OS setup with LVM partitioning for flexible storage.  
- **ELK Stack with Vector**: Elasticsearch for storage/search, Kibana for visualization, Vector for lightweight log pipelines.  
- **Wazuh Integration**: Security monitoring with alerts ingested into Elasticsearch.  
- **Zeek Network Monitoring**: Passive analysis on PCI passthrough NIC.  
- **pfSense Logs**: System syslog and Suricata EVE JSON.  
- **Security Focus**: TLS, keystores for secrets, no swap, high file limits.  

## Prerequisites
- Proxmox VE hypervisor with IOMMU enabled (This guide is focused on Proxmox VE but you can setup the infrastructure in any Hypervisor).  
- Basic Linux knowledge; root/sudo access.  
- Hardware: 32GB RAM, 4 cores, 220GB storage, 2 NICs (the secondary NIC should be setup for SPAN from your switch, mirroring the port you want. In my case my mirrored port is the trunk port of the switch).

## Installation Guides
Follow these guides in sequence. Each is self-contained but builds on the previous.

### 1. Debian 13 Installation and Configuration
[Debian Guide](./docs/debian-install.md)  
- VM setup in Proxmox.  
- Minimal netinst install with LVM partitioning.  
- Hardening and tuningg

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
- Install and configure Syslog-ng
- Configure system logs for Syslog-ng
- Configure Syslog-ng for Suricata EVE JSON.  
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

## Troubleshooting
Common issues across guides:  
- **Connection Failures**: Verify TLS certs and secrets.  
- **Log Ingestion**: Check vector.yaml, inspect service logs for parse issues.
- **Performance**: Monitor RAM; adjust ES heap if needed.
- Refer to individual guides for tool-specific troubleshooting.

## Contributing
Contributions welcome! Fork the repo, create a feature branch.

## License
MIT License. See [LICENSE](./LICENSE) for details.

## Acknowledgments
- Inspired by *Red Dead Redemption 2* for thematic naming to separate the componets for a memoprable repo.  
- Thanks to Elastic, Wazuh, Vector, Zeek, and pfSense communities.  
- Built for cybersecurity enthusiasts.

Happy hunting threats!

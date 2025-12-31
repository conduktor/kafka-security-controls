# Kafka Security Controls

A comprehensive mapping of **118 Apache Kafka security controls** to industry standards (CWE, NIST 800-53, PCI-DSS).

**[View Interactive Controls Browser](https://conduktor.github.io/kafka-security-controls)**

## Overview

This repository provides a structured catalog of security controls for Apache Kafka deployments, covering:

- **Authentication** - SASL (SCRAM, Kerberos, OAuth), mTLS, credential management
- **Encryption** - TLS in transit, at-rest encryption, cipher configuration
- **Authorization** - Topic ACLs, consumer group ACLs, cluster operations, RBAC/ABAC
- **Audit** - Logging, SIEM integration, change tracking
- **Availability** - Replication, disaster recovery, quotas
- **Network Security** - Listener isolation, segmentation
- **Infrastructure** - ZooKeeper, KRaft security
- **Ecosystem** - Kafka Connect, Schema Registry, REST Proxy, MirrorMaker 2, Kafka Streams
- **Data Protection** - Encryption, masking, PII handling, lineage, data contracts
- **Operations** - Patching, hardening, IaC, incident response
- **Monitoring** - Security metrics, anomaly detection, alerting

## File Structure

```
kafka_security_controls.csv
├── sectionID      # Unique control identifier (e.g., KAFKA-AUTH-001)
├── section        # Control category
├── subsection     # Specific control name
├── description    # Detailed description and configuration guidance
├── category       # High-level category
├── cwe_ids        # Related CWE weaknesses (comma-separated)
├── nist_refs      # Related NIST 800-53 controls (comma-separated)
├── pci_refs       # Related PCI-DSS requirements
└── hyperlink      # Reference documentation URL
```

## Integration with OpenCRE

This mapping is designed to integrate with [OpenCRE (Open Common Requirement Enumeration)](https://www.opencre.org), an OWASP project that unifies security standards.

### How it works

```
Kafka Security Control → CWE → OpenCRE → Other Standards
        │                              │
        │                              ├── NIST 800-53
        │                              ├── ISO 27001
        │                              ├── PCI-DSS
        │                              ├── ASVS
        │                              └── ...
        │
        └── Direct mappings to NIST/PCI included
```

### Using with OpenCRE

1. **Import to OpenCRE**: Use the OpenCRE parser at [`application/utils/external_project_parsers/parsers/kafka_security.py`](https://github.com/OWASP/OpenCRE)
2. **Query relationships**: Once imported, query OpenCRE to find equivalent controls across standards
3. **Gap analysis**: Identify which Kafka controls map to your compliance requirements

## Control Categories

| Category | Count | Description |
|----------|-------|-------------|
| Authentication | 14 | Identity verification mechanisms |
| Encryption | 10 | Data protection in transit and at rest |
| Authorization | 15 | Access control and permissions |
| Audit | 10 | Logging and compliance tracking |
| Availability | 11 | HA, DR, and resource quotas |
| Network Security | 5 | Network isolation and segmentation |
| Infrastructure | 8 | ZooKeeper and KRaft security |
| Ecosystem | 15 | Connect, Schema Registry, REST, MM2, Streams |
| Data Protection | 13 | Encryption, masking, lineage, contracts |
| Operations | 11 | Hardening, patching, IaC |
| Monitoring | 6 | Metrics, alerts, anomaly detection |

## Verification Coverage

When using [Conduktor Gateway](https://conduktor.io) as a Kafka proxy with the Conduktor Platform:

| Verification Level | Controls | Coverage |
|-------------------|----------|----------|
| Fully Automated | 107 | 91% |
| Partially Automated | 6 | 5% |
| Manual Attestation | 5 | 4% |

## Usage Examples

### Find controls for a specific CWE

```bash
grep "287" kafka_security_controls.csv  # CWE-287: Improper Authentication
```

### Find all encryption controls

```bash
grep "Encryption" kafka_security_controls.csv
```

### Generate compliance report

```python
import csv

with open('kafka_security_controls.csv') as f:
    reader = csv.DictReader(f)
    pci_controls = [r for r in reader if r['pci_refs']]
    print(f"PCI-DSS relevant controls: {len(pci_controls)}")
```

## Contributing

Contributions welcome! To add or update controls:

1. Edit `kafka_security_controls.csv`
2. Ensure CWE/NIST/PCI mappings are accurate
3. Include hyperlink to official documentation
4. Submit a PR

## References

- [Apache Kafka Security Documentation](https://kafka.apache.org/documentation/#security)
- [OpenCRE - Open Common Requirement Enumeration](https://www.opencre.org)
- [CWE - Common Weakness Enumeration](https://cwe.mitre.org)
- [NIST 800-53 Security Controls](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final)
- [PCI-DSS Requirements](https://www.pcisecuritystandards.org)
- [Conduktor Security Documentation](https://docs.conduktor.io)

## License

This work is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

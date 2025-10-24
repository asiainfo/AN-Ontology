# 5GC Ontology Summary

## Executive Summary

This ontology defines a comprehensive data model for 5G Core Network (5GC) architecture and network element management, covering core network functions including AMF, SMF, UPF, UDM, and their relationships. The ontology is structured into several main sections:

### Overview Statistics
- **Total Classes**: 35 main classes
- **Total Object Properties**: 62 relationship properties
- **Total Data Properties**: 23 attribute properties
- **Total Enumerations**: 4 enumeration types
- **Total Enum Values**: 26 distinct values
- **Main Categories**: 6 (Core Network Functions, Service Components, Licensing, Capabilities, Interfaces, Deployment)

---

## Ontology Structure

```
5G Core Network Ontology
│
├─ Core Network Functions
│   ├─ NetworkFunction (base class)
│   │   ├─ has_neType → NEType [Enum]
│   │   ├─ has_neId → Integer
│   │   └─ has_neName → String
│   │
│   ├─ AMF (Access and Mobility Management Function)
│   │   ├─ inherits → NetworkFunction properties
│   │   ├─ has_basicInfo → AMFBasicInfo [Class]
│   │   ├─ has_serviceInfo → ServiceConfig [Class]
│   │   ├─ has_serviceResource → ServiceResource [Class]
│   │   ├─ has_spComponent → ServiceComponent [Class]
│   │   ├─ has_deploymentMethod → DeploymentMethod [Class]
│   │   ├─ has_license → AMFLicense [Class]
│   │   ├─ has_capability → AMFCapabilityExposure [Class]
│   │   └─ connects_via → Interface [Class][]
│   │       ├─ N2Interface (AMF-GNB)
│   │       ├─ N8Interface (AMF-UDM)
│   │       ├─ N11Interface (AMF-SMF)
│   │       ├─ N12Interface (UDM-AUSF)
│   │       ├─ N14Interface (AMF-other AMF)
│   │       ├─ N15Interface (AMF-PCF)
│   │       └─ N22Interface (AMF-NSSF)
│   │
│   ├─ SMF (Session Management Function)
│   │   ├─ inherits → NetworkFunction properties
│   │   ├─ has_basicInfo → SMFBasicInfo [Class]
│   │   ├─ has_serviceInfo → ServiceConfig [Class]
│   │   ├─ has_serviceResource → ServiceResource [Class]
│   │   ├─ has_spComponent → ServiceComponent [Class]
│   │   ├─ has_deploymentMethod → DeploymentMethod [Class]
│   │   ├─ has_license → SMFLicense [Class]
│   │   ├─ has_capability → SMFCapabilityExposure [Class]
│   │   └─ connects_via → Interface [Class][]
│   │       ├─ N4Interface (SMF-UPF)
│   │       ├─ N10Interface (SMF-UDM)
│   │       ├─ N11Interface (AMF-SMF)
│   │       └─ N7Interface (SMF-PCF)
│   │
│   ├─ UDM (Unified Data Management)
│   │   ├─ inherits → NetworkFunction properties
│   │   ├─ has_basicInfo → UDMBasicInfo [Class]
│   │   ├─ has_serviceInfo → ServiceConfig [Class]
│   │   ├─ has_serviceResource → ServiceResource [Class]
│   │   ├─ has_spComponent → ServiceComponent [Class]
│   │   ├─ has_deploymentMethod → DeploymentMethod [Class]
│   │   ├─ has_license → UDMLicense [Class]
│   │   ├─ has_capability → UDMCapabilityExposure [Class]
│   │   └─ connects_via → Interface [Class][]
│   │       ├─ N8Interface (AMF-UDM)
│   │       ├─ N10Interface (UDM-SMF)
│   │       ├─ N12Interface (UDM-AUSF)
│   │       └─ N21Interface (UDM-SMSF)
│   │
│   └─ UPF (User Plane Function)
│       ├─ inherits → NetworkFunction properties
│       ├─ has_basicInfo → UPFBasicInfo [Class]
│       ├─ has_serviceInfo → ServiceConfig [Class]
│       ├─ has_serviceResource → ServiceResource [Class]
│       ├─ has_spComponent → ServiceComponent [Class]
│       ├─ has_deploymentMethod → DeploymentMethod [Class]
│       ├─ has_license → UPFLicense [Class]
│       ├─ has_capability → UPFCapabilityExposure [Class]
│       └─ connects_via → Interface [Class][]
│           ├─ N3Interface
│           ├─ N4Interface (SMF-UPF)
│           ├─ N6Interface
│           ├─ N9Interface
│           ├─ S1uInterface
│           ├─ SGWU_S5S8Interface
│           └─ PGWU_S5S8Interface
│
├─ Service Components
│   ├─ ServiceComponent [Class]
│   │   └─ (Business processing plane for network elements)
│   │
│   ├─ ServiceConfig [Class]
│   │   └─ (Service information configuration)
│   │
│   └─ ServiceResource [Class]
│       └─ (Service resource information)
│
├─ Licensing
│   ├─ License (base class)
│   │
│   ├─ AMFLicense [Class]
│   │   ├─ has_totalUsers → Integer
│   │   ├─ has_usersPerUnit → Integer
│   │   └─ has_maxUnitNum → Integer
│   │
│   ├─ SMFLicense [Class]
│   │   ├─ has_totalSessions → Integer
│   │   ├─ has_sessionsPerUnit → Integer
│   │   └─ has_maxUnitNum → Integer
│   │
│   ├─ UDMLicense [Class]
│   │   ├─ has_totalUsers → Integer
│   │   ├─ has_usersPerUnit → Integer
│   │   └─ has_maxUnitNum → Integer
│   │
│   └─ UPFLicense [Class]
│       ├─ has_upfSpSessNum → Integer
│       ├─ has_upfSpBandWidth → Integer
│       └─ has_upfSpNum → Integer
│
├─ Capabilities
│   ├─ CapabilityExposure (base class)
│   │
│   ├─ NECapabilityExposure [Class]
│   │   └─ has_NECapabilityExposure → Function [Class]
│   │
│   ├─ AMFCapabilityExposure [Class]
│   │   ├─ inherits → NECapabilityExposure properties
│   │   ├─ has_QuerySctp → Function [Class]
│   │   ├─ has_QueryRan → Function [Class]
│   │   ├─ has_QueryHttp → Function [Class]
│   │   └─ has_QueryAmfUser → Function [Class]
│   │
│   ├─ SMFCapabilityExposure [Class]
│   │   ├─ inherits → NECapabilityExposure properties
│   │   ├─ has_QueryHttp2LinkStatus → Function [Class]
│   │   └─ has_QueryUpfLinkstatus → Function [Class]
│   │
│   ├─ UDMCapabilityExposure [Class]
│   │   ├─ inherits → NECapabilityExposure properties
│   │   ├─ has_QueryAmfReg → Function [Class]
│   │   └─ has_QuerysmfReg → Function [Class]
│   │
│   └─ UPFCapabilityExposure [Class]
│       ├─ inherits → NECapabilityExposure properties
│       ├─ has_QueryStat → Function [Class]
│       └─ has_QueryAssoc → Function [Class]
│
├─ Interfaces
│   └─ Interface [Class]
│       ├─ has_interfaceType → InterfaceType [Enum]
│       ├─ has_ipType → IPType [Enum]
│       ├─ has_ipAddr → String
│       ├─ has_ipMask → Integer
│       ├─ has_status → InterfaceStatus [Enum]
│       ├─ has_ne → NetworkFunction [Class]
│       ├─ has_adjNe → NetworkFunction [Class]
│       └─ has_connectTo → Interface [Class]
│
└─ Deployment
    ├─ DeploymentMethod (abstract class)
    │
    ├─ DockerDeployment [Class]
    │   └─ (Docker container deployment)
    │
    └─ KubernetesDeployment [Class]
        └─ (Kubernetes deployment)
```

## Type Definitions

### Composite Types (Class)

```
AMFBasicInfo [Class] {
    // AMF basic information class
}

SMFBasicInfo [Class] {
    // SMF basic information class
}

UDMBasicInfo [Class] {
    // UDM basic information class
}

UPFBasicInfo [Class] {
    // UPF basic information class
}

ServiceComponent [Class] {
    // Network element service process
}

ServiceConfig [Class] {
    // Service information configuration
}

ServiceResource [Class] {
    // Service resource information
}

Function [Class] {
    // Function class for capability operations
}
```

### Enumeration Types (Enum)

```
# Network Element Types
NEType [Enum] = [AMF|SMF|UDM|UPF]

# Interface Status
InterfaceStatus [Enum] = [InterfaceUnknown|InterfaceUp|InterfaceDown]

# IP Types
IPType [Enum] = [IPv4|IPv6]

# Interface Types
InterfaceType [Enum] = [
    InfterfaceN2|InfterfaceN3|InfterfaceN4|InfterfaceN6|
    InfterfaceN7|InfterfaceN8|InfterfaceN9|InfterfaceN10|
    InfterfaceN11|InfterfaceN12|InfterfaceN14|InfterfaceN15|
    InfterfaceN21|InfterfaceN22|InfterfaceS1u|
    InfterfaceSgwuS5S8|InfterfacePgwuS5S8
]
```

## Key Relationships

### Interface Connectivity
- **ne**: Local network element of the interface
- **adjNe**: Adjacent network element of the interface  
- **connectTo**: Peer interface information

### Network Function Composition
- Each network function (AMF, SMF, UDM, UPF) has:
  - Basic information class
  - Service configuration
  - Service resources
  - Service components
  - Deployment method
  - License configuration
  - Capability exposure
  - Multiple interface connections

### Licensing Structure
- **AMFLicense**: User-based capacity licensing
- **SMFLicense**: Session-based capacity licensing  
- **UDMLicense**: User-based capacity licensing
- **UPFLicense**: Session and bandwidth-based licensing

### Capability Hierarchy
- **CapabilityExposure** → **NECapabilityExposure** → Specific function capabilities
- Each capability exposure class provides specific operational functions for monitoring and management

### Interface Management
- **Interface**: Standardized representation of all network interfaces
- **InterfaceType**: Comprehensive enumeration of 5GC interface types
- **InterfaceStatus**: Real-time status monitoring

### Deployment Methods
- **DockerDeployment**: Container-based deployment
- **KubernetesDeployment**: Orchestrated container deployment

---

## Design Principles

1. **Standards Compliance**: Based on 3GPP 5G core network standards
2. **Modularity**: Clear separation between network functions, interfaces, licensing, capabilities, and deployment
3. **Extensibility**: Base classes allow for future network function additions
4. **Operational Focus**: Includes both configuration and runtime capability exposure
5. **Multi-deployment Support**: Supports both Docker and Kubernetes deployment models
6. **Clear Separation**: Independent modeling of interfaces and deployment concerns
7. **Comprehensive Interface Coverage**: Complete representation of 5GC standard interfaces

This ontology provides a comprehensive semantic model for 5G core network management, enabling standardized representation of network elements, their relationships, licensing models, operational capabilities, interface connectivity, and deployment options across different environments.
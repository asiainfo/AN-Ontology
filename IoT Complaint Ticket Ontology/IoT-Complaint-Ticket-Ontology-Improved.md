# IoT Complaint Ticket Ontology

## Executive Summary

This ontology defines a comprehensive data model for IoT Complaint ticket management systems, covering the complete lifecycle from Complaint detection to resolution. The ontology is structured into three main sections:

### Overview Statistics
- **Total Classes**: 30 composite types
- **Total Enumerations**: 42 enumeration types
- **Total Enum Values**: 183 distinct values
- **Main Categories**: 4 (Core Business, Device & Network, Complaint & Diagnosis, Data Analysis)

---

## Ontology Structure

```
IoT Complaint Ticket Ontology
│
├─ Core Business Objects
│   ├─ Ticket
│   │   ├─ has_id → String
│   │   ├─ has_status → TicketStatus [Enum]
│   │   ├─ has_priority → Priority [Enum]
│   │   ├─ created_at → DateTime
│   │   ├─ updated_at → DateTime
│   │   ├─ assigned_to → Team [Class]
│   │   ├─ reported_by → Customer
│   │   ├─ describes → Complaint
│   │   ├─ affects → Service
│   │   └─ requires → TestCoordination [Class]
│   │
│   ├─ Customer
│   │   ├─ has_id → String
│   │   ├─ has_name → String
│   │   ├─ has_tier → CustomerTier [Enum]
│   │   ├─ has_contact → ContactInfo [Class]
│   │   ├─ owns → Device[]
│   │   └─ subscribes_to → Service[]
│   │
│   └─ Service
│       ├─ has_id → String
│       ├─ has_type → ServiceType [Enum]
│       ├─ has_policy → Policy [Class]
│       ├─ has_sla → SLA [Class]
│       └─ provided_to → Customer[]
│
├─ Device and Network
│   ├─ Device
│   │   ├─ has_type → DeviceType [Enum]
│   │   ├─ has_capability → NetworkCapability [Enum]
│   │   ├─ uses → SIMCard
│   │   ├─ located_at → Location [Class]
│   │   ├─ experiences → Complaint[]
│   │   └─ consumes → DataVolume [Class]
│   │
│   ├─ SIMCard
│   │   ├─ has_iccid → String
│   │   ├─ has_msisdn → String
│   │   ├─ has_imsi → String
│   │   ├─ has_type → CardType [Enum]
│   │   ├─ has_status → CardStatus [Enum]
│   │   ├─ configured_with → NetworkConfig
│   │   ├─ bound_to → Device
│   │   └─ binding_type → BindingType [Enum]
│   │
│   ├─ NetworkConfig
│   │   ├─ has_apn → APN [Class]
│   │   ├─ has_capabilities → NetworkCapability [Enum][]
│   │   ├─ has_restrictions → AccessRestriction [Class][]
│   │   ├─ has_qos → QoSProfile [Class]
│   │   └─ has_regional_policy → RegionalPolicy [Class][]
│   │
│   └─ Network
│       ├─ has_element → NetworkElement [Class][]
│       ├─ has_coverage → Coverage [Class]
│       └─ has_performance → Performance [Class]
│
├─ Complaint and Diagnosis Objects
│   ├─ Complaint Hierarchy
│   │   ├─ Complaint (base class)
│   │   │   ├─ has_id → String
│   │   │   ├─ has_type → ComplaintType [Enum]
│   │   │   ├─ has_subtype → NetworkComplaintSubtype/DeviceComplaintSubtype/ConfigurationComplaintSubtype/BulkComplaintSubtype [Enum]
│   │   │   ├─ has_symptom → Symptom [Class][]
│   │   │   ├─ detected_at → DateTime
│   │   │   ├─ occurred_at → Location [Class]
│   │   │   ├─ affects → Device[]
│   │   │   ├─ has_root_cause → RootCause [Class]
│   │   │   └─ resolved_by → Resolution [Class]
│   │   │
│   │   └─ Specialized Complaints (extends Complaint)
│   │       ├─ LocationDrift
│   │       │   ├─ inherits → Complaint properties
│   │       │   ├─ actual_location → Location [Class]
│   │       │   ├─ reported_location → Location [Class]
│   │       │   ├─ drift_distance → Float (km)
│   │       │   ├─ drift_direction → Direction [Enum]
│   │       │   ├─ business_impact → BusinessImpact [Class]
│   │       │   └─ frequency → DriftFrequency [Enum]
│   │       │
│   │       └─ FakeBaseStation
│   │           ├─ inherits → Complaint properties
│   │           ├─ detection_method → DetectionMethod [Class]
│   │           ├─ affected_network → NetworkType [Enum]
│   │           ├─ mitigation → MitigationStrategy [Class]
│   │           └─ reported_location → Location [Class]
│   │
│   └─ Complaint Analysis
│       └─ BulkComplaintPattern
│           ├─ pattern_id → String
│           ├─ affected_scale → Scale [Enum]
│           ├─ trigger_time → DateTime
│           ├─ trigger_cause → TriggerCause [Enum]
│           ├─ geographic_pattern → GeographicPattern [Enum]
│           └─ related_Complaints → Complaint[]
│
└─ Data Analysis Objects
    ├─ SignalQuality
    │   ├─ rsrp_level → Float (dBm)
    │   ├─ coverage_type → CoverageType [Enum]
    │   ├─ network_type → NetworkType [Enum]
    │   └─ optimization_needed → Boolean
    │
    ├─ DataConsumption
    │   ├─ monitoring_period → DateRange [Class]
    │   ├─ total_usage → DataVolume [Class]
    │   ├─ usage_pattern → UsagePattern [Class]
    │   ├─ anomaly_detection → AnomalyType [Enum]
    │   └─ billing_dispute → Boolean
    │
    └─ TimePattern
        ├─ pattern_type → TimePatternType [Enum]
        ├─ affected_period → TimePeriod [Class]
        ├─ normal_period → TimePeriod [Class]
        └─ impact_scale → Integer
```

## Type Definitions

### Composite Types (Class)

```
ContactInfo [Class] {
    primary_phone: String
    backup_phone: String
    email: String
    wechat: String
    availability: String (Working hours)
}

Location [Class] {
    province: String
    city: String
    district: String
    address: String
    coordinates: Coordinates
    location_type: LocationType
}

Coordinates [Class] {
    latitude: Float
    longitude: Float
}

SLA [Class] {
    sla_id: String
    availability: Float (99.9%)
    response_time: Duration
    resolution_time: Duration
    escalation_threshold: Duration
    penalty_clause: String
}

Duration [Class] {
    value: Integer
    unit: TimeUnit
}

DataVolume [Class] {
    value: Float
    unit: DataUnit
    period: DateRange
}

DateRange [Class] {
    start_date: DateTime
    end_date: DateTime
    duration: Duration
}

Team [Class] {
    team_id: String
    team_name: String
    team_type: TeamType
    contact: ContactInfo
}

TestCoordination [Class] {
    contact_person: String
    contact_phone: String
    available_time: TimeRange
    test_type: TestType
    cooperation_level: CooperationLevel
}

NetworkElement [Class] {
    element_id: String
    element_name: String
    type: ElementType
    status: ElementStatus
    location: String
}

Coverage [Class] {
    signal_strength: SignalLevel
    network_type: NetworkType
    area: Location[]
    quality_score: Float
}

Performance [Class] {
    latency: Integer (ms)
    packet_loss: Float (%)
    throughput: Integer (Mbps)
}

Symptom [Class] {
    symptom_id: String
    symptom_type: SymptomType
    severity: SeverityLevel
    frequency: String
}

RootCause [Class] {
    cause_id: String
    cause_type: CauseType
    confidence_level: Float (0-1)
    evidence: String[]
}

Resolution [Class] {
    resolution_id: String
    resolution_type: ResolutionType
    implemented_by: Team
    implementation_time: DateTime
    success_rate: Float
    notes: String
}

BusinessImpact [Class] {
    impact_id: String
    fee_impact: String
    service_impact: String
    user_complaints: Integer
    reputation_impact: String
    severity: SeverityLevel
}

Parameter [Class] {
    name: String
    value: String
    type: String
}

Condition [Class] {
    condition_id: String
    expression: String
    parameters: Parameter[]
    operator: LogicalOperator
}

Action [Class] {
    action_id: String
    action_type: ActionType
    parameters: Parameter[]
    target: String
}

Rule [Class] {
    rule_id: String
    rule_name: String
    condition: Condition
    action: Action
    priority: Integer
}

AccessRestriction [Class] {
    restriction_id: String
    network_type: NetworkType
    restriction_level: RestrictionLevel
    reason: String
}

QoSProfile [Class] {
    profile_id: String
    uplink_rate: Integer (bps)
    downlink_rate: Integer (bps)
    priority: Integer (1-9)
    latency_requirement: Integer (ms)
    packet_loss_tolerance: Float (%)
}

APN [Class] {
    apn_name: String (e.g. CMIOT, CMNBIOT)
    apn_type: APNType
    gateway_address: String
    authentication: AuthType
}

RegionalPolicy [Class] {
    policy_id: String
    region: Location
    allowed_services: ServiceType[]
    restrictions: AccessRestriction[]
}

Policy [Class] {
    has_id: String
    has_type: PolicyType
    has_rules: Rule[]
    applies_to: Service[]
    has_priority: Integer
}

DetectionMethod [Class] {
    method_id: String
    method_type: DetectionMethodType
    confidence: Float
}

MitigationStrategy [Class] {
    strategy_id: String
    strategy_type: String
    actions: Action[]
    effectiveness: Float
}

UsagePattern [Class] {
    pattern_id: String
    top_domains: Domain[]
    peak_hours: Hour[]
    average_daily: DataVolume
    pattern_type: String
    anomaly_score: Float
}

Domain [Class] {
    domain_name: String
    traffic_volume: DataVolume
    percentage: Float
}

TimePeriod [Class] {
    start_time: Time
    end_time: Time
    timezone: String
    recurring: Boolean
}
```

### Enumeration Types (Enum)

```
# Network Related
NetworkType [Enum] = [2G|3G|4G|5G|NB-IoT]
NetworkCapability [Enum] = [2G|3G|4G|NB-IoT]
ElementType [Enum] = [MSC|MME|HSS|PGW|SGSN|UPF]
ElementStatus [Enum] = [Normal|Degraded|Failed|Maintenance]
SignalLevel [Enum] = [Excellent|Good|Fair|Poor|NoSignal]
CoverageType [Enum] = [Indoor|Outdoor|Underground|HighSpeed|Tunnel]

# Ticket Related
TicketStatus [Enum] = [Open|InProgress|Pending|Resolved|Closed]
Priority [Enum] = [Urgent|High|Medium|Low]
CustomerTier [Enum] = [Gold|Silver|Bronze|Standard]

# Service Related
ServiceType [Enum] = [DataService|VoiceService|SMSService|LocationService|IoTService]
PolicyType [Enum] = [TrafficPolicy|AccessPolicy|QoSPolicy|SecurityPolicy|BillingPolicy]
APNType [Enum] = [Generic|Enterprise|Regional|Service|Test]
AuthType [Enum] = [None|PAP|CHAP|EAP]

# Device Related
DeviceType [Enum] = [ChargingStation|SmartMeter|VehicleTerminal|BroadcastingSpeaker|SharedElectricVehicle|SmartBatterySwapCabinet|WaterDispenserController|WashingMachine|MiFi|NBGasMeter|GPS|POS]
CardType [Enum] = [USIM|eSIM|NanoSIM]
CardStatus [Enum] = [Active|Suspended|Inactive|Testing|BulkOffline|Terminated]
BindingType [Enum] = [Embedded|Removable|DeviceBound]

# Complaint Related
ComplaintType [Enum] = [NetworkComplaint|DeviceComplaint|ConfigurationComplaint|BulkComplaint]
NetworkComplaintSubtype [Enum] = [WirelessNetworkIssue|CoreNetworkIssue|CoverageIssue|2GNetworkSunset]
DeviceComplaintSubtype [Enum] = [HardwareFailure|SoftwareIssue]
ConfigurationComplaintSubtype [Enum] = [APNMisconfiguration|PolicyConflict|DPIWhitelistIssue]
BulkComplaintSubtype [Enum] = [MassiveOffline|GroupMalfunction]
SymptomType [Enum] = [NoConnection|SlowSpeed|HighLatency|WeakSignal|BulkOffline]
SeverityLevel [Enum] = [Critical|High|Medium|Low|Info]
CauseType [Enum] = [SignalCoverage|NetworkCongestion|ConfigError|DeviceFailure|PolicyRestriction|ExternalInterference]
ResolutionType [Enum] = [NetworkOptimization|ConfigChange|DeviceReplace|PolicyUpdate|ManualIntervention]

# Location Related
LocationType [Enum] = [Underground|Campus|Industrial|Rural|Urban|Highway|Indoor]
Direction [Enum] = [North|South|East|West|Northeast|Northwest|Southeast|Southwest]
DriftFrequency [Enum] = [Occasional|Frequent|Continuous|Random]
GeographicPattern [Enum] = [Nationwide|Regional|Local]

# Test Coordination Related
TimeRange [Enum] = [Anytime|Daytime|BeforeNight|Specific]
TestType [Enum] = [SignalTest|SignalingTrace|StressTest]
CooperationLevel [Enum] = [High|Medium|Low]
TeamType [Enum] = [WirelessOpt|CoreNetwork|CustomerService|FieldSupport|Platform]

# Data Analysis Related
Scale [Enum] = [Small(<100)|Medium(100-1000)|Large(1000-10000)|Massive(>10000)]
TriggerCause [Enum] = [ConfigChange|NetworkMaintenance|PolicyUpdate|SystemUpgrade|ExternalEvent]
AnomalyType [Enum] = [TrafficSpike|UnusualPattern|SecurityThreat|ServiceAbuse|ConfigError]
TimePatternType [Enum] = [PeakHourCongestion|OffPeakNormal|DailyRecurring|HolidayAdjustment]
DetectionMethodType [Enum] = [UnexpectedNetworkAttach|SignalAnomalyPattern|RuleBasedDetection]

# Others
ActionType [Enum] = [Assign|Escalate|Notify|Execute|Block|Allow]
RestrictionLevel [Enum] = [NoRestriction|Restricted|PartiallyRestricted|FullyRestricted]
LogicalOperator [Enum] = [AND|OR|NOT|XOR]
TimeUnit [Enum] = [seconds|minutes|hours|days|weeks|months]
DataUnit [Enum] = [MB|GB|TB|KB]
```
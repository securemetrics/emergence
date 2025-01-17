# EmergenceDB GRC Security Graph Model

## Overview
EmergenceDB is an open-source graph model for Governance, Risk, and Compliance (GRC) systems. It allows users to define, query, and manage relationships between key GRC entities such as requirements, controls, policies, risks, and evidence. This schema supports dynamic queries, integrations, and customization to fit diverse organizational needs.

---

## Core Entities and Properties

### Controls
- **Node Label:** `Control`
- **Key Properties:**
  - `ControlID`: Unique identifier (e.g., "AC-1").
  - `Name`: Name of the control.
  - `Description`: Control details.
  - `Implemented`: Boolean indicating if implemented.
  - `Framework`: Associated framework (e.g., NIST, PCI-DSS).

### Requirements
- **Node Label:** `Requirement`
- **Key Properties:**
  - `RequirementID`: Unique identifier (e.g., "NIST-800-53-AC-1").
  - `Name`: Short description.
  - `Description`: Requirement details.
  - `Framework`: Associated framework.
  - `NodePack`: Grouping mechanism for requirements.

### Policies
- **Node Label:** `Policy`
- **Key Properties:**
  - `PolicyID`: Unique identifier.
  - `Name`: Policy name.
  - `Description`: Overview.
  - `LastUpdated`: Last updated timestamp.

### Evidence
- **Node Label:** `Evidence`
- **Key Properties:**
  - `EvidenceID`: Unique identifier.
  - `ArtifactDescription`: Evidence details.
  - `Source`: Evidence origin.
  - `DateCollected`: Collection date.

### Risks
- **Node Label:** `Risk`
- **Key Properties:**
  - `RiskID`: Unique identifier.
  - `Name`: Risk name.
  - `Description`: Details.
  - `Severity`: Severity level.
  - `Likelihood`: Likelihood of occurrence.
  - `Impact`: Potential impact.

---

## Relationships

### Defined Relationships
- **`(:Control)-[:Satisfies]->(:Requirement)`**: Links a control to the requirement it satisfies.
- **`(:Evidence)-[:Supports]->(:Control)`**: Connects evidence to the control it supports.
- **`(:Control)-[:Mitigates]->(:Risk)`**: Indicates a control mitigates a specific risk.
- **`(:Policy)-[:Documents]->(:Control)`**: Links policies to the controls they document.
- **`(:Requirement)-[:RelatesTo]->(:Requirement)`**: Shows conceptual links between related requirements.

---

## Example Queries

### Fetch Controls for a Specific Requirement
```cypher
MATCH (control:Control)-[:Satisfies]->(requirement:Requirement {RequirementID: "PCI-DSS-1.1"})
RETURN control.Name, control.Description
```

### Trace Evidence for a Specific Control
```cypher
MATCH (evidence:Evidence)-[:Supports]->(control:Control {ControlID: "AC-1"})
RETURN evidence.EvidenceID, evidence.ArtifactDescription
```

### Identify Risks Mitigated by Implemented Controls
```cypher
MATCH (control:Control)-[:Mitigates]->(risk:Risk)
WHERE control.Implemented = true
RETURN risk.Name, risk.Description, risk.Severity
```

---

## Getting Started

### 1. Setting Up the Database
- Install a graph database such as [Neo4j](https://neo4j.com/).
- Create indices for `ControlID`, `RequirementID`, and `RiskID` to optimize query performance.

### 2. Populating the Graph
- Import your organization’s GRC data to create nodes and relationships.
- Automate data ingestion from compliance tools, vulnerability scanners, or other sources.

### 3. Customizing the Model
#### Adding Properties:
- Extend existing nodes with additional properties (e.g., `Owner` for `Control` or `Priority` for `Risk`).

#### Adding New Nodes:
- Example: **Audits**
  - `AuditID`, `AuditDate`, `Auditor`
  - Relationships:
    - `(:Audit)-[:Evaluates]->(:Control)`
    - `(:Audit)-[:ReportsOn]->(:Risk)`

#### Adding Relationships:
- Define custom relationships (e.g., `(:Risk)-[:Exacerbates]->(:Risk)` to model cascading risks).

### 4. Visualization
- Use tools like Neo4j Bloom or integrate with Power BI for interactive visualizations.

---

## Governance

1. **Maintenance**
   - Regularly audit nodes and relationships to ensure data accuracy.
   - Version control schema changes.

2. **Access Control**
   - Apply RBAC (Role-Based Access Control) to manage permissions.

3. **Documentation**
   - Maintain a registry of node types, properties, and relationships.

---

## Contact
For questions, feedback, or contributions, reach out to mitchell@securemetrics.io.

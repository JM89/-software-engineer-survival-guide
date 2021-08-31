# Designing Database Systems

## Checklist

* [ ] [Understand the access patterns](#access)
* [ ] [Choose between On-premises vs Cloud](#choose-serverless)
* [ ] [Define Volume of Data To Store](#volume)
* [ ] [Define Performance & High Availability (HA) Model](#ha)
* [ ] [Define Disaster Recovery (DR) Plan](#dr)
* [ ] [Define Upgrades/Patching Process](#patch) 
* [ ] [Define DB/Server Access Strategy](#access) 
* [ ] Define DB Monitoring System / Observability Model 
* [ ] Define Auditing System

## Understand the access patterns <a name="access" />

Define the Type of workload / business problem: 
- access patterns
- availability
- durability
- consistency (ATOMIC Transactions)
- latency
- scalability (RW TPS)
- partition tolerance…

Ensure that you keep a linear scalability.

## Choose between On-premises vs Cloud <a name="choose-serverless" />

Cloud allows more flexibility on installation/configuration/maintenance so you can take your decisions about a database technology for a given business problem without infrastructure impediment.

## Define Volume of Data To Store <a name="volume"/>

Questions:
* how quickly data grow? how data is archived?

Impact:
* Maximum Size of Disk and Vertical scaling

## Define Performance & High Availability <a name="ha"/>

Impacts:
* Technology chosen: fully-managed or hosted 
* Scaling Strategy
* Type of volumes: SSD optimised for IOPS...
* Failover Clustering Model (eg. SQL Server + Windows Failover Cluster)
* Overall cost: number of servers to maintain for the cluster
* Multi AZs/regions
* Read-Replicas

Considerations / Questions:
* What is the target TPS / IOPS / Throughtput during low/normal/high traffic / unusual/scheduled peaks? Is the monitoring in place already?
* Where do you access the data? (region and latencies)
* How do you access them? (only reads)

Cf. [HA & DR Technology Options](#ha-dr-tech-options)

## Define Disaster Recovery (DR) Plan <a name="dr"/>

* Technology chosen: fully-managed or hosted
* Overall cost
* Backup Strategy: frequency, backup tools, impact on db while backing-up
* Replication Strategy: async/sync, physical/logical, multi AZs/regions

Cf. [HA & DR Technology Options](#ha-dr-tech-options)

Metrics:
* Recovery Time Objective (RTO) *[Q: How long the outage is tolerated?]*
* Recovery Point Objective (RPO) *[Q: How much data can we lose? Is Point-In-Time restore required?]*
    - Logical/Software errors: eg. such as someone drop a table by mistakes, bug in application goofed up the data
    - Physical/Hardware errors: eg. disk corruption, network down...

## Define Upgrades/Patching Process  <a name="patch"/>

### Considerations 

* Choice Maintenance Windows (avoid peak hours)
* Have multiple nodes to failover or downtime?
* Automation when possible
* Patch Selection (Security Patches)
* Endpoint Security (ESET) for hosted servers (Antivirus)

## Define DB/Server Access Strategy <a name="access"/>

Depends on the type of Setup (Fully-Managed/Hosted), Technology Chosen (eg. SQL Server) & other options (HA Windows Failover Clustering)

Other considerations:
* company standards 
* national/regional laws
* auditing constrainsts

Who will need the access? 
* Infra during server setup (if hosted), patching (if not automated)
* DBA for product installation and configuration (if hosted), monitoring, patching (if not automated)
* Product Support for firefighting purpose

How the applications will connect? 
* Windows/SQL Server AG Listener: Additional DNS resolution?

Authentication Mechanism:
* Windows/SQL Server: AD or SQL Authentication (Service & User Accounts)

## Methodologies

### HA & DR Technology Options <a name="ha-dr-tech-options"/>

Example of comparison table that can be used to choose between one technology and another:

| Features | Approx. RPO | Approx. RTO |
| --------------- |:-------------:|:-----:|
| Multi-AZ for HA | None | Couple of minutes |
| Snapshot restore | Hours | Under an hour |
| Point-in-time restore | Several minutes | Between 1 and several hours |
| Read Replica promotion | Minutes | Under 5 minutes |
| Read replica promotion (cross-region) | Minutes | Under 5 minutes |


# High Availability and Disaster Recovery for HDInsight Kafka - Considerations

The following documentation covers Disaster Recovery for HDInsight-Kafka.

[High Availability](README.md#1--high-availability)<br>
[Disaster Recovery](DisasterRecovery.md#2--disaster-recovery)
<hr>

## 2.  Disaster Recovery

### 2.0.1. What is your SLA for Disaster Recovery?
The SLA for disaster recovery can be covered under two popular acronyms -
RTO - Recoverty Time Objective
The targeted duration of time and a service level within which a business process must be restored after a disaster (or disruption) in order to avoid unacceptable consequences associated with a break in business continuity.
RPO - Recovery Point Objective
A recovery point objective (RPO) is defined by business continuity planning. It is the maximum targeted period in which data might be lost from an IT service due to a major incident.


The RPO and RTO requirements (and needless to say, your budget) drive the DR architecture for your HDInsight solution.

### 2.0.2. What to replicate?
Topics and associated events.

### 2.0.3. Replication to DR - options

#### 2.0.3.1. Active - Hot standby with dual ingest and processing

![8-replicate-options-1](images/8-dr-options-1.png)
- Applications/integration processes write to Kafka on both clusters
- Both clusters run identical batch jobs and processes to consumer from Kafka
- Standby cluster is offline for reads by applications and end users
- Synchronization tasks need to be run to ensure data is in sync in destination store
- RPO => Low/None | RTO => Low/None | Cost => High
<br><br>
<hr>



#### 2.0.3.2. Active - Hot standby with dual ingest and processing
![8-replicate-options-2](images/8-dr-options-2.png)
- Applications write to Kafka on the active-primary ONLY
- Replication to DR Kafka cluster is incremental, batch, scheduled with Apache MirrorMaker
- Synchronization tasks need to be run to ensure data is in sync in destination store
- RPO => Medium | RTO => Medium | Cost => High
<br><br>
<hr>


#### 2.0.3.3. Active - Hot standby with dual ingest and processing
![8-replicate-options-3](images/8-dr-options-3.png)
- Applications/integration processes publish to/consume from nearest Kafka
- Both clusters run identical processing
- Synchronization tasks need to be run to ensure data is in sync in destination store
- RPO => Lowest/None | RTO => Lowest/None | Cost => High
<br><br>
<hr>

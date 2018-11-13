
# High Availability and Disaster Recovery for HDInsight Kafka - Considerations

HDInsight Kafka is Azure's Hortonworks distribution based managed Kafka as a service.  
The following documentation covers High Availability and Disaster Recovery for HDInsight-Kafka.

High Availability
Disaster Recovery
<hr>

## 1.  High Availability
To level-set, high-availability as referenced in this section has to do with *fault tolerance within the same datacenter*.<BR>
Acronyms used:<BR>
HA => High Availability<BR>
FT => Fault tolerance<BR>

### 1.0.1. HDInsight platform infrastructure - storage
HDInsight Kafka leverages Azure managed disks for storage.  At provision-time you can choose between premium and standard managed disks.<BR>

**Managed disks:**<BR>
By defaut - Azure storage service maintains 3 copies of each disk in the cluster, within the datacenter, across fault and update domains.  In the event of a failure, a replica is served uo seamlessly. <BR>

### 1.0.2. HDInsight platform infrastructure - compute
Azure VMs have an SLA, as do HDInsight master and worker nodes.  To maintain the SLA, the HDInsight service actively montors the health of the nodes and replaces failied nodes automatically.  For the highest fault tolerance HDInsight places nodes across fault and update domains intelligently.

### 1.0.3. Hadoop service component - master nodes
Although Kafka has a amsteless architecture, the management and monitoring services  in Hadoop like Ambari need to be configured HA.  For HA, HDInsight comes with two master nodes, in active and standby mode for maximizing FT.  The same are provisioned intelligently for FT across fault and update domains.


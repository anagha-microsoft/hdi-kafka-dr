
# HDInsight-Kafka: MirrorMaker for replication to DR - by example

This sample covers DR for HDInsight Kafka leveraging MirrorMaker.  In this example, we will provision HDInsight Kafka and dependencies in US East (primary) and US West (secondary).  The following are steps to deploy and configure replication to DR.<br>

## 1.  Primary datacenter - USEast - setup

### 1.0.1. Provision resource group in USEast
Create a resource group.<br>
![Create USE RG-1](images/1-create-rg.png)
<br><br>
![Create USE RG-2](images/1-create-rg-2.png)
<hr>

### 1.0.2. Provision a virtual network in the resource group
![Create vnet 1](images/2-create-vnet-1.png)
<br><br>
![Create vnet 2](images/2-create-vnet-2.png)
<br><br>
<hr>

### 1.0.3. Provision Kafka in the resource group and within the virtual network created
![Create kafka 1](images/3-create-kafka-1.png)
<br><br>
![Create kafka 2](images/3-create-kafka-2.png)
<br><br>
![Create kafka 3](images/3-create-kafka-3.png)
<br><br>
![Create kafka 4](images/3-create-kafka-4.png)
<br><br>
![Create kafka 5](images/3-create-kafka-5.png)
<br><br>
![Create kafka 6](images/3-create-kafka-6.png)
<br><br>
![Create kafka 7](images/3-create-kafka-7.png)
<br><br>

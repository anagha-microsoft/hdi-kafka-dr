
# HDInsight-Kafka: MirrorMaker for replication to DR - by example

This sample covers DR for HDInsight Kafka leveraging MirrorMaker.  In this example, we will provision HDInsight Kafka and dependencies in US East (primary) and US West (secondary).  The following are steps to deploy and configure replication to DR.<br>

## 1.  Primary datacenter - USEast - setup

### 1.0.1. Provision resource group in USEast
Create a resource group.<br>
![Create USE RG-1](images/1-create-rg.png)
<br><br>
<hr>

![Create USE RG-2](images/1-create-rg-2.png)
<hr>

### 1.0.2. Provision a virtual network in the resource group
![Create vnet 1](images/2-create-vnet-1.png)
<br><br>
<hr>

![Create vnet 2](images/2-create-vnet-2.png)
<br><br>
<hr>

### 1.0.3. Provision Kafka within the resource group and virtual network created
![Create kafka 1](images/3-create-kafka-1.png)
<br><br>
<hr>

![Create kafka 2](images/3-create-kafka-2.png)
<br><br>
<hr>

![Create kafka 3](images/3-create-kafka-3.png)
<br><br>
<hr>

![Create kafka 4](images/3-create-kafka-4.png)
<br><br>
<hr>

![Create kafka 5](images/3-create-kafka-5.png)
<br><br>
<hr>

![Create kafka 6](images/3-create-kafka-6.png)
<br><br>
<hr>

![Create kafka 7](images/3-create-kafka-7.png)
<br><br>
<hr>

## 2.  Secondary datacenter - USWest - setup
Repeat the steps above in US West datacenter-<br>
1.  Create resource group<br>
2.  Within the resource group, create a virtual network with a different IP address space that the primary<br>
3.  Provision Kafka in the resource group and virtual network created

## 3.  Configure Global Vnet Peering
We will now peer the virtual networks of the primary and secondary datacenters.
### 3.0.1. Peer the primary datacenter's vnet to the secondary datacenter's
![Create vnet-peer-1](images/4-conf-vnet-peering-1.png)
<br><br>
<hr>

![Create vnet-peer-2](images/4-conf-vnet-peering-2.png)
<br><br>
<hr>

![Create vnet-peer-3](images/4-conf-vnet-peering-3.png)
<br><br>
<hr>

![Create vnet-peer-4](images/4-conf-vnet-peering-4.png)
<br><br>
<hr>

![Create vnet-peer-5](images/4-conf-vnet-peering-5.png)
<br><br>
<hr>

![Create vnet-peer-6](images/4-conf-vnet-peering-6.png)
<br><br>
<hr>

### 3.0.2. Peer the secondary datacenter's vnet to the primary datacenter's

![Create vnet-peer-7](images/4-conf-vnet-peering-7.png)
<br><br>
<hr>

![Create vnet-peer-8](images/4-conf-vnet-peering-8.png)
<br><br>
<hr>

![Create vnet-peer-9](images/4-conf-vnet-peering-9.png)
<br><br>
<hr>



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

## 4.  Configure Kafka to broadcast private IP addresses and listen on all network interfaces 
### 4.0.1. Primary datacenter - configure IP advertising
By default, Zookeeper returns the domain name of the Kafka brokers to clients - not resolvable by entities outside the cluster. Follow the steps below to configure IP advertising.<br>

![Conf-ip-adv-1](images/5-conf-kafka-IP-1.png)
<br><br>
<hr>

![Conf-ip-adv-2](images/5-conf-kafka-IP-2.png)
<br><br>
<hr>

![Conf-ip-adv-3](images/5-conf-kafka-IP-3.png)
<br><br>
<hr>

![Conf-ip-adv-4](images/5-conf-kafka-IP-4.png)
<br><br>
<hr>

![Conf-ip-adv-5](images/5-conf-kafka-IP-5.png)
<br><br>
<hr>

![Conf-ip-adv-6](images/5-conf-kafka-IP-6.png)
<br><br>
<hr>
Paste this at the bottom of the kafka-env section:<br>
```
# Configure Kafka to advertise IP addresses instead of FQDN
IP_ADDRESS=$(hostname -i)
echo advertised.listeners=$IP_ADDRESS
sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
```
![Conf-ip-adv-7](images/5-conf-kafka-IP-7.png)
<br><br>
<hr>

![Conf-ip-adv-8](images/5-conf-kafka-IP-8.png)
<br><br>
<hr>

![Conf-ip-adv-9](images/5-conf-kafka-IP-9.png)
<br><br>
<hr>

### 4.0.2. Primary datacenter - configure listener
Configure Kafka to listen on all network interfaces-<br>

![Conf-listener-1](images/6-conf-kafka-listener-1.png)
<br><br>
<hr>

Replace the listener configuration with this:<br>
```
PLAINTEXT://0.0.0.0:9092 
```

![Conf-listener-2](images/6-conf-kafka-listener-2.png)
<br><br>
<hr>

![Conf-listener-3](images/6-conf-kafka-listener-3.png)
<br><br>
<hr>

![Conf-listener-4](images/6-conf-kafka-listener-4.png)
<br><br>
<hr>

### 4.0.3. Primary datacenter - restart Kafka
Restart Kafka-<br>

![Restart-1](images/7-restart-cluster-1.png)
<br><br>
<hr>

![Restart-2](images/7-restart-cluster-2.png)
<br><br>
<hr>

![Restart-3](images/7-restart-cluster-3.png)
<br><br>
<hr>

![Restart-4](images/7-restart-cluster-4.png)
<br><br>
<hr>


### 4.0.4. Make note of the broker IP addresses
![IPs](images/9-IPs.png)
<br><br>
<hr>

### 4.0.5. Secondary datacenter - repeat 4.0.[1-4]
1.  Configure Kafka for IP advertising
2.  Configure listener to listen on all network interfaces
3.  Restart Kafka
4.  Make a note of the broker IP addresses

## 5.  Setup in primary Kafka cluster
### 5.0.1. SSH into cluster

### 5.0.2. Create Kafka topic

### 5.0.3. Create consumer properties 

### 5.0.4. Create producer properties 

## 6.  Setup in secondary Kafka cluster
### 6.0.1. SSH into cluster

### 6.0.2. Create Kafka topic

### 6.0.3. Create consumer properties 

### 6.0.4. Create producer properties 

## 7.  Start MirrorMaker

## 8.  Test MirrorMaker
### 8.0.1. Launch console producer in primary Kafka cluster 

### 8.0.2. Launch console consumer in secondary Kafka cluster 

### 8.0.3. Validate replication by keying in some data in the producer in primary Kafka cluster 

### 8.0.3. Validate replication by viewing the console consumer in secondary Kafka cluster 




## Dashboard - Kafka
1. Download JSON file from [github release page](https://github.com/tonglo31/Summary/releases)
2. Go to domain:3000/dashboard/import
3. Upload JSON file

## Table of Content
1. [Kafka](#Installation)
2. [JMX Exporter](#configure-prometheus-for-linux-service)
3. [References](#references)


##  Overview
1. [Kafka_System_Metrics]
2. [Consumer]
3. [Producer]
4. [Process/Host]

## 1. Kafka System Metrics

### Active Controller
Total Number of active Controllers

``` bash
sum(kafka_cluster_partition_underreplicated)
```

**Unhealthy: ```If sum is not equal 1 is not normal ```**
##
### Underreplicated Partition
  The number of Partitions being copied.
``` bash
sum(kafka_cluster_partition_underreplicated)
```
**Unhealthy: ``` > 0 is unhealthy. However, if the Kafka cluster is reassigning partitions, this value will also be >0 ```**
##
### Offline Partition
Total Number of offline partition. (Partitions in this state is neither readable nor writable)
``` bash
sum(kafka_controller_kafkacontroller_offlinepartitionscount)
```
**Unhealthy: ```  The presence of >0 is abnormal. ```**

###

### ISR expands
Expansion rate of in-sync replicas

``` bash
sum(rate(kafka_server_replicamanager_isrexpands_total[5m]))
```
###
### ISR Shrink
Shrinkage rate of in-sync replicas

``` bash
sum(rate(kafka_server_replicamanager_isrshrinks_total[5m]))
```

### Average Request Time (Time Series)
Time the request waits for the follower Produce
``` bash
avg(kafka_network_requestmetrics_remotetimems)
```
Time the request waits for the response
``` bash
avg(kafka_network_requestmetrics_responsequeuetimems)
```

Time the request waits for the follower Produce
``` bash
avg(kafka_network_requestmetrics_remotetimems)
```

### Bytes out per topic (Top5)
Rank top5 Output Bytes
``` bash
topk(5, (sum by(topic) ((rate(kafka_server_brokertopicmetrics_bytesout_total[5m])) 
or (irate(kafka_server_brokertopicmetrics_bytesout_total[5m])))))
```

### Bytes In per topic (Top5)
Rank top5 Input Bytes
``` bash
topk(5, (sum by(topic) (rate(kafka_server_brokertopicmetrics_bytesin_total[5m]) 
or irate(kafka_server_brokertopicmetrics_bytesin_total[5m]))))
```

### Message In per topic (Top5)
Rank top5 Message received
``` bash
topk(5, sum by(topic)(rate(kafka_server_brokertopicmetrics_messagesin_total[5m])))
```

## 2. Consumer

### Average Request Latency
``` bash
avg(kafka_server_zookeeperclientmetrics_zookeeperrequestlatencyms)
```

### Average outgoing Byte Rate
``` bash
avg(kafka_server_zookeeperclientmetrics_zookeeperrequestlatencyms)
```

### Average request Rate
``` bash
avg(kafka_server_socket_server_metrics_request_rate)
```

### Average response Rate
``` bash
avg(rate(kafka_server_socket_server_metrics_response_rate[5m])) * 100
```

### Average IO waiting Time
```bash
avg(kafka_server_socket_server_metrics_io_wait_time_ns_avg)
```

### CPU Usage
CPU Usage in Kafka

calculation not sure
```bash
sum(rate(container_cpu_user_seconds_total{namespace=~".*kafka.*"}[30s])) * 100
```

## 3. Process/Host

### Opened Files

```bash
process_open_fds{container="kafka"}
```

### Opened Files Limited (Used %)
Percentage of Occupancy Limit
```bash
(process_open_fds{container="kafka"} / process_max_fds{container="kafka"}) * 100
```

### Log Size By Topic
Rank top 10 log size according to the topics (Only show >= 1kbs )
```bash
topk(10, sum by(topic) (kafka_log_log_size{container="kafka"}) >= 1024)
```

### Log Size (top10)
Rank top 10 log size
``` bash
topk(10, kafka_log_log_size{container="kafka"})
```
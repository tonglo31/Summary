
# Prometheus & Grafana 




## Installation

Install Prometheus

```bash
  tar -zxvf prometheus-2.36.0.linux-amd64.tar.gz
  sudo mv prometheus-*.linux-amd64 /opt/
```

Install Grafana
```bash
  tar -zxvf grafana-enterprise-8.5.4.linux-amd64.tar.gz
```

## Configure Prometheus for Linux Service

```bash
[Unit]
Description=Prometheus Server
Documentation=https://prometheus.iodocs/introduction/overview
After=network-online.target

[Service]
User=root
Restart=on-failure

ExecStart=/opt/prometheus \
    --config.file /opt/prometheus/prometheus.yml 

[Install]
WantedBy=default.target
```

## Enable Service
```bash
sudo systemctl reload-daemon
sudo systemctl start grafana-server
sudo systemctl start prometheus
sudo systemctl enable grafana-serveer
sudo systemctl enable prometheus
```

## Endpoint
``` bash
Prometheus::9090/
Grafana::3000
```



    
## Grafana - Overview
QPS: update every 5mins \
Buffer Pool Size

``` bash
MySQL uptime: mysql_global_status_uptime
QPS: rate(mysql_global_status_queries[$__interval]) or irate(mysql_global_status_queries[5m])
```

## Grafana - Network Traffic
Inbound: Received
Outbound: Sent
Display as Graph (5mins)
``` bash
rate(mysql_global_status_bytes_received[$__interval]) or 
irate(mysql_global_status_bytes_received[5m])
```

## Grafana - Network Usage
### Received
``` bash
increase(mysql_global_status_bytes_received[60m])
```
### Sent

``` bash
increase(mysql_global_status_bytes_sent[60m])
```

## Grafana - Client Thread Activity
### Peak Threads Connected
``` bash
max_over_time(mysql_global_status_threads_connected{instance="YOUR ADDRESS"}[$__interval]) or
max_over_time(mysql_global_status_threads_connected{instance="{YOUR ADDRESS"}[TIME])
```

### Peak Threads Running
``` bash
max_over_time(mysql_global_status_threads_running{instance="YOUR ADDRESS}[TIME]) or 
max_over_time(mysql_global_status_threads_running{instance="YOUR ADDRESS"}[$__interval])
```

## Grafana - Table open status
### Hit ratio

Hits / Hits + Missed
``` bash
(rate(mysql_global_status_table_open_cache_hits[TIME]) or 
    rate(mysql_global_status_table_open_cache_hits[$__interval])) /
    ((rate(mysql_global_status_table_open_cache_hits[TIME]) or 
    rate(mysql_global_status_table_open_cache_hits[$__interval])) +
    (rate(mysql_global_status_table_open_cache_misses[TIME]) or 
    rate(mysql_global_status_table_open_cache_misses[$__interval])))
```

### Hit rate
``` bash
rate(mysql_global_status_table_open_cache_hits[$__interval]) or 
    irate(mysql_global_status_table_open_cache_hits[5m])
```

## Grafana - MySQL Select Type
### Select_scan
The number of joins that did a full scan of the first table.

``` bash
rate(mysql_global_status_select_scan[$__interval]) or 
    irate(mysql_global_status_select_scan[TIME])
```

### Select Full Join
The number of joins that perform table scans because they do not use indexes. If this value is not 0, you should carefully check the indexes of your tables.

``` bash
rate(mysql_global_status_select_full_join[$__interval]) or 
    irate(mysql_global_status_select_full_join[TIME])
```

### Select Full Range Join
The number of joins that used a range search on a reference table.

``` bash
rate(mysql_global_status_select_full_range_join[$__interval]) or 
    irate(mysql_global_status_select_full_range_join[TIME])
```

### Mysql Questions
The number of statements executed by the server. This includes only statements sent to the server by clients and not statements executed within stored programs, unlike the Queries variable. This variable does not count ``` COM_PING ```, ``` COM_STATISTICS ```, ``` COM_STMT_PREPARE```, ```COM_STMT_CLOSE```, or ```COM_STMT_RESET``` commands.

### Questions
``` bash
rate(mysql_global_status_questions[TIME]) OR 
    rate(mysql_global_status_questions[$__interval])
```

## Grafana - MySQL commands

``` bash 
sum(rate(mysql_global_status_commands_total{command=~"select|insert"}[TIME])) without (command)
sum(rate(mysql_global_status_commands_total{command=~"delete|update"}[TIME])) without (command)
```
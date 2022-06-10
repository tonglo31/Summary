prometheus version 2.36.0
# Prometheus Alerts
- [Prometheus Alerts](#prometheus-alerts)  
    - [Modify Prometheus Config](#modify-prometheusconfig)  
    - [Create New Rules File](#create-new-rules-file)  
    - [Make Those Changes Work](#make-those-changes-work)  
    - [Result](#result)  
    - [Troubleshooting](#troubleshooting)  
        - [Failed to fetch](#failed-to-fetch)  

## Modify Prometheus Config
The location of config file: `/opt/prometheus/prometheus.yml`  
### Rules File Location Setup
change the path or insert current rules file path under "rule_files:" in `prometheus.yml`
![image](https://user-images.githubusercontent.com/71573064/172993221-c038ac46-575c-4022-bd0e-0717380ee591.png)  
  
If you always have rules file, just skip the **Create New Rules** File part.  
## Create New Rules File
Create new file from the path you set in last part if you do not have any rule file.
![image](https://user-images.githubusercontent.com/71573064/172993570-85485087-0af0-44eb-b315-19926bae055d.png)  
  
The format of rules file is found in https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/.  
![image](https://user-images.githubusercontent.com/71573064/172993522-310f5959-3470-499f-b2cf-6d89c9386576.png)
  
## Make Those Changes Work
Restart the prometheus server.
Here my own restart way (May have other good way?)
```
ps -ef
sudo kill 9 <prometheus PID>
sudo systemctl start prometheus
```
The process of prometheus in `ps -ef`
![image](https://user-images.githubusercontent.com/71573064/172994194-a6b5eef8-44c4-4cd8-843a-5283a97c232d.png)

## Result
You can view list of rules in `http://hk3cvdv02344:9090/rules` or `<domain name>:<port>/rules`  
![image](https://user-images.githubusercontent.com/71573064/172992947-97ce7683-329c-488b-b446-55cd842c6acc.png)  
It will work on Alerts page (`http://hk3cvdv02344:9090/alerts` or `<domain name>:<port>/alerts` ).  
![image](https://user-images.githubusercontent.com/71573064/172994447-7317995c-4e65-4c05-96d7-86543420798a.png)  
  
## Troubleshooting
### Failed to fetch
#### Situation  
Unexpected response status when fetching server time: Failed to fetch  
![image](https://user-images.githubusercontent.com/71573064/172994040-073e037a-4571-466c-9cd5-25d6e42e7dea.png)  
After that, the server shut down.  
![image](https://user-images.githubusercontent.com/71573064/172994269-90b76add-0d24-4307-8160-48b188bc764f.png)  
#### Solution
If your rules file have some error on file syntax or your query(such include some grafana varible), Prometheus cannot the file sucessfully.  
The error of the rules file should be fixed. Then restart the Prometheus server again to re-load those file.  

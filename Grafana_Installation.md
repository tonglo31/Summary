# Installation
## Installation for RPM-based Linux (Red Hat)
#### Reference: https://grafana.com/docs/grafana/latest/installation/rpm/
### Install manually with YUM
run in server
```
wget <rpm url>
sudo yum install <.rpm file name>
```
if face `unable to establish SSL connection` when using wget in the installation   
download .rpm file from https://grafana.com/grafana/download  
upload to the server and run `sudo yum install <.rpm file name>`.


### Install from YUM repository
view install guide in https://grafana.com/docs/grafana/latest/installation/rpm/.  
but the installation is blocked by `tcp connection reset by peer`.  
![image](https://user-images.githubusercontent.com/71573064/172516551-b1d9cd05-193f-4748-9584-99639381d91a.png)

## Start Server
start the service and verify that the service has started
```
sudo systemctl daemon-reload
sudo systemctl start grafana-server
sudo systemctl status grafana-server
```
Configure the Grafana server to start at boot
```
sudo systemctl enable grafana-server
```

Some special requirment such as **Serving Grafana on a port < 1024, Serving Grafana behind a proxy** can view in the offical guide.

next guide is `Grafana_Started.md`
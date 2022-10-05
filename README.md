# Ansible Playbook: rpi_install_node_exporter
## Part of my Raspberry Pi cluster project

# Purpose

This playbook installs the node exporter service for publishing metrics that can be scraped by Prometheus. It can also update the configuration of an existing Prometheus host.<br>
After installation the node-exporter service will be enabled and started. To view its status (or disable/stop):
```shell
systemctl status node-exporter.service
```
The metrics by default are published to port 9100 and can be viewed using:
```shell
curl http://localhost:9100/metrics
```

## Requirements
```yaml
collections:
  - community.general
  - community.docker
```
## Role Variables

Variables for each role are listed below, along with default values (see ```defaults/main.yml```)
```yaml
# install_node_exporter role
download_url: https://github.com/prometheus/node_exporter/releases/download/v1.4.0/node_exporter-1.4.0.linux-arm64.tar.gz
install_path: /opt/node-exporter # default directory where node exporter binary will be installed
web_port: 9100 # default web.listen-address port can be changed when theres a conflict

# prometheus_config role
prometheus_host: 192.168.0.1
prometheus_config_dir: /etc/prometheus # default location of prometheus.yml 
prometheus_job_name: Raspberry Pi Cluster # enter your desired job name
prometheus_scrape_interval: 5s # prometheus global default is usually 15s
```
## Dependencies

None

## Example Playbook
```yaml
---
- name: install node_exporter on rpi cluster nodes
  hosts: all
  become: true
  gather_facts: true  
  vars:
    inc_prometheus_config: true # prometheus will be configured if true    
  tasks:
    - name: install node exporter
      include_role:
        name: install_node_exporter    
    - name: configure prometheus
      include_role:
        name: prometheus_config
      when: inc_prometheus_config|bool
```

## License

[MIT](LICENCE)

## Author Information

This role was created in 2022 by [Lee Woodhouse](https://www.leewoodhouse.com/)

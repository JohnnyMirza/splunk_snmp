# splunk_snmp

--version 1: f5 and foritnet support
--v 1.1.: Splunk App for Infrastructure version 2.1.0 uses the entity_classes.conf file

**SNMP Network Monitoring from Splunk.**

Pre-Requisites: Splunk App for Infrastructure


Steps:
- Install net-snmp on Splunk HF
  - dnf install net-snmp
  - systemctl enable snmpd
  - systemctl start snmpd
  
- Install telegraf on a Splunk HF
  - sudo yum -y update
   ```
   cat <<EOF | sudo tee /etc/yum.repos.d/influxdb.repo
   [influxdb]
   name = InfluxDB Repository - RHEL 
   baseurl = https://repos.influxdata.com/rhel/7/x86_64/stable/
   enabled = 1
   gpgcheck = 1
   gpgkey = https://repos.influxdata.com/influxdb.key
   EO
   ```
   - sudo yum -y install telegraf
   - sudo systemctl enable --now telegraf
  
- Copy the telegraf conf files from GiT folder to the /etc/telegraf/telegraf.d folder on the HF
- Replace the /opt/splunk/etc/apps/splunk_app_infrastructure/default/collectors.conf on the HF to the one from git
copy MIBS to /usr/share/snmp/mibs folder on the HF
***Note: for Splunk App for Infrastructure version > 2.1.0, use the entity_classes file instead of the collectors.conf file***


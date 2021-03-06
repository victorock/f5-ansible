Workflow
---------
- Take input from a variable files and based on input configure the BIG-IP
  - Onboarding - yes/no
  - Standalone - yes/no - ONLY standalone supported right now, so ONLY option yes
  - What type of application - http/https
  - IP address's
  
- Call appropraite playbooks based on input

Example Variable File
---------------------
```
## Onboarding BIG-IP ##
onboarding: "yes" #Options: yes/no. 
standalone: "yes"
banner_text: "--------Welcome to demo BIGIP----------"

bigip1_hostname: 'bigip1.local'
bigip2_hostname: 'bigip2.local'

ntp_servers:
 - '172.27.1.1'
 - '172.27.1.2'

dns_servers:
 - '8.8.8.8'
 - '4.4.4.4'

ip_version: 4

#What service do you want to deploy on the BIG-IP
service: "http_service" #Options: http_service/https_service 

# BIG-IP related inforamtion
consumer_vlan_name: "External_VLAN"
consumer_vlan: "900"
consumer_interface: "1.1"

provider_vlan_name: "Internal_VLAN"
provider_vlan: "901"
provider_interface: "1.1"

bigip1_ip: 10.192.74.53
bigip1_username: "admin"
bigip1_password: "admin"

#SELF-IP and floating IP information
bigip1_selfip_information:
- name: 'External-SelfIP'
  address: '10.168.68.10'
  netmask: '255.255.255.0'
  vlan: "External_VLAN"
- name: 'Internal-SelfIP'
  address: '192.168.68.10'
  netmask: '255.255.255.0'
  vlan: 'Internal_VLAN'

#VIP information
vip_name: "http_vs"
vip_port: "80"
vip_ip: "10.168.68.105"

#Pool memeber information
pool_members:
- port: "80"
  host: "192.168.68.140"
- port: "80"
  host: "192.168.68.141"

#Specify the iRules you want to attach to the Virtual Server
rule:
- irule1
- irule2
- irule4

#Do you want to upload the irules to the BIG-IP?
upload_irule: "yes"

#Specify the profiles you want to attach to the Virtual Server
#Profile must already exist on the BIG-IP
profiles:
- http
- httpcompression

```

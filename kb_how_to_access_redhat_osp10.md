# How to access Redhat Openstack 10 environment
Assumed that your pc is located in company's internal network,now you can access the environment by web or cli.
but when you are at home and want to access the environment by VPN , it seems that it is impossible, maybe you can help me to solve it.

## web portal 

### step1-add a static route

in windows:
route add -p 192.168.101.0 mask 255.255.255.0 172.30.1.120 

in linux:  
1)ip r a  192.168.101.0/24 via 172.30.1.120   
2)fix above route rule in file for working after next rebooting,you can refer 
[How to add a stacic route in rhel linux] (https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/sec-Configuring_Static_Routes_in_ifcfg_files.html,"rhel")  


so ping 192.168.101.1 or 192.168.101.14 is ok. 

### step2 - access URL
open browser like firefox , go the following link:
<http://192.168.101.14>

user:admin  
password:genomics  

this is a screenshot:
![](http://i1.piimg.com/4851/5c48c647536f3094.png)


## cli 

ssh genomics@172.30.1.120
password:genomics 

```sh

[root@centos7 ~]# ip r
default via 172.30.0.1 dev eno49  proto static  metric 100 
172.30.0.1 dev eno49  proto static  scope link  metric 100 
172.30.1.0/24 dev eno49  proto kernel  scope link  src 172.30.1.120  metric 100 
192.168.100.0/24 dev virbr1  proto kernel  scope link  src 192.168.100.1 
192.168.101.0/24 dev virbr2  proto kernel  scope link  src 192.168.101.1 
192.168.102.0/24 dev virbr3  proto kernel  scope link  src 192.168.102.1 
192.168.103.0/24 dev virbr4  proto kernel  scope link  src 192.168.103.1 
192.168.104.0/24 dev virbr5  proto kernel  scope link  src 192.168.104.1 
192.168.105.0/24 dev virbr6  proto kernel  scope link  src 192.168.105.1 
192.168.106.0/24 dev virbr7  proto kernel  scope link  src 192.168.106.1 
192.168.122.0/24 dev virbr0  proto kernel  scope link  src 192.168.122.1 


[genomics@centos7 ~]$ ls
overcloudrc
[genomics@centos7 ~]$ source overcloudrc 
[genomics@centos7 ~]$ openstack endpoint list
+----------------------------------+-----------+--------------+----------------+
| ID                               | Region    | Service Name | Service Type   |
+----------------------------------+-----------+--------------+----------------+
| 1f51478dd366444882588aa5b0e6823e | regionOne | cinder       | volume         |
| 17e19dd2085c4bbf9d5fe89338ff602d | regionOne | heat         | orchestration  |
| 15625928225a46539862fc6e1a76adc6 | regionOne | heat-cfn     | cloudformation |
| d2a9425cf3e5475fbe1e78728f7d485d | regionOne | aodh         | alarming       |
| 15301f866aa4413f804763dcc26cfe40 | regionOne | ceilometer   | metering       |
| b1759595900a4ceca329073324fdf691 | regionOne | glance       | image          |
| 689ffa161aab4805b53e7691e5c69e69 | regionOne | cinderv3     | volumev3       |
| 97d83dec6cb844a6b2a2e8cb0f24c799 | regionOne | nova         | compute        |
| ca4ae4d112a54a90a3ebd1e18c9b1f8d | regionOne | swift        | object-store   |
| b4621bda55894d6fbaec058f8985d266 | regionOne | keystone     | identity       |
| df947fff019942d383d423a07a654323 | regionOne | gnocchi      | metric         |
| 7682f543d2b74ad0890670c09f048d33 | regionOne | cinderv2     | volumev2       |
| 69fc0284891446cda001d27a9a35560d | regionOne | neutron      | network        |
+----------------------------------+-----------+--------------+----------------+
[genomics@centos7 ~]$ openstack server list 

[genomics@centos7 ~]$ 


```

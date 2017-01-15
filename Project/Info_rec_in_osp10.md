# one controller , one compute 

2017-01-14 03:30:17Z [overcloud.AllNodesDeploySteps.ControllerPostPuppet.ControllerPostPuppetMaintenanceModeConfig]: CREATE_IN_PROGRESS  state changed
2017-01-14 03:30:17Z [overcloud.AllNodesDeploySteps.ControllerPostPuppet.ControllerPostPuppetMaintenanceModeConfig]: CREATE_COMPLETE  state changed
2017-01-14 03:30:17Z [overcloud.AllNodesDeploySteps.ControllerPostPuppet.ControllerPostPuppetMaintenanceModeDeployment]: CREATE_IN_PROGRESS  state changed
2017-01-14 03:31:23Z [overcloud.AllNodesDeploySteps.ControllerPostPuppet.ControllerPostPuppetMaintenanceModeDeployment]: CREATE_COMPLETE  state changed
2017-01-14 03:31:23Z [overcloud.AllNodesDeploySteps.ControllerPostPuppet.ControllerPostPuppetRestart]: CREATE_IN_PROGRESS  state changed
2017-01-14 03:32:30Z [overcloud.AllNodesDeploySteps.ControllerPostPuppet.ControllerPostPuppetRestart]: CREATE_COMPLETE  state changed
2017-01-14 03:32:30Z [overcloud.AllNodesDeploySteps.ControllerPostPuppet]: CREATE_COMPLETE  Stack CREATE completed successfully
2017-01-14 03:32:30Z [overcloud.AllNodesDeploySteps.ControllerPostPuppet]: CREATE_COMPLETE  state changed
2017-01-14 03:32:30Z [overcloud.AllNodesDeploySteps]: CREATE_COMPLETE  Stack CREATE completed successfully
2017-01-14 03:32:31Z [overcloud.AllNodesDeploySteps]: CREATE_COMPLETE  state changed
2017-01-14 03:32:31Z [overcloud]: CREATE_COMPLETE  Stack CREATE completed successfully

 Stack overcloud CREATE_COMPLETE 

Started Mistral Workflow. Execution ID: 866bef4a-7b75-4db2-a904-4e4950b5256f
/home/stack/.ssh/known_hosts updated.
Original contents retained as /home/stack/.ssh/known_hosts.old
Overcloud Endpoint: http://192.168.101.13:5000/v2.0
Overcloud Deployed

real	35m41.058s
user	0m5.593s
sys	0m0.576s
[stack@director ~]$ heat stack-list
WARNING (shell) "heat stack-list" is deprecated, please use "openstack stack list" instead
+--------------------------------------+------------+-----------------+----------------------+--------------+
| id                                   | stack_name | stack_status    | creation_time        | updated_time |
+--------------------------------------+------------+-----------------+----------------------+--------------+
| 01f5c799-f65e-403e-a740-c84d949acb35 | overcloud  | CREATE_COMPLETE | 2017-01-14T02:58:57Z | None         |
+--------------------------------------+------------+-----------------+----------------------+--------------+
[stack@director ~]$ 
[stack@director ~]$ 



[root@overcloud-controller-0 my.cnf.d]# pcs status 
Cluster name: tripleo_cluster
Stack: corosync
Current DC: overcloud-controller-0 (version 1.1.15-11.el7_3.2-e174ec8) - partition with quorum
Last updated: Sat Jan 14 03:39:26 2017		Last change: Sat Jan 14 03:31:21 2017 by root via cibadmin on overcloud-controller-0

1 node and 11 resources configured

Online: [ overcloud-controller-0 ]

Full list of resources:

 ip-192.168.105.15	(ocf::heartbeat:IPaddr2):	Started overcloud-controller-0
 ip-192.168.102.14	(ocf::heartbeat:IPaddr2):	Started overcloud-controller-0
 ip-192.168.102.16	(ocf::heartbeat:IPaddr2):	Started overcloud-controller-0
 Clone Set: haproxy-clone [haproxy]
     Started: [ overcloud-controller-0 ]
 Master/Slave Set: galera-master [galera]
     Masters: [ overcloud-controller-0 ]
 ip-192.168.103.53	(ocf::heartbeat:IPaddr2):	Started overcloud-controller-0
 Clone Set: rabbitmq-clone [rabbitmq]
     Started: [ overcloud-controller-0 ]
 Master/Slave Set: redis-master [redis]
     Masters: [ overcloud-controller-0 ]
 ip-192.168.104.15	(ocf::heartbeat:IPaddr2):	Started overcloud-controller-0
 ip-192.168.101.13	(ocf::heartbeat:IPaddr2):	Started overcloud-controller-0
 openstack-cinder-volume	(systemd:openstack-cinder-volume):	Started overcloud-controller-0

Daemon Status:
  corosync: active/enabled
  pacemaker: active/enabled
  pcsd: active/enabled
[root@overcloud-controller-0 my.cnf.d]# 
[root@overcloud-controller-0 my.cnf.d]# 
[root@overcloud-controller-0 my.cnf.d]# ovs-vsctl show 
92e77772-90f4-4ab5-9725-988f8e6aa87c
    Manager "ptcp:6640:127.0.0.1"
        is_connected: true
    Bridge br-ex
        Controller "tcp:127.0.0.1:6633"
            is_connected: true
        fail_mode: secure
        Port phy-br-ex
            Interface phy-br-ex
                type: patch
                options: {peer=int-br-ex}
        Port br-ex
            Interface br-ex
                type: internal
        Port "eth1"
            Interface "eth1"
    Bridge br-int
        Controller "tcp:127.0.0.1:6633"
            is_connected: true
        fail_mode: secure
        Port patch-tun
            Interface patch-tun
                type: patch
                options: {peer=patch-int}
        Port int-br-ex
            Interface int-br-ex
                type: patch
                options: {peer=phy-br-ex}
        Port br-int
            Interface br-int
                type: internal
    Bridge br-tun
        Controller "tcp:127.0.0.1:6633"
            is_connected: true
        fail_mode: secure
        Port patch-int
            Interface patch-int
                type: patch
                options: {peer=patch-tun}
        Port br-tun
            Interface br-tun
                type: internal
        Port "vxlan-c0a86a0f"
            Interface "vxlan-c0a86a0f"
                type: vxlan
                options: {df_default="true", in_key=flow, local_ip="192.168.106.11", out_key=flow, remote_ip="192.168.106.15"}
    ovs_version: "2.5.0"
[root@overcloud-controller-0 my.cnf.d]# 




[root@overcloud-compute-0 ~]# ip r
default via 192.168.103.1 dev eth0 
169.254.169.254 via 192.168.103.10 dev eth0 
192.168.102.0/24 dev eth1  proto kernel  scope link  src 192.168.102.10 
192.168.103.0/24 dev eth0  proto kernel  scope link  src 192.168.103.62 
192.168.104.0/24 dev eth3  proto kernel  scope link  src 192.168.104.10 
192.168.106.0/24 dev eth2  proto kernel  scope link  src 192.168.106.15 
[root@overcloud-compute-0 ~]# ovs-vsctl show 
99538fd8-dc2b-4be9-aae7-b90a8604d185
    Manager "ptcp:6640:127.0.0.1"
        is_connected: true
    Bridge br-ex
        Controller "tcp:127.0.0.1:6633"
            is_connected: true
        fail_mode: secure
        Port br-ex
            Interface br-ex
                type: internal
        Port phy-br-ex
            Interface phy-br-ex
                type: patch
                options: {peer=int-br-ex}
    Bridge br-int
        Controller "tcp:127.0.0.1:6633"
            is_connected: true
        fail_mode: secure
        Port patch-tun
            Interface patch-tun
                type: patch
                options: {peer=patch-int}
        Port br-int
            Interface br-int
                type: internal
        Port int-br-ex
            Interface int-br-ex
                type: patch
                options: {peer=phy-br-ex}
    Bridge br-tun
        Controller "tcp:127.0.0.1:6633"
            is_connected: true
        fail_mode: secure
        Port patch-int
            Interface patch-int
                type: patch
                options: {peer=patch-tun}
        Port "vxlan-c0a86a0b"
            Interface "vxlan-c0a86a0b"
                type: vxlan
                options: {df_default="true", in_key=flow, local_ip="192.168.106.15", out_key=flow, remote_ip="192.168.106.11"}
        Port br-tun
            Interface br-tun
                type: internal
    ovs_version: "2.5.0"
[root@overcloud-compute-0 ~]# 
















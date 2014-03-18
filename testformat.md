crmsh pcs cheatsheet
--------------------

Function | crmsh | pcs | notes
--- | --- | --- | ---
list cib | `crm configure show` | |
list cib as XML | `crm configure show xml` | pcs cluster cib |
show status | `crm status` <br> `crm_mon -1` | `pcs status` | `crm_mon` is not a crmsh feature but a pacemaker one
control node standby | `crm node standby <node>` <br> `crm node online <node>` | `pcs cluster standby <node>` <br> `pcs cluster unstandby <node>` | crm has the ability to set the status on reboot or forever.  <br> pcs can apply the change to all the nodes. 
set cluster properties | `crm configure property stonith-enabled=false` | `pcs property set stonith-enabled=false` |
list RA classes | `crm ra classes` | `pcs resource standards` |
list Resource Agents | `crm ra list ocf` <br> `crm ra list lsb` <br> `crm ra list service` <br> `crm ra list stonith` <br> `list RA info` | `pcs resource agents ocf` <br> `pcs resource agents lsb` <br> `pcs resource agents service` <br> `pcs resource agents stonith` <br> `pcs resource agents` | 
list RA info | `crm ra meta IPaddr2` | `pcs resource agent IPaddr2` | Takes last argument from the lists above
create resources | `crm configure primitive ClusterIP ocf:heartbeat:IPaddr2 \ ` <br> `params ip=192.168.122.120 cidr_netmask=32 \ ` <br> `op monitor interval=30s` | `pcs resource create ClusterIP IPaddr2 ip=192.168.0.120 cidr_netmask=32` | The standard and provider (ie: ocf:heartbeat) are determined automatically since IPaddr2 is unique. The monitor operation is automatically created based on the agent's metadata. 
show resources | `crm resource show` | `pcs resource show` | A last argument (resource name) can be supplied. crm also shows fencing resources. 
show fencing resources | `crm resource show` | `pcs stonith show` |
modify resources | `crm resource param ClusterIP set clusterip_hash=sourceip` | `pcs resource update ClusterIP clusterip_hash=sourceip` `pcs resource update ClusterIP ip=192.168.0.98 nic=` |
control resources | `crm resource start <resource>` <br> `crm resource stop <resource>` | `pcs resource enable <resource>` <br> `pcs resource disable <resource>` |
delete resources | `crm resource delete <resource>` | `pcs resource delete <resource>` |
show resource defaults | `crm configure show type:rsc_defaults` <br> `crm configure show type:op_defaults` | `pcs resource defaults` <br> `pcs resource op defaults` | git table erroneously list rsc for pcs 
set resource op defaults | `crm configure op_defaults timeout=240s` | `pcs resource op defaults timeout=240s` |
list constraints | none - closest is `crm configure show` | `pcs constraint` | Apart from groups, crmsh does not interpret constraints and therefore knows nothing about resource dependencies.
set colocation | `crm configure colocation <name_id> INFINITY: <resource1> <resource2>` | `pcs constraint colocation add <resource2> with <resource1> INFINITY` |     

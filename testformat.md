crmsh pcs cheatsheet
--------------------

Function | crmsh | pcs | notes
--- | --- | --- | ---
list cib | `crm configure show` | |
list cib as XML | `crm configure show xml` | pcs cluster cib |
show status | `crm status` <br> `crm_mon -1` | `pcs status` | `crm_mon` is not a crmsh feature but a pacemaker one
control node standby | `crm node standby <node>` <br> `crm node online <node>` | `pcs cluster standby <node>` <br> `pcs cluster unstandby <node>` | crm has the ability to set the status on reboot or forever.
 <br> pcs can apply the change to all the nodes. 

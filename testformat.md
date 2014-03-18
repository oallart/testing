crmsh pcs cheatsheet
--------------------

Function | crmsh | pcs | notes
--- | --- | --- | ---
list cib | `crm configure show` | |
list cib as XML | `crm configure show xml` | pcs cluster cib |
show status | `crm status`
`crm_mon -1` | `pcs status` |

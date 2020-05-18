# Sync Timeout

By default, a Sync transaction is not limited by time. However, you can limit the sync time of an LUI to avoid bottlenecks and stuck instances.\
If a timeout is set and the sync exceeds the predefined timeout, Fabric rollbacks the changes and throws the following exception: Timeout occurred.\
A sync timeout can be defined either per session or at an LU Schema level.

![image](https://k2vacademy.s3.amazonaws.com/Fabric/6_Sync/6_7_sync_timeout_levels.png)



### How do I Set the Sync Timeout on an LU Schema?
The Sync property in the LU Schema Properties tab has the following setting:
* Timeout (sec) – Set a timeout in seconds for syncing LUI.\
By default, this field = 0 whereby no timeout is defined for the LU schema, however it can be edited so that the Sync Timeout is defined in seconds.

[**Click for more information about Sync Properties.**](https://github.com/k2view-academy/K2View-Academy/wiki/Sync-Methods)

### How do I Set The Sync Timeout on a Session Level?
Use the following command to override the Timeout set for the LU Schema:
* set sync_timeout\
Syntax: 
* set sync_timeout=<sync_timeout_sec>
* set sync_timeout='' - to set timeout back to LU default value\
For example:
* set sync_timeout=60;
* set sync_timeout='';

When Sync Timeout is defined on a session level, it applies to each sync on the LUI, regardless of the Timeout value in the LU Schema.


[![Previous](https://k2vacademy.s3.amazonaws.com/General/Previous.png)](https://github.com/k2view-academy/K2View-Academy/wiki/Sync-Method--Levels)[<img align="right" width="60" height="54" src="https://k2vacademy.s3.amazonaws.com/General/Next.png">](https://github.com/k2view-academy/K2View-Academy/wiki/Skip-Sync)








# Use Resource Governor to Limit CPU Usage by Backup Compression

By default, backing up using compression significantly increases CPU usage, and the additional CPU consumed by the compression process can adversely impact concurrent operations. Therefore, you might want to create a low-priority compressed backup in a session whose CPU usage is limited by Resource Governor when CPU contention occurs. This topic presents a scenario that classifies the sessions of a particular SQL Server user by mapping them to a Resource Governor workload group that limits CPU usage in such cases.


These Notes go through the following scenarios
1. Setting up a login and user for low-priority operations
2. Configuring Resource Governor to limit CPU usage
3. Verifying the classification of the current session (Transact-SQL)
4. Compressing Backups using a session with limited CPU

## Setting up a login and user for low-Priority operations

The scenario in this topic requires a low-priority SQL Server login and user. The user name will be used to classify sessions running in the login and route them to a resource governor workload group that limits CPU usage. 

The following procedure describes the steps for setting up a login and user for this purpose, followed by a Transact-SQL e.g
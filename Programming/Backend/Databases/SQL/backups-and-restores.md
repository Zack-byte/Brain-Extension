# SQL Server Backups and Restores
The SQL Server backup and restore component provides an essential safeguard for protecting critical data stored in your SQL Server databases. To minimize the risk of catastrophic data loss, you need to back up your databases to preserve modifications to your data on a regular basis. A wel-planned backup and restore strategy helps protect databses against data loss caused by a variety of failures.

In addition to local storage for storing the backups, SQL Server also supports backup to and restore from the `Azure Blob Storage Service`. For database files stored using the Microsoft Azure Blob storage service, SQL Server 2016 provides the option to use Azure snapshots for nearly instantaneous backups and faster restores. 

Azure also offers an enterprise-class backup solution for SQL Server running in Azure VMs. A fully-managed backup solution, it supports Always On availability groups, long-term retention, point-in-time recovery, and central management and monitoring.

## Why back up?
Backing up your SQL Serv er databases, running test restores procedures on your backups, and storing copies of backups in a safe, off-site location protects you from potentially catastrophic data loss. **Backing up is the only way to protect your data**

With valid backups of a databse, you can recover your data form many failures such as:
- Media failures
- User errors (e.g dropping a table)
- Hardware failures (e.g a damaged disk drive or permanent loss of a server)
- Natural disasters. By using SQL Server Backup to Azure Blob storage service, you can create an off-site backup in a different region. to use in the event of a disaster.

Additionally, backups of a database are useful for routine administrative purposes, such as copying a databse from one server to another, setting up Always On AG's or databse mirroring, and archiving. 

## Glossary of backup Terms
- `back up` [verb]: the process of creating a `backup` [noun] by copying data records from a SQL Server database, or log records from its transaction log.
- `backup` [noun]: A copy of data that can be used to restore and recover the data after failure. Backups of a database also can be used to restore a copy of the DB to a new location.
- `backup device`: A disk or tape device to which SQL Server backups are written and from which they can be restored. SQL Server backups can also be written to an Azure Blob storage service, and `URL` format is used to specify the destination and the name of the backup file.
- `backup media`: One or more tapes or disk files to which one or more backups have been written.
- `data backup`: A backup of data in a complete databse (a database backup), a partial database(a partial backup), or a set of data files or filegroups (a file backup).
- `database backup`: A backup of a databse. Full databse backups represent the whole databse at the time the backup finished. Differential databse backups contain only changes made to the database since its most recent full databse backup.
- `differential backup`: A data backup that is based on the latest full backup of a complete or partial DB or a set of data files or filegroups (the differential base) and that contains only the data that has changed since that base.
- `full backup`: A data backup that contains all the data in a specific DB or set of filegroups or files, and also enough log to allow for recovering that data.
- `log backup`: A backup of transaction logs that includes all log records that were not backed up in a previous log backup. (full recovery mode)
- `recover`: To return a datbase to a stable and consistent state.
- `recovery model`: A DB property that controls transaction log maintenance on a DB. Three recovery models exist: simple, full, and bulk-logged. The recovery model of DB determines its backup and restore requirements.
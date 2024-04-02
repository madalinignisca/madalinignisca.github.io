---
layout: post
title:  "Postgresql data directory structure"
date:   2024-04-02 19:00:00
categories: [postgresql]
---

If you can connect using psql, then you can use this command:
```
postgres=# SHOW data_directory;
data_directory
-----------------------
/opt/postgres/data/
```

| directory | description |
|-----------|-------------|
| base | This is the main table storage. Beneath this directory, each database has its own directory, within which the files for each database table or index are located |
| global | Tables that are shared across all databases, including the list of databases. |
| pg_commit_ts | Transaction commit timestamp data |
| pg_dynshmem | Dynamic shared memory information |
| pg_logical | Logical decoding status data |
| pg_multixact | Files used for shared row-level locks |
| pg_notify | LISTEN/NOTIFY status files |
| pg_replslot | Information about replication slots |
| pg_serial | Information on commited serializable transaction |
| pg_snapshots | Exported snapshot files |
| pg_stat | Permanent statistics data |
| pg_stat_tmp | Transient statistics data |
| pg_subtrans | Subtransaction status data |
| pg_tblspc | Symbolic links to tablespace directories |
| pg_twophase | State files for prepared transactions (a.k.a. two-phase commit) |
| pg_wal | Transaction log or Write-Ahead Log |
| pg_xact | Transaction status files |

None of the aforementioned directories contain user-modifiable files, nor should any of the files be manually deleted to save space, or for any other reason. Don’t touch it, because you’ll break it, and you may not be able to fix it! It’s not even sensible to copy files in these directories without carefully following the procedures described in Chapter 11, Backup and Recovery. Keep off the grass!

_Excerpt From
PostgreSQL 16 Administration Cookbook
Gianni Ciolli, Boriss Mejías, Jimmy Angelakos,  Vibhor Kumar, Simon Riggs
This material may be protected by copyright._

---
date: 2016-10-01 15:17:36 
layout: post
title: "6 reasons to choose PostgreSQL 9.6"
description: ""
category: english
tags: [PostgreSQL,parallelism]
---

PostgreSQL 9.6 was released a few days ago and it's another huge milestone for the PostgreSQL community ! 
The release notes are way too long, so I've decided to pick up 6 big improvements that may change the way 
you will use PostgreSQL.

<!-- More -->

  ![](  https://c1.staticflickr.com/5/4002/4280292398_c5ca8c7176_z.jpg  )

1. **Parallelism** is probably the main attraction of this version : a long-awaited feature that will open the door to many new usecases. In a nutshell, in the previous versions, Postgres could only use one single core per query, even if other processors were available. The limitation is now over and many different forms of queries can use parallelism : sequential scans, joins and aggregates can now be run in parallel on multiple core, if you want to.

2. **Better Lock Monitoring** : the pg_stat_activity view now provides much better wait information. When a process is waiting for a lock, you'll see the type of lock and details of the wait event that's putting your query on hold. Also with the pg_blocking_pids() function you'll know what's blocking a given server process. Such monitoring will let DBA know how long backend waited for particular event and therefore identify bottlenecks.

3. **Multiple Synced Standbys** : Previously synchronous replication was possible for at most one node. PopstgreSQL 9.6 now supports multiple synchronous standby servers. It enables users to consider one or more nodes as synchronous and increase the level of transaction durability by ensuring that transaction commits wait for replies from all of those nodes.

4. **Preventing bloat** : Until now a long-running report or cursor displaying query results could block cleanup of dead rows, bloating all volatile tables in the database, causing performance problems and excessive use of storage space. A new parameter called old_snapshot_threshold allows the cluster to cleanup a dead rows when the transaction which modified it has completed and all snapshots which can still see it have reached a certain age…

5. **PostgreSQL FDW improvements** : With more than 80 Foreign Data Wrappers (FDW) you can connect PostgreSQL to almost any remote data store. Version 9.6 brings improvements to the postgres_fdw, such as an option to control the fetch_size and the ability to “push down” operations ( joins and sorts ) to the remote PostgreSQL instance. If you want to aggregate data from multiple PostgreSQL servers, this is a huge win.

6. **Remote Apply** : PostgreSQL 9.6 adds a new replication method called 'remote_apply' where the master waits for the transaction to be applied on the remote side, not just written to disk. This is slower than the classic replication mode but not that much and it guarantees that all “commited data” are available for slave read. If you want the distribute read queries on multiple standby nodes, this new mode is for you !

Of course spotting only 6 items is a hard choice. They are many others enhancements in this release such as : Phrase Full Text Search, the pg_visibility extension, better vacuums on frozen pages, index-only scans for partial indexes, command progress reporting, and as always…… numerous performance improvements !

For a detailed view of this version, the wiki page below is a nice starting point : [https://wiki.postgresql.org/wiki/NewIn96](https://wiki.postgresql.org/wiki/NewIn96)




``Photo Credit :`` [duncan @ Flickr](https://www.flickr.com/photos/duncan/4280292398/sizes/z/) CC BY-NC

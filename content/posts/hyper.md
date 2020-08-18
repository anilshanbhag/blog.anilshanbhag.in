---
title: Hyper and In-Memory Databases
date: 2020-08-18
description: Why are in-memory databases not more popular ? 
tags: [db]
---

AWS has made it easy to get the latest and greatest hardware. You can easily get machines O(TB) of DRAM for a few dollars per hour. r5.16x large instance for example has the following specs:

```
r5.16xlarge	64vCPU	256ECU	512 GiB	EBS Only	$4.032 per Hour
```

TPC-H benchmark is a standard dataset is a popular OLAP benchmark. Scale factor 1000 of TPC-H benchmark generates 1TB of data which after removing ununsed columns and dictionary compression come to nearly 280GB of data. This dataset has 6 billion rows !
This dataset can easily be operated on using an in-memory database --- one of the best in-memory databases is Hyper. Hyper can operate at memory-bandwidth speed (~150GBps on a Xeon today). 

Hyper could processs queries on this dataset sub 2s for aggregation queries and sub 10s for more complex SQL queries. I find it surprising that today when most companies (all except big tech) likely have lesser than 6 billion rows and use things like Redshift / Snowflake to run their workloads. They could make their workloads like BI dashboards, ad-hoc analysis, etc much faster by simply using an in-memory database.

To try Hyper, download Tableau Server distribution and install it. You don't need a license to run Hyper. Once installed:

```
# cd to Tableau install dir/packages/hyper.<ver>/

./hyperd --log-dir . -d db --init open --skip-license --no-password configure. 

./hyperd --log-dir . -d db --init open --skip-license --no-password run

# connect using psql
psql -h localhost -U root -p <port>
```

The instructions work on Tableau Server 20.3. 

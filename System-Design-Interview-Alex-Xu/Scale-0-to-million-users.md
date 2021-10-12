===

All Credits - The Genius of <i>Alex Xu</i> **\[System Design Interview - An Insider's Guide\]**

===

- ### build a system that supports a single user and gradually scale it up to serve several million users. 
everything is on a single server : web app, database, cache etc.

- ### growth of userbase
separate web-tier and database-tier and scale independently.

which **database** to choose? 

Relational(SQL) and 

Non Relational(NoSQL) DBs - `KV stores`, `graph`, `column` and `document` stores. 

Use non-relational databases for:
- `super-low latency`, `unstructured data`, `massive data`, `SERDEs`

**scaling** `vertical` and `horizontal` - Vertical Scaling when traffic is low, comes with `hard limit` and has `no failover` or `redundancy`.

- ### bring in a Load-Balancer

Users connect to the Public IP of the load balancers directly. Private IPs are used for communication with servers. 

- ### Database Replication

usually with a master/slave relationship b/s original(master) and slaves. If `master` slave goes offline, one of the slaves will be promoted. <br>
In production, promoting a new master is complicated since a slave may be lagging at then - otherwise more complicated approaches like `multi-masters` and `circular replications` exist. <br>

- ### Add a Cache Layer

shift static content (JS/CSS/image/video files) to a `CDN`. Multiple Cache Servers to avoid `SPOF`. Also since Cache storages are volatile, the data as a `SSoT` needs to be<br>
established on a persistence layer. Also Caches must have `eviction policies` e.g `LRU`, `LFU`, `FIFO`. <br>
Some of the Considerations to use for CDNs - `cost` since CDNs are 3rd party, `appropriate cache expiry`, `fallbacks`, `invalidating files`, `object versioning` etc <br>

- ### stateless web-tier

move state out of the web-tier. Store session data in a persistent storage e.g Relational DB or a NoSQL. <br>
(Optionally, stateful servers enabled with sticky IP routing from Load Balancers, but adds more overhead). Other disadvantages include `Adding/Removing servers` and <br>
handling server failures. <br>

- ### GeoDNS

a `DNS Service` that allows domain names to be resolved into IP addresses basis location of the user. <br>
Replicate Data across multiple Data Centers. 
  



- Key Characteristics for distributed system:
  - Scalability: grow horizontally (add servers) vs vertically (add power)
  - Reliability (not vulnerable) vs Availability (be available)
  - Efficiency: latency and bandwidth
  - Serviceability/Manageability: easy to debug and patch

- Load Balancing (help horizontally adding servers): distribute traffic and stop requests when server's down
  - Can be added in 3 cases: ![load-balancer.png](img%2Fload-balancer.png)
  - LB algorithms: LCM, LRTM, LBM, RR, WRR, IP Hash https://www.cloudflare.com/learning/performance/types-of-load-balancing-algorithms/
  - Redundant LB: use 2 lb as a cluster to handle single failure of point

- Caching: (vertically, normally used in frontend): latest requested data is likely to be requested again
  - Types:
    - Application Server Cache: local storage (local memory or disk) of response data 
      - To avoid cache miss, use global cache or distributed cache
    - Content Distribution Network (CDN): for sites storing large amounts of static media
      - Alternative: serve static media from a lightweight HTTP server like Nginx first, when your system grow then change DNS to CDN
  - Cache Invalidation Schemes: keep cache data coherent with db
    - Write-through: data written to cache and db at the same time (best for data loss but high writing latency)
    - Write-back: data written to cache alone (low latency high risk of data loss)
  - Cache Eviction Policies:
    - FIFO, LIFO, LRU, MRU, LFU, RR

- Sharding/Data Partitioning
  - Schemes:
    - Horizontal Partitioning: Group different range of data in different tables (bottleneck: how to partition data evenly)
    - Vertical Partitioning: Separate features into different servers (bottleneck: user growth will cause more servers to be added)
    - Directory based Partitioning: loosely couple {data entity key:DB server}, can add servers to DB pool without having an impact on application
  - Criteria:
    - Key/Hash-based: Evenly distributed data but hash val changes each time adding new nodes, use consistent hashing to resolve
    - List Partitioning: Group and subgroup
    - Round Robin Partitioning
    - Composite Partitioning: combine 1-3 and customize
  - Common Problems: Joins and de-normalization, Referential integrity, re-balancing

- Indexes: catalogs to fastening data access 
  - Unnecessary indexes decrease write performance

- Proxies: server between clients and backend servers; can cache a resource and serve to all clients 
![proxy.png](img%2Fproxy.png)
  - Types: 
    - Open Proxy: Accessible by any Internet user
      - Anonymous Proxy: hide users IP address
      - Transparent Proxy: first IP address is disclosed
    - Reverse Proxy: obtain resource on behalf of a client

- Redundancy and Replication: replication shares info to ensure consistency among redundant components 

- SQL (relational) vs NoSQL (non-relational): rdb are structured and have predefined schemas, nosql db are unstructured distributed and dynamic (e.g. file system)
  - SQL: store data in rows and cols (MySQL, Oracle, MS SQL Server, SQLite, Postgres, MariaDB)
  - NoSQL: use different syntax then SQL
    - Key-Value Stores: Redis, Voldemort, Dynamo
    - Document Stores: CouchDB, MongoDB
    - Wide-Column/Columnar DB: store containers for rows, but each row doesn't have to have the same number of columns, good for analyzing large db (Cassandra, HBase)
    - Graph DB: store graph relationships (Neo4J, InfiniteGraph)
  - NoSQL can be horizontally scalable (cheap), SQL can be vertically scalable (expensive)
  - Most SQL db are ACID compliant - better bet on reliability and safety, NoSQL may sacrifice ACID compliance for performance and scalability
  - When to choose SQL over noSQL: 
    - Ensure ACID compliance 
    - Data is structured and unchanging
  - When to choose NoSQL over SQL:
    - Storing large Volumes of data with no structure 
    - To use cloud computing and storage
    - Rapid Development

- CAP Theorem: a distributed software system can't simultaneously provide > two out of three guarantees: Consistency, Availability, Partition Tolerance (CAP).
  - Consistency: can be achieved by updating several nodes before allowing further reads
  - Availability: Achieved by replicating data across servers
  - Partition tolerance: replicating data across servers and networks to keep system up through network down
  ![CAP.png](img%2FCAP.png)

- Consistent Hashing: improve caching system


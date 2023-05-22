## Concepts
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


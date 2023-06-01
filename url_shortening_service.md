## Design a URL Shortening Service like TinyURL
&nbsp;&nbsp;&nbsp;&nbsp;Similar services: bit.ly, goo.gl, qlink.me...
### Requirement Clarification
- Functional requirements:
  - Create a shorter and unique alias for a given url
  - Short URL will direct user to the original url
  - Customize link for the short url
  - Short url gets expired after a customized timespan
- Non-functional requirements: high availability for redirecting, low latency for creating, not predictable url
### API Design
- API: 
  - create_url(api_dev_key:str, original_url:str, username:str=None, custom_alias:str=None, expiration_date:str=None) -> String
    - Returns a shortened url, if fail returns an error code
  - delete_url(api_dev_key, url_key) -> String
    - Return "URL deleted" once url is retrieved
- Returns a shortened url, if fail returns an error code
### Estimation
- Traffic: number of directions, QPS rate
- Storage: number of objects to store, storage capacity
- Bandwidth: incoming data size, outgoing data size
- Memory: cache size
### DB Design: 
- large amount of records, each record is small, no relationship between records, read heavy - NoSQL Key-Value Pairs (Redis, Voldemort, Dynamo)
- Table design: URL + User
### Diagram: 
- 
### Dive in && Bottleneck:
- Key Generation
  - Encoding actual URL: 
    - what if actual url is encoded? what if multiple user all gets a same result with the same actual url? (add an increasing sequence/userid as salt, might get other problems)
  - Generate keys offline: 
    - KGS but you have to pay attention to concurrency (use two tables used/not used to store keys, lock data structure so only one server get a key at one time)
    - Replica to handle single point of failure
    - Learn to compute KGS DB size by base64 encoding and more
  - Key Lookup: HTTP 302 Redirect, HTTP 404 Not Found
  - Customer key size limit
- Data Partitioning: 
  - Range Based Partitioning: may results in un
- 
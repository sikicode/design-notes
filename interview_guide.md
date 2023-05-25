## System Design Interview Guide
### Standard Process
- Step1: Requirements Clarification
  - Use cases: as a ..., I want to ... so that ...
  - Non-functional requirements (optional): latency, bandwidth
- Step2: System Interface Design (API definition)
- Step3: Back of envelope estimation: scale, storage, network bandwidth
- Step4: Define data model: db table, entities, attributes
- Step5: High level diagram
- Step6: Dive in details (dive into 2 to 3 components): scaling, partitioning, load balancing and caching
- Step7: Resolve bottlenecks: performance, data replicas, single point of failure
![sdi time.png](img%2Fsdi%20time.png)
### Common API Parameters
- api_dev_key(string): API developer key for a registered user, you can pass username as well to double guarantee authentication ([Why API keys instead of username?](https://security.stackexchange.com/questions/32910/why-do-apis-use-api-keys-instead-of-usernames))
- user_name(string): used in encoding
- expiration_time(string): date & time to timeout a service
### Estimation Units
- [Calculate bit-byte-KB-MB-GB-TB-PB-EB](http://www.wu.ece.ufl.edu/links/dataRate/DataMeasurementChart.html)
- [Powers of 10](https://www.varsitytutors.com/hotmath/hotmath_help/topics/powers-of-10)
### Design Database
- [What's read-heavy?](https://www.mullie.eu/why-your-code-doesnt-scale/#:~:text=Being%20read%2Dheavy%20means%20there,being%20able%20to%20service%20requests.)
- Split User info into a separate table with primary key=UserID, other attributes can include email, name, creationDate, lastLogin time etc.
- Use hashing & encoding if you need a unique value for each result
  - [Encoding vs Encryption vs Hashing vs Salting](https://medium.com/hackernoon/what-devs-need-to-know-about-encoding-encryption-hashing-salting-stretching-76a3da32e0fd) 
  - [Encode Tools](https://emn178.github.io/online-tools/index.html)
  - [Unicode (UTF) vs Binary (base64/62/32)](https://stackoverflow.com/questions/22677217/what-is-the-difference-between-a-unicode-and-binary-string#:~:text=The%20former%20describe%20the%20machine,two%20domains%20is%20encoding%2Fdecoding.)
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
# Database design for usage prediction model inference

**Author**: Sebastian Krieger<br />
**Status**: DRAFT<br />
**Type**: DESIGN<br />
**Created**: 2025-10-21<br />
**Post-history**:  

Database design to support efficient and scalable inference for usage prediction models in the mobility platform.

# CONTEXT

The mobility platform is introducing machine learning models to predict vehicle usage patterns. These predictions need to be stored, queried, and updated efficiently to support real-time decision-making and analytics. The current database schema is optimized for transactional data, but not for storing model inference results, which are often time-series and require fast read/write access. The drivers for this decision include scalability, performance, and maintainability as the number of vehicles and predictions grows.


# DECISION

In the context of storing and retrieving usage prediction results for vehicles, facing the challenge of high-frequency writes and reads, we decided to implement a dedicated time-series database (e.g., TimescaleDB) for model inference results and neglected using the existing transactional database schema, to achieve high performance, scalability, and efficient querying of time-based data, accepting the downside of increased operational complexity and the need to maintain an additional database system, because time-series databases are optimized for this workload and provide built-in features for retention policies and aggregation.


# CONSEQUENCES

The impact of this decision is improved performance and scalability for storing and querying prediction results. Trade-offs include additional operational overhead, potential data consistency challenges between databases, and the need for team members to learn new database technologies. However, the benefits in query speed and scalability outweigh these concerns for our use case.


# COMPLIANCE

All data stored in the time-series database will comply with GDPR by ensuring personal data is anonymized or pseudonymized where necessary. Data retention policies will be enforced to automatically delete outdated predictions. Access controls will be implemented to restrict who can view or modify inference results, supporting DORA compliance for auditability and security.


# COMMENTS

Alternatives considered included extending the existing transactional schema or using a NoSQL database. References: [TimescaleDB documentation](https://docs.timescale.com/), [GDPR guidelines](https://gdpr.eu/). Further evaluation may be needed as the system scales.

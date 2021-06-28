# Work Experience

## Skills
**Language** Python, Scala,  Javascript, C++, Java  
**Web/API** Play Framework, React, Redux, Webpack, HTML, SCSS, GraphQL, RESTful API
**Database**  MongoDB, PostgresQL
**Infra / Tool**  Kubernetes, Kafka,  RabbitMQ, Splunk, Datadog, Vault, Jenkins, Docker
**Machine Learning**  Tensorflow, Scikit-Learn, Numpy, Pandas
**Knowledge**  Agile/Scrum Methodology, Continuous Integration/Continuous Delivery (CI/CD) , Service-Oriented Architecture (SOA), Backend/Full-Stack Software Development, Machine Learning, Object-Oriented Design,  API design, Bioinformatics

## Rally Health 
05.2018 ~ Current San Francisco, CA, United States

**Software Engineer II**  
Designed systems with stringent correctness, scalability and long-term maintainability to put healthcare in hand of millions of members.

### Security Initiative
- Established a fault-tolerant at-rest key rotation system to re-encrypt billions of records with PHI/PII in MongoDB  asynchronously without sacrificing microservices performance and warrant the safety of data of  50 millions members
  - Built a backward compatible service which can decrypt/encrypt records with both the legacy secret management tool and Vault
  - Increased the scalability by using RabbitMQ and Akka Actor with message-driven feedback control design
  - Set up a Kubernetes CronJob as retry/reconciliation mechanism to deal with failure

### Performance (p95)  Initiative
- Lead the effort to upgrade the MongoDB driver and adopt Wee-Pickle, an efficient Scala serialization system. The DB operation Read/Write Response Time (p95) of microservices is improved by 27%
- Redesigned the UI application and API discovery mechanism by reducing CORS and internal traffic routing within SPAs and edge services, and significantly reduced the initial page load time (p95) of SPAs by 30%
- Built a GraphQL endpoint with Play Framework, Scala and Sangria to reduce the number of API calls from SPAs by 70%

### CI/CD Initiative
- Pioneered in the journey from Continuous Integration (CI) to Continuous Delivery (CD) at Rally and reduced 90% of time spent on the software release process
  - Created missing functionalities in Jenkins pipeline library
  - Utilized Snyk for dependency / container scanning to ensure security
  - Certified software quality with enhanced regression / performance  / smoke test
  - Set up actionable alerts and crafted dashboards with Datadog and Splunk for post-deployment system monitoring

### Banzai Initiative
- A cross-team effort to bring about the schema management for applications to send /retrieve messages from Kafka clusters
  - Automated the Avro schema generation process from Scala case classes
  - Implemented the producer-defined schema registration mechanism upon services startup to ensure compatibility while schema evolution

## Alternative Military Service    
Taipei, Taiwan

> Diagnosed manual, repetitive tasks in different departments through interviews and built software in Visual Basic for Applications (VBA) as an interface to automate the process of interacting with a legacy system to reduce wasted time and error rate.

## DNArails 
Taipei, Taiwan 

**Software Engineer Intern**

> Built AnnoSeq, a software for rapidly detecting cancer-related mutation hotspots in sequencing data, which integrates data from multiple public/private databases to make annotation of genomic variants and creates data visualization with d3.js.

## University of Wisconsin, Madison
Research Assistant
>  Contributed to **MetaSRA**, a tool to generate annotation/re-coding of sample-specific metadata in the Sequence Read Archive based on biomedical ontology.

Teaching Assistant
> CS 576: Bionformatics

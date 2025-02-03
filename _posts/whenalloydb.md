---
layout: post
title: "Struggling to determine when to opt for AlloyDB vs CloudSQL"
subtitle: 
#description: ""
#cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/adp/associatedatapractitionerbadge.png
share-img: /assets/img/adp/associatedatapractitionerbadge.png
readtime: true
share-title: ""
#share-description: "TXXXXX"
#share-img: /assets/img/pcne/googlecloudprofessionalcloudnetworkengineerbadge.png
tags: [AlloyDB, CloudSQL, PostgreSQL, Google Cloud, Comparison]
---

There are various relational database options from Google Cloud including:

- AlloyDB (PostgreSQL)
- Cloud SQL Enterprise (MySQL, PostgreSQL and MS SQL Server)
- Cloud SQL Enterprise Plus (MySQL, PostgreSQL and MS SQL Server)
- Spanner (Proprietory with PostgreSQL interface)

AlloyDB is the latest product offering, boasting  significant performance enhancements and price performance benefits vs standard PostgreSQL. Whilst AlloyDB and CloudSQL offer fully managed service instances of PostgreSQL, it can be difficult to determine what product is best suited. In this blog, I offer some insight and guidance to help you determine what database offering you should consider depending upon your applications requirements. This should come in handy for those who are struggling to pick a product to start with

* toc
{:toc}

# What Database Offering Do I Need?

Prior to the arrival of AlloyDB in 2022, businesses looking to modernise their databases, reduce costs and avoid vendor lock in from proprietory database offerings typically opted to migrate to Open Source database offerings, frequently opting for PostgreSQL. Within Google Cloud, this would result in a migration to CloudSQL PostgreSQL. Many organisations have successfully migrated workloads to Cloud SQL PostgreSQL realising savings, performance optimisations and greater availablility and resiliency. Equally Cloud SQL PostgreSQL flexible compute size options and read only replica's have ensured applications get their required performance. However with the introduction of AlloyDB, it is no longer the defacto migration path, and furthermore, some applications already running on Cloud SQL may find they can get better price-performance from AlloyDB.

Unfortunately there isn't a silver bullet and it isn't as simple as saying 'for workload X choose AlloyDB, and for workload Y choose Cloud SQL' for the best price-performance. As with most things cloud related, the answer is 'it depends.'

# Spanner
Whilst Cloud Spanner isn't a PostgreSQL database offering, it offers a [PostgreSQL interface](https://cloud.google.com/spanner/docs/postgresql-interface) that provides limited supported PostgreSQL features. I've also heard people asking the question 'when should we use Spanner vs AlloyDB,' and the asnwer to this one is more easily defined, so I have included it here for reference. The use case scenarios regarding Spanner are typically when an application requires:

- Globally distributed multi master database.
- SLA of 99.999%

In these scenarios, Spanner is the only appropriate solution as neither AlloyDB or Cloud SQL offer either of these features. Spanner would also be a suitable product offering when extremely high performance requirements were required, above what Cloud SQL was capable of offering. Spanner's primary use case was workloads requiring high performancy, high availability and global consistency across multiple regions. The downside being this came at a comparitably expensive price point vs Cloud SQL, and required adopting a proprietory database (and in the case of migration, significant refactoring effort). 

However, AlloyDB is now able to bridge this gap with it's 4X performance improvements for transactional workloads, and 10X performance improvements for Analytical workloads, based on an enhanced open source PostgreSQL instance. As a result, applications that historically have required Spanner for performance reasons, may now find AlloyDB is capable of meeting the requirements that Cloud SQL missed.

# Cloud SQL PostgreSQL
Cloud SQL PostgreSQL is availale in two editions: Cloud SQL Enteprise, and Clous SQL Enterprise Plus. Before comparing against AlloyDB, it's important to highlight the key differences between these two products. which will go towards simplifying the AlloyDB comparison.

<CONSIDER ADDING ALLOYDB SECTION TO TOP DETAILING FEATURES ETC FOR COMPARISON/QUCIK REF. WEIGH UP VALUE OF CLOUD SPANNER TOO. POTENTIALLY TABLE COMPARING ALL TOGETHER>

## Cloud SQL Enterprise (PostgreSQL) vs Cloud SQL Enterprise Plus (PostgreSQL)
| Feature           | Cloud SQL Enterprise (PostgreSQL)                                                                   | Cloud SQL Enterprise Plus (PostgreSQL)                               |
|-------------------|---------------------------------------------------------------------------|---------------------------------------------------|
| Availability       | 99.95% highly available deployment             | 99.99% highly available deployment                 |
| Machine Types       | General purpose machine family                               | Performance optimised machine family                               |
| Machine Configuration Limits      | CPU: 96vCPU, Memory: 624GB RAM, 1:6.5 core:memory ratio                                      | CPU: 128vCPU, Memory: 864GB RAM, 1:8 core:memory ratio      |
| Maintenance Downtime         | <30 seconds                               | <1 second         |
| Data Cache        | No       | Yes                         |
| Point-in-time log retention     | Up to 7 days                                               | Up to 35 days                                 |

Applications requiring 4 9's availability, high performance, read caching, minimal downtime, and the ability to perform point in time restores greater than 7 days, would need to opt to Cloud SQL Enterprise Plus. If the application requirements are particularly low e.g. small instance ~2/4vCPU, a small volume of data, no read replica requirements, then Cloud SQL Enterprise (PostgreSQL) is likely to be the optimal solution from both a cost and performance perspective. However, if the requirements include read replicas, a large volume of data, and a larger instance sizing e.g. 32vCPU, comparisons against AlloyDB should be made. Depending upon the volume of data, nuber of read replicas, AlloyDB can offer significant cost savings as unlike Cloud SQL, storage costs are a flat cost regardless of how many read replicas.

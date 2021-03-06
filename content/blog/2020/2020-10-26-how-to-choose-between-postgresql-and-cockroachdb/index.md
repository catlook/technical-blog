---
layout: post
title: "How to choose between PostgreSQL and CockroachDB"
date: 2020-10-26
comments: true
author: Steve Croce
authorAvatar: 'https://gravatar.com/avatar/56d03e2d0f853cff39c129cab3761d49'
bio: "As Senior Product Manager for the ObjectRocket Database-as-a-Service
offering and Head of User Experience for ObjectRocket, Steve oversees the
day-to-day planning, development, and optimization of ObjectRocket-supported
database technologies, clouds, and features. A product manager by day, he still
likes to embrace his engineer roots by night and develop with Elasticsearch,
SQL, Kubernetes, and web application stacks. He's spoken at
KubeCon + CloudNativeCon, OpenStack summit, Percona Live, and various Rackspace
events."
published: true
authorIsRacker: true
categories:
    - Database
    - ObjectRocket
metaTitle: "How to choose between PostgreSQL and CockroachDB"
metaDescription: "As CockroachDB and PostgreSQL have consolidated a place in the market when it comes to relational
workloads, a number of folks have started asking which they should choose."
ogTitle: "How to choose between PostgreSQL and CockroachDB"
ogDescription: "As CockroachDB and PostgreSQL have consolidated a place in the market when it comes to relational
workloads, a number of folks have started asking which they should choose."
slug: "how-to-choose-between-postgresql-and-cockroachdb"
canonical: https://www.objectrocket.com/blog/cockroachdb/how-to-choose-between-postgresql-and-cockroachdb/
---

*Originally published on Aug 15, 2019 at ObjectRocket.com/blog*

As CockroachDB&reg; and PostgreSQL&reg; have consolidated a place in the market when it comes to relational workloads,
many folks have started asking which they should choose. CockroachDB offers true global-scale SQL with distributed
transactions and horizontal read/write scaling built-in for unprecedented scale, resiliency, and performance for
SQL workloads. However, there are still some scenarios where PostgreSQL might just be a better fit.

<!--more-->

{{<img src="picture1.jpg" title="" alt="">}}

### Similarities between CockroachDB and PostgreSQL

These two technologies overlap quite a bit. First and foremost, both boast:

* SQL compliance
* ACID transactions
* PostgreSQL wire protocol compatibility 
* Broad client driver and ORM support

This functionality covers most major points, which means the choice comes down to more nuanced decision points. With
only a few exceptions, you can try an app on top of either database and later transition to the other without having
to rewrite your app. 

Want to check out CockroachDB, but decide that PostgreSQL is a better fit? The chances are pretty good that you won’t
run into any trouble. Do you have an app running on PostgreSQL, but you’re looking for better scaling and failover?
CockroachDB could be a better fit.  

### Differentiators to help you decide

Compatibility, complex queries, scale, and flexibility might help you choose one option over the other.

#### Scale

The biggest difference is how the products handle scaling, replication, and high availability (HA). CockroachDB was
built from the ground up to provide a global SQL datastore with distributed transactions. You can spread your data
across clouds and regions with fine-grained control over what data is allowed to reside in each region or cloud.
Though solutions and extensions do exist for providing some of the same functionality with PostgreSQL, it’s not as
complete nor as straightforward to configure and manage.

CockroachDB’s focus on global scale allows it to be a lot more cloud-friendly. CockroachDB expects a large number of
smaller, disposable nodes, so scaling and HA are just handled effortlessly behind the scenes for you.

PostgreSQL, on the other hand, does provide a number of solutions for multi-master, scaling, and HA, but most of that
functionality is not included in PostgreSQL and requires third-party extensions. Also, the setup, configuration, and
day-to-day management are a bit more complex for an HA PostgreSQL deployment.

#### Flexibility

A real benefit of PostgreSQL is its many years of battle hardening and the scope of tunables and extensions. Just compare
the documentation for [Server Configuration](https://www.postgresql.org/docs/11/runtime-config.html) on PostgreSQL, and
you see a vast array of options and tuning parameters for your cluster. Want Isolation levels? You’ve got four options,
whereas CockroachDB gives you only one. Want replication? PostgreSQL gives you [eight alternatives](https://www.postgresql.org/docs/13/different-replication-solutions.html), while CockroachDB handles it behind the scenes.

PostgreSQL also offers a huge ecosystem of extensions to expand the product. Hundreds of extensions are publicly available,
and you can also write your own. These range from adding clustering (like Citus) to new objects (postGIS) to optimizing
PostgreSQL for a specific use case (Timescale). This flexibility definitely comes with a cost, though. It can introduce
complexity and impact the performance and stability of your instance. You could also end up misconfiguring your environment.
The CockroachDB approach simplifies things so that building and managing a cluster is straightforward.

#### Compatibility

If you need complete PostgreSQL or fuller SQL conformance, PostgreSQL is a better bet. Whether you’ve got a legacy app or you
need a backend store for a standard CMS or web framework, there could be a heavy reliance on the corners of PostgreSQL or SQL
that Cockroach might not support yet. Though Cockroach Labs continues to add more [features and functionality](https://www.cockroachlabs.com/docs/v19.1/sql-feature-support.html) to the product, it’s not 100% compatible with PostgreSQL yet.
Another area where you might see a difference is how CockroachDB handles roles, users, groups, and authentication. The PostgreSQL
authentication options are [extremely robust](https://www.postgresql.org/docs/current/client-authentication.html), and though
CockroachDB does offer [RBAC](https://www.cockroachlabs.com/docs/stable/authorization.html), there are some significant differences
between the two technologies.

You can overcome compatibility challenges, but it is ultimately up to your app and your ability to identify and address potential
incompatibilities.

#### Complex queries

An area where Cockroach Labs has invested a ton of effort has been the ability to perform joins and improve performance with
their [cost-based SQL query optimizer](https://www.cockroachlabs.com/blog/building-cost-based-sql-optimizer/). However, if
you have a Business Intelligence or analytics workload with extremely complex queries and multiple joins, views, aggregations,
and expression evaluations, PostgreSQL might be the better option.

This is an area where you can easily test with an evaluation or proof of concept. The closer your use case leans towards
analytics queries and OLAP, PostgreSQL might be the better bet. With quick OLTP-style transactions, CockroachDB can help the most.

### Summary comparison

| | CockroachDB | PostgreSQL |
| --- | --------| -----------|
| **Year of initial release** | 2015 | 1996 |
| **Current Stable Version** | 20.1.0 | 13 |
| **Licensing** | Business Source License [BSL](https://www.cockroachlabs.com/blog/building-cost-based-sql-optimizer) core components. Cockroach Community License [CCL](https://www.cockroachlabs.com/docs/v19.1/licensing-faqs.html#what-licenses-does-cockroachdb-use)enterprise features PostgreSQL License | PostgreSQL License |
| **SQ: Conformance\*** | Full or partial conformance with ~244 SQL:2011 features | Conforms with ~385 SQL:2011 features |
| **Bonus points** | Online Schema changes, distributed transactions |  Stored procedures, cursors, triggers, materialized views
| **Wire Protocol** | [PostgreSQL wire protocol](https://www.postgresql.org/about/licence/) | PostgreSQL wire protocol |
| **Client Drivers** | [Tested options](https://www.cockroachlabs.com/docs/stable/install-client-drivers.html) plus large ecosystem due to PostgreSQL wire protocol | Large ecosystem of official and community provided drivers |
| **CMS/Framework Compatibility** | Partial, via PostgreSQL wire compatibility | Broad support and compatibility for major frameworks 
| **Plugins/Extensions** | Enterprise feature pack | Large ecosystem of community extensions |
| **Replication/HA** | Yes, built-in | Via open source additions/extensions |
| **Multi-Master/Clustering** | Yes, built-in | Via open source additions/extensions |
| **Multi-Datacenter/Geo** | Yes, built-in | Custom or via open source additions/extensions |
| **Authentication** | Password, Certificate | Password, Certificate, GSSAPI, SSPI, Ident, LDAP, RADIUS, PAM, BSD |
| **Permissions** | User-based permissions and RBAC | RBAC with row and column level permissions, full SQL:2011 privilege support |
| **Strengths** | Cloud-native scaling, high availability, geo-distribution, straightforward configuration and deployment | Flexibility, tunability, compatibility, and ecosystem |
| **Weaknesses** | Latency and richness of SQL support/features | Complexity at scale, read performance
| **The Bottom Line** | Choose CockroachDB when you are building a highly transactional, OLTP-style workload, or the ability to scale out (locally or globally) is important | Choose PostgreSQL if your workload includes heavier analytics queries or you need access to a huge feature set, ecosystem, and compatible apps |

\* Since no datastore that I know of 100% conforms to the full SQL:2011 spec, I just looked at how much of the spec each product supports.

You have two great options before you. Both can be used in concert to create an amazing datastore portfolio. If you’re building from
scratch today and you don’t have extremely unique or PostgreSQL-specific needs and scaling matters, then look seriously at CockroachDB
as an amazing opportunity. However, if you already know what you need and want to focus on the broad flexibility of PostgreSQL, we can
help there as well.

Both PostgreSQL and CockroachDB are available now. Find which is the right fit for you.

### Conclusion

<a class="cta purple" id="cta" href="https://www.rackspace.com/data/dba-services">Learn more about Rackspace DBA Services.</a>

Use the Feedback tab to make any comments or ask questions. You can also click
**Sales Chat** to [chat now](https://www.rackspace.com/) and start the conversation.

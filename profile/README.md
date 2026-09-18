# Lakestream

**Building an open ecosystem around stream storage**

Lakestream is an open API and specification for stream storage on object storage, with a defined integration into the lakehouse. This organization is its open-source home. It hosts the specification, **Ursa** (our implementation of it) and **Ursa for Apache Kafka® (UFK)**, all under Apache 2.0.

## Why Lakestream

Parquet standardized the file. Apache Iceberg® and Delta Lake standardized the table on top of it, so any engine can read the same copy. Streams never got that. Durability came from replication between brokers, so the records, the consensus protocol and the process that ran them were one artifact.

Object storage changes that. Once durability belongs to the object store, what's left is a layout and a contract, and the Lakestream specification writes them down: how a stream is laid out in a bucket, how an append becomes durable, how offsets are assigned, how a cursor reads across what's been written and what's been compacted, and how a closed segment is registered as a table. It contains no protocol; the semantics clients see belong to the engine above the storage. Anything can read a stream without asking the process that wrote it.

![A lakehouse, holding data to analyze the business, and a Streamhouse, holding data to run the business, share one governance layer and one open infrastructure layer on object storage, where open table formats (Iceberg and Delta) and open stream storage (Lakestream) sit side by side.](./assets/lakehouse-streamhouse.svg)

A lakehouse holds data to analyze the business; a Streamhouse holds data to run it. They stand on the same foundation of object storage, open table formats and catalogs. The lakehouse got its half of that foundation opened a decade ago. Lakestream is our attempt at the other half.

## Projects

| Project | What it is | Status |
|---|---|---|
| [Lakestream specification](https://openlakestream.org/docs/specification) | The API and specification: stream catalog, log, cursors, data format, and how a stream becomes readable as a table | Evolving |
| [Ursa](https://github.com/lakestream-io/ursa) | The Java storage engine that implements the specification, embeddable in messaging brokers. Includes the stream materialization framework, which turns streams into lakehouse tables and other queryable states | 1.0 |
| [UFK](https://github.com/lakestream-io/kafka) | Ursa for Apache Kafka: a fork of Apache Kafka that adds Ursa as diskless storage. Diskless topics keep their records on object storage; every other topic stays Kafka | Developer preview |
| [leaderless-log-protocol](https://github.com/lakestream-io/leaderless-log-protocol) | The leaderless log protocol used in Ursa | Published |

Ursa keeps stream metadata in [Oxia](https://github.com/oxia-db/oxia), open source under the CNCF. Its storage is protocol-neutral: Ursa already runs under both the Kafka and Apache Pulsar® services in StreamNative Cloud. The open build ships with Kafka today; Pulsar is coming.

## Get started

Read the specification. Point a coding agent at it. Build something exciting and fun.

- **Read the specification:** [openlakestream.org/docs/specification](https://openlakestream.org/docs/specification)
- **Run UFK:** [quickstart](https://openlakestream.org/docs/ursa-for-kafka/quickstart) and [current limitations](https://openlakestream.org/docs/ursa-for-kafka/limitations)
- **Embed Ursa:** [quickstart](https://openlakestream.org/docs/ursa/quickstart)

## Build on it

Building on Lakestream doesn't need our permission. An engine for another protocol, sitting on the same storage the way UFK does. An implementation of the API in another language. A materializer for a system we haven't implemented yet. We expect others to build services on the same specification, including ones that compete with ours.

Contributions of every kind are welcome, to the specification as much as to the code:

- **Ask questions and share ideas** in [GitHub Discussions](https://github.com/orgs/lakestream-io/discussions).
- **Report bugs** as issues in the relevant repository.
- **Propose specification changes** in the open, as a discussion, before implementing them.
- **Send pull requests.** Sign off your commits with `git commit -s` (Developer Certificate of Origin). There's no CLA.

Lakestream, Ursa and UFK are licensed under the Apache License 2.0.

---

*Lakestream is stewarded by [StreamNative](https://streamnative.io).*

*Apache Kafka®, Apache Pulsar®, Apache Iceberg®, Apache Flink®, and Apache Polaris™ are trademarks of the Apache Software Foundation. Delta Lake is a project of the Linux Foundation. Unity Catalog is a trademark of Databricks, Inc. Snowflake Horizon Catalog is a trademark of Snowflake Inc. Amazon S3 is a trademark of Amazon.com, Inc. All other marks are the property of their respective owners. Lakestream, Ursa and UFK are not affiliated with or endorsed by the Apache Software Foundation.*

# Connect 

`docker run -it --network scripts-linux_default  --rm cassandra cqlsh apache-cassandra-db`


# Architecture

- Keyspace: defines how a dataset is replicated, for example in which datacenters and how many copies. Keyspaces contain tables.
- Table: defines the typed schema for a collection of partitions. Cassandra tables have flexible addition of new columns to tables with zero downtime. Tables contain partitions, which contain partitions, which contain columns.
- Partition: defines the mandatory part of the primary key all rows in Cassandra must have. All performant queries supply the partition key in the query.
- Row: contains a collection of columns identified by a unique primary key made up of the partition key and optionally additional clustering keys.
- Column: A single datum with a type which belong to a row.


# CQL

### Show cluster name and address

`SELECT cluster_name, listen_address FROM system.local`

### Create a Keyspace

create keyspace customer with replication = { 'class': 'SimpleStrategy', 'replication_factor': 1  };

### Create type

create type customer.address ( address text, city text, state text, zip_code text, country text);

### Create a table


create table customer.customer (id uuid primary key, name text, created_date date, addresses set<frozen<customer.address>>);
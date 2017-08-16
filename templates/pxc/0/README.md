# Percona XtraDB Cluster

### Info:

This template creates a Percona XtraDB Cluster on top of Rancher.

When deployed from the catalog, a three node cluster is created with a database, root password, database user and password. The cluster is set up for replication between all of the nodes. Health check monitors port 8000 for clustercheck status updates.

### Usage:

Once deployed, use a mysql client to connect:

`mysql -u<db_user> -p -h<pxc>`

### 分布式系统的CAP理论：

C：一致性，所有节点的数据一致；

A：可用性，一个或多个节点失效，不影响服务请求；

P：分区容忍性，节点间的连接失效，仍然可以处理请求；

任何一个分布式系统，需要满足这三个中的两个。

MySQLReplication：可用性和分区容忍性；

Percona XtraDBCluster：一致性和可用性。

因此MySQL Replication并不保证数据的一致性，而Percona XtraDB Cluster提供数据一致性。

Percona XtraDBCluster是MySQL高可用性和可扩展性的解决方案。Percona XtraDBCluster提供的特性有：
1. 同步复制，事务要么在所有节点提交或不提交。
2. 多主复制，可以在任意节点进行写操作。
3. 在从服务器上并行应用事件，真正意义上的并行复制。
4. 节点自动配置。
5. 数据一致性，不再是异步复制。

Percona XtraDBCluster完全兼容MySQL和Percona Server，表现在：
1. 数据的兼容性
2. 应用程序的兼容性：无需更改应用程序

它的集群特点是：
1. 集群是有节点组成的，推荐配置至少3个节点，但是也可以运行在2个节点上。
2. 每个节点都是普通的mysql/percona服务器，可以将现有的数据库服务器组成集群，反之，也可以将集群拆分成单独的服务器。
3. 每个节点都包含完整的数据副本。

优点如下：
1. 当执行一个查询时，在本地节点上执行。因为所有数据都在本地，无需远程访问。
2. 无需集中管理。可以在任何时间点失去任何节点，但是集群将照常工作。
3. 良好的读负载扩展，任意节点都可以查询。

缺点如下：
1. 加入新节点，开销大。需要复制完整的数据。
2. 不能有效的解决写缩放问题，所有的写操作都将发生在所有节点上。
3. 有多少个节点就有多少重复的数据。
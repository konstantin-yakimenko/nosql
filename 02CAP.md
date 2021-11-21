## CAP теорема

### MongoDB
MongoDB можно назвать строго консистентной только если работает только одна нода.
В случае кластера запись идет на primary ноду и есть возможность читать из secondary.
В случае партицирования и недоступности primary ноды происходит выбор новой primary.
Таким образом кластер Replica-Sets MongoDB обеспечивает
- устойчивость к партицированию
- высокую доступность
- консистентность в конечном счете.

По классификации CAP: **AP**

### MSSQL
MSSQL реляционная бд, которая позволяет создвать различные [типы репликаций](https://docs.microsoft.com/en-us/sql/relational-databases/replication/types-of-replication?view=sql-server-ver15):

| Replication type | Description |
| ------ | ------ |
| Transactional replication | Changes at the Publisher are delivered to the Subscriber as they occur (in near real time). The data changes are applied to the Subscriber in the same order and within the same transaction boundaries as they occurred on the publisher. |
| Merge replication | Data can be changed on both the Publisher and Subscriber, and are tracked with triggers. The Subscriber synchronizes with the Publisher when connected to the network and exchanges all rows that have changed between the Publisher and Subscriber since the last time synchronization occurred. |
| Snapshot replication | Applies a snapshot from the Publisher to the Subscriber, which distributes data exactly as it appears at a specific moment in time, and does not monitor for updates to the data. When synchronization occurs, the entire snapshot is generated and sent to Subscribers. |
| Peer-to-peer | Built on the foundation of transactional replication, peer-to-peer replication propagates transactionally consistent changes in near real-time between multiple server instances. |
| Bidirectional | Bidirectional transactional replication is a specific transactional replication topology that allows two servers to exchange changes with each other: each server publishes data and then subscribes to a publication with the same data from the other server. |
| Updatable Subscriptions | Built on the foundation of transactional replication, when data is updated at a Subscriber for an updatable subscription, it is first propagated to the Publisher and then propagated to other Subscribers. |

В зависимости от типа данные синхронизируются либо одельными транзакциями, либо блоками.
MS SQL предоставляет мощный [инструмент по разрешению конфликтов](https://docs.microsoft.com/en-us/sql/relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication?view=sql-server-ver15)
Но не в ущерб доступности.

По классификации CAP: **AP**

### Cassandra
Cassandra может быть отнесена к AP или CP в зависимости от [настроек](https://docs.datastax.com/en/archived/cassandra/3.0/cassandra/dml/dmlConfigConsistency.html)
При одних настройках достаточно дождаться ответа только от одной ноды, при других от всех нод кластера.

По классификации CAP: **AP** или **CP** в зависимости от конифигурации

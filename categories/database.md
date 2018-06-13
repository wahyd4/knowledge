# Relation
- Mysql
- Postgres
- Microsoft SQL Server
- Oracle
- Sqlite

# NoSql
- Monodb
	- Replica Set
		- Primary
		- Secondary
		- Hidden
- Redis
	- Cluster
		- Strong recommend 3 masters and 3 slaves
- Hbase
- Cassendra

# SQL
- Index
	- Index is unique but not mandatory
- join
- MYSQL
	- tips
		- datetime
			- 8 bytes
 			    `1000-01-01 00:00:00 ~ 9999-12-31 23:59:59`
			- store a absolute value
		- timestamp
			- 4 bytes `1970-01-01 08:00:01 ~ 2038-01-19 11:14:07`
			- will impacted by time zone
			- index by timestamp will be faster than datetime due to 4 bytes.

## SQL join diagram

![sql join diagram](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/Knowledge.mindnode/resources/FC67BE77-F837-4207-B3C4-45205F7C9C40.png)

# Message Queue

# Rabbitmq

# activeMQ

# Redis

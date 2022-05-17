# Neo4j

Using graph database in order to increase the chance of preventing a security breach by identifying anomalies faster and easier using a graph system/ database such as Neo4j

if you think about messaging withing the department of state what are some factors or signs of a data breach or an employee being compromised or participating in underhand activities. 
 
one way is to look for out of the ordinary behaviors or anomalies and in order to do that you can use metadata and messages to get results such as using locations, number of users, and specific users


so said

USER sends messages to LOC 1. and the n_users from there are 40
USER sends messages to LOC 2 and the n_users from there are 80
USER sends messages to LOC 3 and the n_users from there are 15
USER sends messages to LOC 4 and the n_users from there are 1 



you can also use: 
Location in combination with frequency or volume as well as associated such as same department Bureau ect.

ACID compliance: 
	- atomicity: the integrity of the entire database transaction not just a component of it. In other words if one part of a transaction doesn't work like it's supposed to the other will fail as a result and vice versa 
	- consistency: only data which follows those rules is permitted to be written to the database if a transaction occurs and results in data that does not follow the rules of the database it will be rolled back to a previous iteration of itself 
	- isolation: ability for a database to concurrently process multiple transactions 
	- durability: data is there once a transaction is completed even if a power outage or system failure occurs 


NEO4j written in java and scala 

Enterprise and community 

Enterprise includes backups clustering and failover abilities

Cypher a declarative query language similar to SQL but optimized for graphs 

Constant time traversals 

Drivers for popular programming languages including Java JavaScript .NET Python and many more 

Drivers connect to NEO4j either through Http or through the Binary Bolt Protocol

Binary Bolt protocol:  it is based on the pack stream serialization and supports the cypher type system protocol versioning authentication and TLS via certs for Neo4j clusters bolt provides smart client routing with load balancing and failover
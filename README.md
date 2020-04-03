

# Graph Database

### General

A graph database is useful to model the entity relationship, exactly in the way as it exists in the physical world. The key feature that separates graph based database from every other database if their ability to store the relationships, and the connections as first class entities. 

A general graph based database has two units: 
  - Nodes
  
    Noun cases: a person, place, or a thing, or a valued data name. Each of these nodes are identified using a named label.
          
        Example: a 'name' node is a node with label, 'Name', that has the properties: 'firstName', 'middleName', 'lastName'.
        There can exist another node called 'Name' representing buildings, or a place, or a thing.
        
  - Relationships
  
    Each of the nodes are connected by means of what we call it a relationship. Say two nodes, Person can be conected with a     relationship, 'IS_FRIEND'. 
          
        Example: (Person) - [:IS_FRIEND] -> (Person) 

### Key

The graph database can be found to be used with following constraints:  
  - Table Name (Labels)
  - Rows (Nodes)
  - Columns (Properties)
  - Joins (Relationships)
  
Unique features: 
- A Node can have as many labels. 
- Nodes with same labels need not bear same set of properties. 
- Relationships/schema can be created as and when it is required in real time.

### Perks of using a graph database over traditional database system

- Length of the general query is very long and difficult to read when it comes to a general database 
- Most SQL queries for large scale organizations are tangled with joins that are completely functional, but impractical with respect to performamce as its size increases. 
- Graphs make it easier to model and store relationship.
- Relationship traversal can be computed in constant time, even with growing data size.
- Additional of properties or relationships can be done without the need of any schema migration.


# Neo4j

### General

Neo4j serves as a benchmark for asset compliant, transactional database. It comes with a graph platform, that has the following features which are inline with the another general purpose database as well.  
  - Index free adjacency, every connected component can be traversed in constant time without the need of an index.
  - ACID (Atomic, Consistent, Isolated, Durable), if a relationship between nodes are created, they are updated as the connection is established. 
  - Clusters, and extensive library support
  - Availability of tools, and language driver enabled support
  
### Converting a relational database to a graph based database

  - Glance in the ER-diagram of your relational database
  - Locate the foreign keys, and replace them with RELATIONSHIPS
  - Identify the join tables, and eliminate the same with RELATIONSHIPS or RELATIONSHIPS with property values (if they are attributed join tables)

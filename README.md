

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
  
  
# Cypher

### General

Cypher is basically the graph query language, which is purely based on patterns. Patterns in Cypher use ASCII-Art in the following manner: 
    
    1. Nodes
    
    - Nodes are surrounded by parantheses
    Example: (), (Person)
    
    - Labels, or tag, start with ':', and group nodes by roles or types
    Example: (p:Person)
    
    - Node can have properties, delimitted by curly brackets. 
    Example: (p:Person {first_name: 'Pukar', last_name: 'Acharya'})
    
    
    2. Relationships
    
    - Relationships are wrapped with hyphen or square brackets
    Example: -->, -[h: HIRED]->
    
    - Directions in a relationship is established with >, or a <
    Example: (p1) - [h:HIRED] -> (p2), (p1) <- [h:HIRED] - (p2)
    
    - Relationships have properties as well 
    Example: - [HIRED {type: 'full_time'}) -> 
    
    Here: h, p1, p2 are references that can be used at later end while using the query. 
    
    
Example: query to return who drives a car owned by a lover
    
    MATCH
          (p1:Person) - [:DRIVES] -> (c:Car) - [:OWNED_BY] -> (p2:Person) <- [:LOVES] - (p1)
    RETURN
          p1

### Create Data

    Example: 
           <-------- Node --------->               <-------- Node --------->
    
    CREATE (:Person {name: 'Pukar'}) - [:LOVES] -> (:Person {name: 'Julie'})
    
           <-Label->                                         <--Property-->

### Query Data

    Example 1: who does Pukar love?
    
    MATCH
         (:Person {name: 'Pukar'}) - [:LOVES] -> (op:Person)
    RETURN
         op
          
          
    Example 2: finding Pukar's car? 
    
    MATCH
        (:Person {name: 'Pukar'}) - [:DRIVES] -> (c: Car)
    RETURN
        c
          
    OR, 
    
    MATCH
        (p:Person] - [:DRIVES] -> (c: Car)
    WHERE
        p.name = 'Pukar'
    RETURN
        c
          
    OR more specific description/properties of the car, 
    
    MATCH
        (p:Person] - [:DRIVES] -> (c: Car)
    WHERE
        p.name = 'Pukar'
    SET
        c.brand = 'Voodoo', 
        c.model = 'V2'
    RETURN
        c
    
### Create Uniqueness

    Example 1: say a named node, 'Pukar' should be made in such a way that there exists no duplicate records
    
    CREATE CONSTRAINT ON (p:Person})
    ASSERT p.name IS UNIQUE 
    
    Example 2: 
    
    MERGE (a: Person {name: 'Pukar'})
    CREATE (a) - [:HAS_PET] -> (:Dog {name: 'Jack'})
    
    ==> looks into the graph for a person named Pukar, instead of creating a new node Pukar, and operates on the person node if it exists, or else it will create a new node
    
    Example 3: 
    
    MERGE (a: Person {name: 'Pukar'})
    ON CREATE SET
      a.instagram = '@iampukar'
    MERGE (a) - [:HAS_PET] -> (:Dog {name: 'Jack'})
    
    ==> looks into the graph for a person named Pukar. Else create a new node, and set it's property 'twitter', and then create a HAS_PET relationship from Person Pukar to Dog named Jack, ONLY IF that pattern exactly doesn't exist in the graph.
    
### Case Sensitivity

    Case Sensitive: Node labels, Relationship types, Property keys
    Case Insensitive: Cypher keywords (like, MATCH, RETURN)
    
### Aggregates

    WHERE - used to filter results
    
    Example 1:
    
    MATCH (m: Movie)
    WHERE m.title = "Ice Age"
    RETURN m
    
    Example 2:
    
    MATCH (p:Person) - [r:ACTED_IN] -> (m;Movie)
    WHERE m.released >= 2000
    RETURN m.released, a.name
    
Note:

    * null doesn't mean NULL explicitly, but relates to missing or undefined values. Meaning, the value doesn't exist on that given node.
    
    * =~ allows us to do regular expression matching.


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

### Key:

The graph database can be found to be used with following constraints:  
  - Table Name (Labels)
  - Rows (Nodes)
  - Columns (Properties)
  - Joins (Relationships)
  
Unique features: 
- A Node can have as many labels. 
- Nodes with same labels need not bear same set of properties. 
- Relationships/schema can be created as and when it is required in real time.

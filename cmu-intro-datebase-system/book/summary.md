# Introduction
## What and Why is DBMS?
DBMS are ued to manage colelctions of data that:
- High valuable
- Relative large
- Accesses by multiple stakeholders

2 main models:
- OLTP (online transaction processing): Main goal is support a large amount of users when each of them will process on a relative small of data
- OLAP (data analytics): Working on a large amount of data at once

## Why don't use file system directly?
- Data redundancy and inconsistency
- Access and query data problem
- Data isolation
- Data intergrity is not ensured
- Atomicity problems
- Concurrent-access problem
- Data authority problem

## Data models

Data model is conceptual tools for describing data, data relationships, data semantics and data constrainnts

4 different categories of data models:
- Relational model: data and relationships among them are represent by tables. Also known as record-based model.
- Entity-relationship model: Collection of entities and relationship.
- Semi-structured Data Model: The semi-structured data model permits the specifi-
cation of data where individual data items of the same type may have different sets of attributes
- Object-based data model: Database systems allow procedures to be stored in the database system and executed by the database system. This can be seen as extending the relational model with notions of encapsulation, methods, and object identity.

## Relational Data model

Data and relationship among them are abstracted to tables and columns. 3 abstraction level:
- Physical abstraction: Abstract the process of how data is stored in physical memory
- Logical abstraction: Abstract what data is being stored and relationship among them
- View level abstraction: Not every user needs to view full context of database but a subset of them. The subset is called View

Instance vs Schema:
- Instance is the data being stored at a particular time. (backup instance, current instance)
- Schema is a set of definition of database. There're 2 types:
  - Physical schema: How data being store
  - Logical schema: What data being store 

Database engine:
- Storage managemer: The storage manager is the component of a database system that provides the interface between the low-level data stored in the database and the application programs and queries submitted to the system:
  - Component: Authorization and Integrity manager, transaction manager, file manager, buffer manager.
  - Physical data structure implement: data files (data itself), data dictionary (data metadata), Indices (indexes)
- Query processor:
  - Component: DDL interpreter, DML compiler (query optimization engine), query evaluation engine 
- Transaction management:
  - Component: Recovery manager and concurrency-control manager
  - Recovery manager takes place in ensure Atomicity and Durability 
  - Concurrency-control manager takes place in isolation

## Chapter Summary
- A database-management system (DBMS) consists of a collection of interrelated data and a collection of programs to access those data. The data describe one particular enterprise.
- The primary goal of a DBMS is to provide an environment that is both convenient and efficient for people to use in retrieving and storing information.
- Database systems are ubiquitous today, and most people interact, either directly or indirectly, with databases many times every day.
- Database systems are designed to store large bodies of information. The management of data involves both the definition of structures for the storage of information and the provision of mechanisms for the manipulation of information. In addition, the database system must provide for the safety of the information stored in the face of system crashes or attempts at unauthorized access. If data are to be shared among several users, the system must avoid possible anomalous results.
- A major purpose of a database system is to provide users with an abstract view of the data. That is, the system hides certain details of how the data are stored and maintained.
- Underlying the structure of a database is the data model: a collection of conceptual tools for describing data, data relationships, data semantics, and data constraints.
- The relational data model is the most widely deployed model for storing data in databases. Other data models are the object-oriented model, the object-relational model, and semi-structured data models.
- A data-manipulation language (DML) is a language that enables users to access or manipulate data. Nonprocedural DMLs, which require a user to specify only what
data are needed, without specifying exactly how to get those data, are widely used today.
- A data-definition language (DDL) is a language for specifying the database schema and other properties of the data.
- Database design mainly involves the design of the database schema. The entityrelationship (E-R) data model is a widely used model for database design. It provides a convenient graphical representation to view data, relationships, and constraints.
- A database system has several subsystems.
  - The storage manager subsystem provides the interface between the low-level data stored in the database and the application programs and queries submitted to the system
  - The query processor subsystem compiles and executes DDL and DML statements.
- Transaction management ensures that the database remains in a consistent (correct) state despite system failures. The transaction manager ensures that concurrent transaction executions proceed without conflicts.
- The architecture of a database system is greatly influenced by the underlying computer system on which the database system runs.Database systems can be centralized, or parallel, involving multiple machines. Distributed databases span multiple geographically separated machines.
- Database applications are typically broken up into a front-end part that runs at client machines and a part that runs at the backend. In two-tier architectures, the front end directly communicates with a database running at the back end. In threetier architectures, the back end part is itself broken up into an application server and a database server.
- There are four different types of database-system users, differentiated by the way they expect to interact with the system. Different types of user interfaces have been designed for the different types of users.
- Data-analysis techniques attempt to automatically discover rules and patterns from data. The field of data mining combines knowledge-discovery techniques invented by artificial intelligence researchers and statistical analysts with efficient implementation techniques that enable them to be used on extremely large databases.

# Data system
- System store data for sometime and give some kind of access protocol (Database, Cache Service or event Message Queue)
- Different kind of data system fit for some kind of task (indexing system for search, caching system, OLTP database, message queue). Combining them make great application but also lead to some different problems

# Foundation
## Reliable
**The system should continue to work correctly (performing the correct function at the desired level of performance) even in the face of adversity (hardware or software faults, and even human error)**
### What is work correctly?
- A system works correctly is a system which works as expectation include:
    - Performs function as user expected 
    - Can tolerate the user making mistakes (tolerant protocol) or using the software in unexpected way (validation?)
    - Performance is good enough for the required use case, under expected load and data volume. (System limitation)
    - Prevent any unauthorized acces and abuse
- Things go wrong called faults. System ftolerating certain types of fault 
### Some common fault
#### Hardware fault
- Hardware can fault anytime. For example GCP Cloud SQL monthly uptime percentage is 99.95%. There are 43200 minutes in a month (for average 30 days), 99.95% uptime percentage => there're 21 minutes (round down from 21.6) downtime a month in estimated. So the question is what do in that 21 minutes?
- Multi-machine-redundancy can be a good solution. With 0.05% percent downtime each machine, if we have 3 machine so the downtime percentage just 5*$10^6$% monthly downtime percentage.
- Rolling update can used for some specific cases (like we have to shutdown for some upgrade,etc...).
#### Software fault
- Software bug, leak on resource (process runaway but keep hold the resource), cascading failures (a component fault lead to system fault) and slowdonw because of system lead to corrupted response.
- Come from the assumption (which is not always correct). For example, assumpt SQL will be in uptime forever (like from above).
- There's no quick solution for this kind of error. Do some small things can help: thinking about assumption and interaction in the system (with well document. Document a system is a good way to think all over again), thorought testing, allowed processed to crash and restart. Monitoring and analyzing system is a must.
#### Human errors
- Human are unreliable
- Some approaches to prevent: 
    - Minimizes opportunities for error, balance restriction and flexibility (Use case, UI/UX)
    - Decouple places where people make the most mistakes from the places where they can cause failure. (Give them place to play)
    - Test (Unit), test (intergration) and test (E2E). More test, more conner case, less human errors.
    - Recovery quickly from error (revert, rollout)
    - Set up detail and clear monitoring with some good metrics (error rate on feature for example). Add tracking if needed for more detail and make decision based on metrics.
    - Make a good training, user-guide.
## Scalable

**As the system grows (in data volume, traffic volume, or complexity), there should be reasonable ways of dealing with that growth**

#### What is the load?
- Based on the architecture of system (RPS, R/W ratio, CCU, cache hit rate,...etc). Each system has its own definition of load
#### What is performance?
- After we have the load, we have the performance number (throuhgput, repsonse time,... etc).
- What do we do when the load's increased and keep performance the same
- Pencentile and histogram is reasonable in case using for performance metric
#### Handle the load
**An architecture that scales well for a particular application is built around assumptions of which operations will be common and which will be rare** (load parameters. Wrong parameters -> wrong assumption)
## Maintainable
**Over time, many different people will work on the system (engineering and operations, both maintaining current behavior and adapting the system to new use cases), and they should all be able to work on it productively**
- No one like to fix other's bug T.T 
- To avoid create legacy system ourselves, follow 3 principles:
    - Operability: Make it easy to keep the system running smoothly (old version running smoothly => if new version fail just rollback :D )
        - A good ops (sysops, devops) team can help. System should be built to make routine task easy.
    - Simplicity: Make it easy for new engineers (at some level) to understand the system, by removing as much complexity as possible from the system:
        - Complexity can be in many forms: Explosion of the state space (many state), tight coupling of modules, tangled dependencies, incosistent naming and termiinology (one object different naming), hack aimed at solving performance problems, special-casing to work around (ad-hoc case)
        - How to manage complexity of a project? -> Reduce accidental complexity. What is accidental complexity? -> Not inherent in the problem that the software solves but arises only from the implementation -> Use abstraction
    - Evolvability: Make it easy for engineers to make changes to the system in the future. Also known as extensibility, modifiability or plasticity:
        - Making change easy. Your system's requirement won't remain unchanged. Using some working pattern can help (TDD and refactoring). If you want to refactor -> must ensure system do the thing right -> TDD come to the rescue
# Data model
- Application are built by layering one data model on top of another. Each layer hides the complexity of the layers below it by providing a clean data model. The key question is **How is it represented in terms of the next-lower layer?**

## Relational model
- In relational model, data is organized in **relations** (table). Each relation is an unordered collection of **tuples** (row).
- Relational model lie in business data processing
- Use-cases:
  - Transaction processing (support for banking processing, booking, ticketing, etc...)
  - Batch processing (customer invoice, payroll, etc...)
- How NoSQL (not only SQL) birth? -> Different application has different requirement. Relational model is not fit for all use-cases so we need different model for different use-cases (polyglot persistence)

## Problem of Relational model
- Object-relational mismatch: Some extra jobs have to be done to mapping application object and relation model (ORM, etc...)
- Handle One-to-many relationship is sometime awkward (multiple way to do it, like using foreign key and join table, using unstructured data type, etc..)

## Problem of NoSQL
- Handle many-to-many or many-to-one relationship is often weak
- Support of join is depended on the engine
- This lead to hard to normalize data (data duplication, data inconsistency, etc...)

## Choosing between document and relational databases based on model

### Application need?
- If application has document-like structure (a tree of one-to-many relationships where always loaded at once), then the document model can be a good fit.
- If application has many-to-many relationships, then the document model is awkward and less efficient. The relational model is a better fit.

### Schema flexibility
- If the schema is likely to change, then a document model may be more flexible and therefore easier to evolve. (schema-on-read)
- If the schema is unlikely to change, then a relational model may be better, because it can enforce schema constraints more rigourously. (schema-on-write)

### Data locality for queries
- If the application frequently needs to access the same document together, then storing the document in one place is more convenient (document model)

### Convergence of document and relational databases
- Relational databases are adding support for JSON documents, and document databases are adding support for relational-like joins.

## Query Language

### Imperative query
- Pure code
### Declarative query
- Declarative abstract (or hide) the implementation detail of database engine. This lead to database engine can introduce the improvement itself and doesn't require any application change. The downside is it's more limited in database function

Example:
- SQL
- CSS

### MapReduce query:
- Somewhere in between declarative query (restricted by database engine) and imperative query (write code). 
- Powerful tool (since it can call to many other functions)
- Example of supported engine:
  - MongoDB

## Graph-like data model
- Consists of two kinds of object: vertices and edges
  - Vertices contains:
    - Identifier (ID)
    - Set of inbound edges
    - Set of outbound edges
    - Its information
  - Edges contains:
    - Identifier
    - Tail vertex (start)
    - Head vertex (end)
    - Relationship label
    - Its properties
- Used it own query languange:
  - Cypher Query Languange 
  - SQL for Graph
  - SPARQL (Use with triple store model)
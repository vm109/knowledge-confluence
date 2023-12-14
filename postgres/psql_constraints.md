### Constraints like Primary Key and Foreign Key    

- What is the role of primary and foreign key in normalization process and data integrity?
    - Primary key and foreign key are necessary to maintain the data integrity.
    - Primary key and foreign key role in data integrity
        - Primary key does require the column to be not null. So we can rely on primary key to believe the data is not missing
        - Foreign key relation makes sure that when a record in one table is related to the other then the record in other table is available.


- What is the role of primary key in data integrity and reliability?
    - Primary Key enforces no NULL values and duplicates
    - Since foreign keys refere to the primary keys in other tables it ensures no orphaned records are formed
    - Primary key uniquely identifies records and thus maintains uniqueness of records.

- What is the role of foreign key in data integrity and reliability?
    - Foreign key maintains `referential integrity` by ensuring records are present with primary_key in related table. 
    - Foreign key prevents orphans. As Foreign key relates a record in one table to the primary_key in another table. 
    - Foreign key can cascade `delete` and `update` that is any changes to primary_key are propagated to the foreign_key column thus maintaining consistency.

- Can you summarize how are primary key and foreign key are important?
    - Foreign key is essential for referential integrity and making sure records are present with primary_key in other table, thus donot allow creation of orphan records in related tables.
    - Foreign key maintains this integrity by cascading any changes in primary_key to foreign_key
    - Primary key maintains data integrity by maintaining uniqueness in records and allow no null values.

- How do foreign keys contribute to query optimization?
    - Foreign key defines the relation between tables. 
    - So when JOINs between tables are made on foreign keys, it allows query optmizer to generate optimized query plan.
    - Foreign keys are created using indexing on referenced and referencing columns. Query optimizer can use these indexes to create optimized query plan.

- Why is it importnt to have foreign key relationship between tables in a relational database? 
    - to have refrential integrity 
        - this includes cascading any updates and deletes of the related primary key
    - `avoid creating orphaned records`. So this again comes under referential integrity. 
    - Enforced relationship between tables.
        - When tables are normalized A complete record makes sense only when multiple records across tables are joined. 
        - So these relationship of tables can be enforced with foreign key. 
    - And also having foreign key between related tables will imporve the performance of the query. 
        - As query optimizer will look at the relation of the tables by foreign key and create a optimized query plan.

- What are the drawbacks of using a foreign key? 
    - There is a overhead of creating tables in order when intially setting tables with foreign key relations. 
    - Unintended data loss due to incorrectly handled cascaded update and delete
    - Those databases with write intensive workload foreign keys will introduce more latency as it needs to check the existence of record in the referenced table.
    - foreign keys will have impact during operations like large data migrations and imports.

<!-- # TODO -->
- What happens if you try to insert a value into a foreign key that does not exist in referenced primary_key?

- What are self referencing foreign keys and why are they used and is there any example?

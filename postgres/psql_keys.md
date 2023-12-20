### Primary Keys, Foreign Keys, Composite Keys, Unique keys

- **Primary Key**: 
    - A primary key uniquely identifies a record within a table.
    - A Primary key guarantees that the value is not null for that column.
    - A primary key also guarantees that values are unique in the column.
    - We can only crate one primary key constraint per table.

- **Foreign Key**:
    - Foreign key relates 2 tables, i.e a primary table record references a record in another table with a foreign key.
    - Foreign key values can be NULL meaning that particular record is not referencing anything in the other table. 
    - Foreign key establishes relation between tables in a relational db model. 
    - Foreign key allows query optimizer to create a optimized query plan.
    - Foreign key ensures `referential integrity`, that is a foreign key column cannot contain other values than the values present in related/referenced primary key column. Thus ensuring no orphan values in the foreign key column.

- **Unique Key**: 
    - A non primary key can also have a unique contraint. 
    - A column or set of columns can be unique.
    - This makes sure records in the unique key column are unique. 
    - Unique key column does not gaurantee records to not null. 
    - Unlike primary key there can be multiple unique keys in a table.

- **Composite Key**: 
    - Since a Primary key needs to be unique identifier, some times only one column of the table cannot saisfy that condition. Composite keys are used where single column cannot identify a record uniquely.
    - So a combination of 2 or more columns can form a primary key called composite key. 
    - How can a composite key referenced in another table?
        - if table1 has column1, column2 as primary composite key and table2 wants to rrefer table1 then table2 have to create foreign key on both column1 and column2. 
        - `FOREIGN KEY (reference_column1, reference_column2) REFERENCES table1 (column1, column2)`
    - composite keys natuarally occur in tables which relates 2 tables. 
        - example in a task_manager with tasks and users. the table like `task_assignment` which relates both the above tables will naturally have composite keys.


- What is the difference between unique keys and primary keys?
    - Unique keys only represent column values are unique. 
    - Unique keys donot guarantee values are not null.
        - so a unique key column can have multiple null values.
    - Unlike primary key a table can have multiple Unique keys.
    - Primary keys are `indexed` which enhances the data retrieval. But unique keys are not indexed.

- can we restrict the values of a column to be not null even though the column is not a primary key?
    - yes we can add a not null constraint to the column and restrict it from adding any null values. 
    - `Alter table <table_name> alter column <column_name> SET NOT NULL`

- Some useful psql commands for adding and droping constraints on a table
    - To add a primary key `alter table <table_name> add constraint <constraint_name> primary key(<column_name1>, <column_name2>...)`
    - To add a foreign key `alter table <table_name> add constraint <constraint_name> foreign key(<column_name>) references <reference_table>(<column_name>)`
    - To make a column unique `alter table <table_name> add constraint <constraint_name> unique (<column_name>);`
    - To drop a contraint on a table `alter table <table_name> drop constraint <contraint_name>`    

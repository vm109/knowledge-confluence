### Indexing

- What is indexing in sql?
    - Indexing helps to easily identify records when the record set is huge. 
    - indexing uses sorting algorithms to sort data based on a column or multiple columns
    - When we create a primary key then the data is indexed based on the key. 
        - how does this work if the key is composite key?
    - Indexing can be done either `physically sorting` or `logical sorting`
    - some of the popular indexing is b-tree indexing. 
        - well suited for integers, text, date
    - Indexing has both pros and cons. 
        - Indexing helps to optimize read queries and read join queries.
        - Indexing helps to optimize aggregate queries and sorting queries
        - While Indexing can slow the write process. 
        - can we index on read replicas and not index on write replicas of a cluster?
    - When the index is compound index i.e index on multiple columns how would that effect the index sorting process?

- What are the indexes used for JSON types?
    - GIN is used for indexing JSON data. 
    - Generalized Inverted Index.

- What is a partial Index? 
    - Partial index is only created for a subset of rows based on a condition to reduce idnex size and improve performance of specific queries.
    - Some scenarios where we could use a partial index
        - If specific queries which target a category are significant then we can create index on that subset of rows belonging to that category. 
        - If most of the queries are on recent data then we can create partial index on that recent data
        - ```sql 
                create index <index_name> on <table_name> (<column_name>, <column_name>) where <condition>
            ```
    - This reduces index size, improves query performance
    - But to create partial index we need to monitor usage pattern            

- Does indexing means sorting data and how does that affect in compound indexes say for example timestamp and json columns or timestamp and text columsn as they are different types?
    - Indexing does not mean sorting the entire table necessarily, but it creates a separate new data structure.
    - In psql b-tree is default index type and it is efficient in searching, updating and deleting.
    - psql will create a sorted data structure for indexed columns only.
    - B-tree is efficient with comparable types like strings, integers, timestamps
- What are unique indexes? 
- What are high selective indexes and how does that affect query optimization?
- Why is index monitoring important and how can we do that in postgres?


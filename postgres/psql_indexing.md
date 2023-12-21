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
    - When the index is compound index i.e index on multiple columns how would that effect the index sorting process?

- What are the indexes used for JSON types?
    - GIN is used for indexing JSON data. 
    - Generalized Inverted Index.

- What is a clustered index and non-clustered index and their differences?
    - clustered index orders the data physically.
        - clustered indexes maintain data and index in one place. 
        - since index and data are in one place data retrieval is much faster. 
        - But data modifications will result will data re-organizaing/re-order which will cause data modification to take longer.
        - there should be **only one** clustered index per table.
    - non-clustered index does not affect physical order of the rows.    
        - non-clustered index donot physically re-order the data.
        - index structure and actual data are seperate. And there will be pointers from index to the data
        - as the index and data are separate data retrieval takes little longer than clustered index
        - but as the index structure is separate from data, any data modification will be quick.

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

- In Psql does primary key create a clustered index?
    - In PSQL primary key does not guarantee creation of a clustered index. 
    - A primary key simply creates a unique index, which does not necessarily mean clustered index.
    - we need to exclusively define a clustered index and there can only be one clustered index.

- Does indexing means sorting data and how does that affect in compound indexes say for example timestamp and json columns or timestamp and text columsn as they are different types?
    - Indexing does not mean sorting the entire table necessarily, but it creates a separate new data structure.
    - In psql b-tree is default index type and it is efficient in searching, updating and deleting.
    - psql will create a sorted data structure for indexed columns only.
    - B-tree is efficient with comparable types like strings, integers, timestamps

- Can we index on read replicas and not index on write replicas of a cluster?
    - In a clustered setup usually indexes are cretaed on master replica.
    - So I guess it is not an option to have indexes on read replicas while not having index on write replicas.

- What is index rebuilding and why should we do that and how we do that?
    - indexes are structures built on the data of indexed columns.
    - as data is changed we need to re-build the index. Although in most of the databases restructuring if indexes are self managed.
    - why should we do re-indexing or rebuild a index?
        - **data fragmentation**: 
            - when data is inserted, updated or deleted then data fragmentation happens.
            - i.e over time data stored in index is not efficiently organized which makes data retrieval from index ineffecient.
            - the exact reasons of fragmentation is internal details but we can know if fragmentation happened or not by monitoring the index performance.
            - we need to rebuild a index to make the index efficient again.
            - Postgres sql handles index rebuilding automatically, we can also chose to manually rebuild index.
            - regular monitoring of indexes will help to identify any fragmentaion of the indexes. 
            - regular maintenance of indexes like `VACCUM` or `REINDEX` can help to make the index efficient again.
        - **stastics update**: 
            - re-building the indexes always involves updating index stats.
            - index statstics maintain stats about how data is distributed in a column, which helps query planner to chose a index for a query or to not use a index.
            - index stats are usually maintained by postgres automatically.
            - we can also trigger a stats update by `ANALYZE`   
        - postgres sql will trigger autovaccum whenever data updates,inserts and deletes happen. This will update the   index `data distribution` stats frequently. So the query optimizer will always have a optimized low cost query.
        - we can also manually `VACCUM`/`REINDEX` to rebuild index and also manually `ANALYZE` to update data distribution stats                  

- In practice did you create a index and is it clustered or un-clustered?
    - I did create indexes for several use-cases.
    - but in most cases I did not create a clustered index. 
    - I did not see a use cases where our queries are super dependent on one column.
    - sql command for creating a index. 
      ```sql 
        CREATE INDEX <index_name> on <table_name>(<column_name>)
      ```

- How to see the query plan to check the difference of query before and after index?
    - we can execute `EXPLAIN <sql>`
    - this will show the sql query plan
    
- Scenario1: 
    - I have created a index on a Array column
    - by default it created a b-tree
    - then changed to GIN index. 
        - CREATE INDEX <index_name> ON <table_name> USING GIN (<column_name>)
    - ran `Explain <sql with where conditio on indexed column>` 
    - but the query plan is showing a sequntial scan 
    - So sometimes even though we have created a index, query planner will chose to do sequential scanning if the `data distribution stats` are not enough for the query planner to use index.
    - **can I force to use a index in a sql?**
        - **No** index usage in a query cannot be forced. 
        - But we can make sure that a column has an index. 
        - And some times if the monitoring suggests that the index is slow, and fragmentation happenend on the index we can `REBUILD` index
        - Or if we can run `ANALYZE` to update the `data distribution` stats. 
        - these ways we can allow query optimizer to use the index.

<!-- TODO -->
- What are unique indexes? 
- What are high selective indexes and how does that affect query optimization?
- Why is index monitoring important and how can we do that in postgres?
- What should we consider when we create a compound/composite index?
    - compound/composite index is when we create a index on 2/more columns
    - `create index <index_name> on <table_name> using <index_type> (<column_name1>, <column_name2>)`
    - so when we create a composite key which is a primary key then we dont need to create a index seperately unless we need to change the index type that is from BTree to GIN/GIST etc


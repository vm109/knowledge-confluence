### basic interview questions
- What is a jsonb type in psql? how is it different from json
    - jsonb stores data in byte format and json stores in text format. 
    - jsonb is more eficient and faster to query and also stores keys in sorted order. 
    - jsonb also supports indexing on individual keys. 
    - jsonb is smaller in size than json
    - jsonb validates for general json format but donot validate for duplicate keys.
- How can you query and manipulate json data in psql?
    - for selecting a single key in json we use `->` operator.
    - i.e for example 
    ```sql  
     select taskdata->'id' from dailytasks
    ```
    - here in this example taskdata is column name, id is key in json, dailytasks is tablename.
    - for where condition in a json data we use `->>` operator
    - i.e 
    ```sql
     select * from dailytasks where taskdata->>'id'='taskid1322
     ```
- What is denormalization and where would you use denormalization process?
    - Denormalization is a way of maintaining the data of a record in one place even it means to repeat some parts of it multiple times.
    - it should be used when we need to join multiple tables multiple times which is inefficient and inperformant.
    - also when data retrieval is frequent than data modification
    - so it should be used when complexity and inefficiency of joins outweighs the redundancy of data.

- What is the difference between insert, update and upsert and when should each of those used?
    - insert: inserts data into a table 
    - update: updates an existing data record in a table with a condition. 
    - upsert: is a combination of insert and update.  

- How do you upsert in psql?
    -  ```sql
        insert into tablename(column_with_constraint, column1, column2) values(value1, value2, value3) on conflict (column_with_constraint) do update set column1=value1, column2=value2
    ```       
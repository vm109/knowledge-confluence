### Postrgres Triggers
1. How did you use triggers in your application and why are they used? 
    - Triggers are stored procedures which are executed on special events like `insert`, `update` and `delete` into the database.
    - Triggers help to maintain data integrity by validation logic. i.e; to not update or insert when a special condition matches.
    - I used trigger to avoid circular redirects on documents. i.e when a redirect is created from A -> B -> A
    - Why I have crated a trigger instead of business logic in the application is as the source of the truth is within database and it would be extra network call to get the redirect data and make the check. Also the logic is simple enough and per row basis which justifies to be a database trigger.
    ``` sql
    IF THEN
        RAISE EXCEPTION  'reason for exception';
    END IF
    ```
    - usually we create a function which is execute on each row before insert/update

2. What are the components of trigger? 
    - `function` -  to execute when a trigger is matched
    - `level` - will the trigger function execute for each row or for the entire statement.
    - `timing` - BEFORE, AFTER a sql statement i.e before insert, after update, before delete
    - `new and old` - a trigger function validation is done on NEW and OLD row record.

3. How to effectively use triggers? 
    - triggers come with an efficiency cost. i.e whenever a transaction is done there is a overhead of the trigger
    - so we should properly maintain the indexes and use the indexed columns to be efficient while triggering functions. 
    - we can batch process triggers by using statement level triggers than row level triggers when possible. 
    - keep the trigger function logic simple and avoid complex logics and reduce the entire transaction time.
    - avoiding or keeping cascaded triggers as minimal as possible to reduce the latency overhead of a transaction.
    - triggers usually acquire locks on affected rows. So we need to judiciously use triggers
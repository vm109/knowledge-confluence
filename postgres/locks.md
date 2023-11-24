### Postgres Locks

1. What is the difference between pessimistic locking and optimistic locking? 
    - Those are 2 different strategies/approaches used to proceed with a transaction while updating a existing record. 
    - Pessimistic locking assumes there will be conflicts while updating a existing record. 
        - So in pessimistic locking, lock on that record is acquired imnmediately before any update. 
        - pessimistic locking is done by using `select * ... for update`
    - Optimistic locking assumes that conflict while updating a record is minimal.
        - a version number is maintained or a time stamp is checked. While updating the record if there is a change/conflict in version number obtained before and while updating then the transaction will not be done.


2. How are Pessimistic Locking and Optimistic locking  done?
    - Pessimistic Locking: A Lock is exclusively obtained on the record on which transaction is done. Once the transaction is done Lock is exclusively released. 
        - Example: `select * ... for update`
    - Optimistic Locking: A revision/time stamp is maintained to determine if there is a conflict in record before updating the record. If the revision is same before transaction started and while updating then update is done or will not be done.

3. Are there any implications with any of these locking strategies/approaches?
    - Pessimistic Locking: 
        - Since pessimistic locking is done by acquiring lock on the records exclusively those records will be locked till the transaction is done. which will block any other transactions on that record and will have efficiency implications. 
        - can lead to reduced performance in highly conccurent application due to contention.
    - Optimistic Locking: 
        - There are no exclusive locks on any records, so though there is no latency or blocking implications there is a overhead of maintaining the version of the records for determining the conflicts while updating records.  
        - Additional application logic is reqquired to detect conflicts   

// TODO: add the details here
4. Give some practical Examples for usage of these and how did you implement it in your code?
    - did you use pessimistic locking and how did you acquire lock and how did you release lock?
    - did you use optimistic locking and how did you determine there is a conflic between the versions while updating?

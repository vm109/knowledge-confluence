### Normalization of Data

- What is normalization of data?
    - Normalization is a way of reducing redundancy in data. 
    - Normalization enforces consitency of data through primary and foreign keys
    - In Normalization any big tables are split into smaller and related tables.
    - Through primary and foreign key contraints data consistency and integrity/reliability is maintained

- Briefly summarize all 3 normalization forms?
    - 1NF: Each column should represent only one type of data 
    - 2NF: should obey 1NF and non primary key attributes should be `fully depend on primary key` without partial dependency. 
        - 2NF is when 
        - i.e for example (empid, projectid, employeename, skill_of_project_needed)
        - here (empid, projectid) are primary key
        - but a non-primary key `skill_of_project_needed` is only dependent on projectid.
        - so a non-primary attribute is only partially dependent on the primary key.
    - 3NF: should obey 2NF and there shouldnt be any transient dependency in non-primary key columns. i.e one non-primary attribute can be derived from the other non-primary key
        - Transient relationship is, if we can derive the value of a `non-primary` column from the other non-primary column. like if we have `date of birth` and `age` columns, those are transiently dependent.       

<!-- TODO question -->
- Foreign Key Contraint: Should the foreign key unique? If not how to maintain data integrity in relations of data? 
    - for example [studentid, course ]   [course, instructor] same course can have multiple instructors?
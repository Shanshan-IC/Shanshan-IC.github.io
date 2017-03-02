---
layout:     post
title:      "SQL Paritioning"
category:   SQL 
tags:       SQL
---
* content
{:toc}

The example is test in Postgre SQL.

Step 1: Create the big table

```sql
CREATE TABLE student (student_id bigserial, name varchar(32), score smallint);
```

Step 2: Create the sub Table

```sql
CREATE TABLE student_qualified (CHECK (score >= 60 )) INHERITS (student) ;
CREATE TABLE student_nqualified (CHECK (score < 60)) INHERITS (student) ;```

table student_qualified and student_nqualified will cover inherits the big table.

Step 3: Define the rule or Trigger

Even we define the CHECK Condition, when insert new data into table student, Postgre SQL couldnot find the subtable. So we need to create the rule to make sure data inserted into the correct partition.

Firstly, let us define the Rule

```sql
CREATE OR REPLACE RULE insert_student_qualified 
AS ON INSERT TO student 
       WHERE score >= 60
       DO INSTEAD
       INSERT INTO student_qualified VALUES(NEW.*);

CREATE OR REPLACE RULE insert_student_nqualified 
AS ON INSERT TO student 
       WHERE score < 60
       DO INSTEAD
       INSERT INTO student_nqualified VALUES(NEW.*);
```

Step 4: insert some data into the table

```sql
INSERT INTO student (name,score) VALUES('Jim',77);
INSERT INTO student (name,score) VALUES('Frank',56);
INSERT INTO student (name,score) VALUES('Bean',88);
INSERT INTO student (name,score) VALUES('John',47);
INSERT INTO student (name,score) VALUES('Albert','87');
INSERT INTO student (name,score) VALUES('Joey','60');
```

Step 5: show the data distribution

```sql
SELECT p.relname,c.tableoid,c.* 
FROM student c, pg_class p
WHERE c.tableoid = p.oid
```

We also define the Trigger to make conditions for insertion.

```sql
CREATE OR REPLACE FUNCTION student_insert_trigger()
RETURNS TRIGGER AS 
$$
BEGIN
     IF(NEW.score >= 60) THEN
         INSERT INTO student_qualified VALUES (NEW.*);
     ELSE 
         INSERT INTO student_nqualified VALUES (NEW.*);
     END IF;
     RETURN NULL;
END;
$$
LANGUAGE plpgsql ;

CREATE TRIGGER insert_student 
    BEFORE INSERT ON student
    FOR EACH row
    EXECUTE PROCEDURE student_insert_trigger() ;
```

If the trigger doesnot work, you have to open the trigger, in postgresql.conf, to define 

track_functions = all

In the end, I test the create table and select operations status in partitioning, compared with the original big table. Even the speed to create table is quite slow, but the selection is significantly quicker than the original table.
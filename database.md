# Database (Oracle)

## Constraints

### What are the constraints applicable on a table?

* Not null,
* Primary key
* Unique
* Foreign key
* Check

## keys

### What are the differences between  primary key and unique key?

Unique key constraint is used to prevent the duplication of key values within the rows of a table and allow null values. 

Primary key allows each row in a table to be uniquely identified and ensures that no duplicate rows exist and no null values are entered. Only one by table. Primary key is a special unique key


## triggers

## When are triggers useful

1. To drive column values automatically.
1. To enforce complex integrity constraints.
1. To enforce complex business rules.
1. To customize complex security authorizations.
1. To maintain replicate tables.
1. To audit data modification.
1. Generate ID (Oracle < 12g)

### Can triggers do commits?

Committing in a trigger is not allowed because a trigger is part of a larger transaction.
Exception: PRAGMA AUTONOMOUS_TRANSACTION; but in that case it will be another transaction

### trigger types

#### Statement triggers

Executed when a statement is executed

#### Row trigger

Executed for each row affected by a dml statement.

`:new` and `:old` are the variable to get values before and after a statement.

#### Instead of trigger

These triggers has useful to intercept dml on views and execute an alternative dml on other tables.

#### user event trigger

Executed on ddl, user logon/logoff. This could be useful for setting up a user session.

#### System event trigger

Executed on system events such as DB startup, shutdown, server erros

## unsorted

### What is a transaction? 

A transaction symbolizes a unit of work performed within a database management system (or similar system) against a database, 
Atomicity requires that each transaction be "all or nothing"
The consistency property ensures that any transaction will bring the database from one valid state to another.
The isolation property ensures that the concurrent execution of transactions results in a system state that would be obtained if transactions were executed sequentially
The durability property ensures that once a transaction has been committed, it will remain so, even in the event of power loss, crashes, or errors.

source: [wikipedia](https://en.wikipedia.org/wiki/ACID)

## truncate vs delete

Truncate is a ddl command, delete is a dml command.

Truncate, no where clause, table lock, Minimal logging in transaction log, so it is perform faster.

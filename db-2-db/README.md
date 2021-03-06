# Database to Database!

## Introduction
This scenario exports data from a table one database to table in another database. 

## Screencast of this Quickstart

Link to a screencast of this quickstart on our youtube channel:

[![DB-2-DB Quickstart](https://img.youtube.com/vi/BeVK5RCkog0/0.jpg)](https://youtu.be/BeVK5RCkog0)

*`<<Click to Play>>`*


## Getting Started

You can follow with the video above to build the integration or you can import the [DB-2-DB-export.zip](DB-2-DB-export.zip?raw=true).

The Start connection fires according to a simple schedule and selects rows from a table every minute. 

`SELECT * FROM contact`

The Finish connection inserts data into the contact table which in this case is in the very same database.

`INSERT INTO todo (task, completed) VALUES (:#task, 0)`

The SELECT from the start step returns the collection of data. Because of that, we have to add 'split' step from which the integration is continuing for every item from the collection. 
**Note** that in our case, the collection contains only one item so the rest of the integration after the split step is done only once. If `SELECT * FROM contact` returned 10 items, 10 items would insert in the final step.

The output of the Start connection are the fields "first_name, last_name, company, lead_source and create_date". The input is simply one field 'task'. So there is a data shape mismatch and a 'datamapper' is required. In the datamapper we combine `firstname + " " + lastname + " " + company` and map that into the `task` field. Note that the data shapes are calculated dynamically based on the queries given in the database donnections. Parameters are prefixed with `:#`.

## What did we learn?

* We used a Database Connector to read and write from and to a table.
* We used the datamapper to map in and output data.

## Extra Credit

You can check what's going on using the Todo app using the url you obtain using 

echo http://todo-syndesis.`minishift ip`.nip.io

and also, you can login to the DB pod using

```
oc get pods
oc rsh syndesis-db-1-c84cz
sh-4.2$ psql -Usampledb
sampledb=> select * from todo;
```


# Persistence with tingoDB Database

"Persistence" implies storing data somewhere that won't disappear when
the power goes out.  This could be a simple file where you know the
format or it could be more formal, such as a "database" which will
serve to help accessing the data when it gets large (a database
management system standardizes how to access the data file optimizes
certain types of access).

Relational databases are the type where data are stored in a
table-like organization (e.g., rows, columns).  And the entries can be
structued or unstructured.  Relational databases can use multiple
tables for storage efficiency (imagine one table that lists your home
address and one table that lists all of the books you have checked out
of library).  Usually there is a "primary key" that cross-references
tables; this is often somthing like an account number, social security
number, or phone number.

Because we want to run our database on a low-resource device (the pi),
we want a compact DB implementation. One alternative is a "key/value"
database. In this type, the values can be unstructured and the model
for access is very simple (but perhaps less access speed efficient).

<p align="center">
<img src="/docs/images/databases.jpg" width="30%">
</p>
<p align="center">
<i>Relational database</i>

For a relational database, we will use
[TingoDB](http://www.tingodb.com) which is a relational database
similar to mongoDB but is more compact and works on a laptop or pi.

In this skill you will set up a database, write some data to it, and
then read it back out.

## Assignment
1. Install tingoDB and any helper apps to bring up node and the db on your laptop
2. Use a simple data structure to host sensor data (time, sensor_id, smoke, temperature).
Time is seconds since Jan 1, 1970, smoke is logical, and temperature is in C.
3. Use the [smoke.txt](/docs/skills/docs/smoke.txt) file as your data source
4. Write the data into your db
5. Demonstrate a query to the database to retrieve all instances (time and temperature) when sensor ID 1 has smoke.
6. Report

## Reference material
- [Smoke.txt File](/docs/skills/docs/test-data/smoke.txt)
- [Tingo DB recipe for sensor data](/docs/recipes/docs/tingo.md)
- [TingoDB](http://www.tingodb.com) 
- [Tutorial on Node.js and Mongodb](https://www.w3schools.com/nodejs/nodejs_mongodb.asp)

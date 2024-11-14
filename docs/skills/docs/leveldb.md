# Persistence and Databases

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

Because we want to run our database on a low-resource device (the Pi),
we explore another variant: a "key/value" database. In this typle, the
values can be unstructured and the model for access is very simple
(but perhaps less access speed efficient).

<p align="center">
<img src="/docs/images/databases.png" width="80%">
</p>
<p align="center">
<i>(a) Relational database, (b) Key/value stores>
</p>

We tested [LevelDB](http://leveldb.org), a key/value database with a
Node.js interface on the Pi zero recently and it worked pretty
well. It's lightweight and easy to use. You are free to use any
database you want, but this is a good starting point. Note: on the Pi,
in 2019 this required node v9 (v10 was an issue due to 32-bit issues)

In this skill we want you to set up a Leveldb database on your laptop
 to log and retrieve data from a collection of sensors in your
 system. (Later you may need to do this on a pi for a quest.)


## Assignment
1. Install leveldb and any helper apps to bring up node and the db on your laptop
2. Use a simple data structure to host sensor data (time, sensor_id, smoke, temperature). Time is seconds since Jan 1, 1970, smoke is logical, and 
temperature is in C.
3. Use the smoke.txt file as your data source. 
4. Write the data into your db
5. Demonstrate a query to the database to retrieve sensor IDs with smoke and their temperature
6. Report

## Reference material
- [Database Design Pattern](/docs/design-patterns/docs/dp-db.md)
- [LevelDB](http://leveldb.org)
- [Intro to LevelDB and node](http://web.archive.org/web/20130502222338/http://dailyjs.com/2013/04/19/leveldb-and-node-1/)
- [Smoke.txt File](/docs/skills/docs/test-data/smoke.txt)

- [Installing LevelDB on RPi](https://thisdavej.com/beginners-guide-to-installing-node-js-on-a-raspberry-pi/)
- [More](https://www.raspberrypi.org/forums/viewtopic.php?t=140747)
- [More](https://itnext.io/introduction-to-node-js-a-beginners-guide-to-node-js-and-npm-eca9c408f9fe)
- [More](https://github.com/cncjs/cncjs/wiki/Setup-Guide:-Raspberry-Pi-%7C-Install-Node.js-via-Node-Version-Manager-(NVM))
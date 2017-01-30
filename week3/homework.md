## Homework 3.1
Start a mongod server instance (if you still have a replica set, that would work too).

Next, download the handout and run:
<pre>mongo --shell localhost/performance performance.js</pre>
<pre>homework.init()</pre>

Build an index on the "active" and "tstamp" fields. You can verify that you've done your job with
<pre>db.sensor_readings.getIndexes()</pre>

When you are done, run:
<pre>homework.a()</pre>
and enter the numeric result below (no spaces).

Note: if you would like to try different indexes, you can use `db.sensor_readings.dropIndexes()` 
to drop your old index before creating a new one. (For this problem you will only need one index 
beyond the `_id` index which is present by default.)

<pre>db.sensor_readings.createIndex({active:1, tstamp:1})</pre>

## Homework 3.2
In a mongo shell run `homework.b()`. This will run in an infinite loop printing some output as it runs various statements against the server.

We'll now imagine that on this system a user has complained of slowness and we suspect there is a slow operation running. 
Find the slow operation and terminate it.

In order to do this, you'll want to open a second window (or tab) and there, run a second instance of the mongo shell, with something like:

<pre>$ mongo --shell localhost/performance performance.js</pre>
Keep the other shell with homework.b() going while this is happening. Once you have eliminated the slow operation, run (on your second tab):
<pre>db.currentOp()</pre>
<pre>db.killOp()</pre>
<pre>homework.c()</pre>
and enter the output below. Once you have it right and are ready to move on, ctrl-c (terminate) the shell that is still running the homework.b() function.

## Homework 3.3

Download and extract the json file in products.zip

Then perform the following in the terminal (or at the command prompt):
<pre>mongoimport --drop -d pcat -c products products.json</pre>
If that looks somewhat familiar, that's because it's (nearly) the same command you used to import the pcat.products collection for Homework 2.1, with the only difference in the command being that it will drop the collection if it's already present. This version of the collection, however, contains the state of the collection as it would exist once you've solved all of the homework of chapter 2.

Next, go into the pcat database.

mongo pcat
Create an index on the products collection for the field, "for".
<pre>db.products.createIndex({for: 1})</pre>
After creating the index, do a find() for products that work with an "ac3" phone ("ac3" is present in the "for" field).
<pre>db.products.find({for: 'ac3'})</pre>
Q1: How many products match this query?
db.products.find({for: 'ac3'}).count()
Q2: Run the same query, but this time do an explain(). How many documents were examined?
Q3: Does the explain() output indicate that an index was used?
Check all that apply:
Q1 : 4
Q2 : 4
Q3 : Yes

## Homework 3.4
Which of the following are available in WiredTiger but not in MMAPv1? Check all that apply.

`Document level locking`

`Data compression`

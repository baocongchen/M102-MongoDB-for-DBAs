### Homework 1.1
Download and install MongoDB from [www.mongodb.org](https://www.mongodb.org). Then run the database as a single server instance on your PC (that is, run the mongod binary). Then, run the administrative shell.
From the shell prompt type
<pre>
db.isMaster().maxBsonObjectSize
</pre>
at the ">" prompt.

What do you get as a result?
<pre>
16777216
</pre>

### Homework 1.2
Download Handouts:
[Products__hw1.2_m102_529e39a8e2d42347509fb3f0.json](https://university.mongodb.com/static/MongoDB_2017_M102_January/handouts/Products__hw1.2_m102_529e39a8e2d42347509fb3f0.3eb7cd1a9633.json)
Download the handout. Take a look at its content.

Now, import its contents into MongoDB, into a database called "pcat" and a collection called "products". Use the mongoimport utility to do this.

When done, run this query in the mongo shell:
<pre>
db.products.find( { type : "case" } ).count()
</pre>
What's the result?
<pre>3</pre>

### Homework 1.3
At this point you should have pcat.products loaded from the previous step. You can confirm this by running in the shell:
<pre>
db.products.find()
// or:
db.products.count()
// should print out "11"
</pre>
Now, what query would you run to get all the products where brand equals the string "ACME"?
<pre>db.products.find({brand:"ACME"})</pre>

### Homework 1.4
How would you print out, in the shell, just the value in the "name" field, for all the product documents in the collection, 
without extraneous characters or braces, sorted alphabetically, ascending? (Check all that would apply.)
<pre>
var c = db.products.find( { }, { name : 1, _id : 0 } ).sort( { name : 1 } );
while( c.hasNext() ) {
    print( c.next().name);
}
//OR
var c = db.products.find( { } ).sort( { name : 1 } );
c.forEach( function( doc ) { print( doc.name ) } );
</pre>

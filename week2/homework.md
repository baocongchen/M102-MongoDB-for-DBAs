## Homework 2.1
Download Handouts:
- [Homework2__hw2.1_m102_529fe537e2d42347509fb412.js](https://university.mongodb.com/static/MongoDB_2017_M102_January/handouts/Homework2__hw2.1_m102_529fe537e2d42347509fb412.a51ae9e0ff0e.js)
- [Products__hw1.2_m102_529e39a8e2d42347509fb3f0.json](https://university.mongodb.com/static/MongoDB_2017_M102_January/handouts/Products__hw1.2_m102_529e39a8e2d42347509fb3f0.3eb7cd1a9633.json)

We will use the pcat.products collection from week 1. So start with that; if not already set up, import it:
<pre>
mongoimport --drop -d pcat -c products products.json
</pre>
You can find products.json from the Download Handouts link.

In the shell, go to the pcat database. If you type:
<pre>
use pcat;
db.products.count()
</pre>
the shell should return 11.

Next, download homework2.js from the Download Handouts link. Run the shell with this script:
<pre>
mongo --shell pcat homework2.js
</pre>
First, make a mini-backup of the collection before we start modifying it. In the shell:
<pre>
b = db.products_bak; db.products.find().forEach( function(o){ b.insert(o) } )
 // check it worked:
b.count()
// should print 11
</pre>
If you have any issues you can restore from "products_bak"; or, you can re-import with mongoimport. (You would perhaps need in that situation to empty the collection first or drop it; see the --drop option on mongoimport --help.)

In the shell, type:
<pre>
homework.a()
</pre>
What is the output? (The above will check that products_bak is populated.)
<pre>3.05</pre>

## Homework 2.2

Add a new product to the products collection of this form:
<pre>
{
    "_id" : "ac9",
    "name" : "AC9 Phone",
    "brand" : "ACME",
    "type" : "phone",
    "price" : 333,
    "warranty_years" : 0.25,
    "available" : true
}
</pre>

Note: in general because of the automatic line continuation in the shell, you can cut/paste in the above and shouldn't have to type it all out. Just enclose it in the proper statement(s) to get it added.

Next, load into a shell variable the object corresponding to
<pre>
_id : ObjectId("507d95d5719dbef170f15c00")
</pre>

-Then change `term_years` to 3 for that document. (And update it in the database.)
-Then change `over_rate` for sms in limits to 0.01 from 0. Update that too.
At the shell prompt type:

homework.b()
What is the output?
<pre>
//db.products.insert({_id: 'ac9', name: 'AC9 Phone', brand: 'ACME', type: 'phone', price: 333, warranty_years: 0.25, available: true})
//c = db.products.find({_id : ObjectId("507d95d5719dbef170f15c00")})
//c.term_years = 3
//c.limits.sms.over_rate = 0.01
0.050.019031
</pre>

## Homework 2.3
How many products have a voice limit? (That is, have a voice field present in the limits subdocument.)

Input your answer below, (just a number, no other characters).

While you can parse this one by eye, please try to use a query that will do the work of counting it for you.

Just to clarify, the answer should be a number, not a document. There should be no brackets, spaces, quotation marks, etc.

<pre>
//db.products.find({"limits.voice": {$exist: true}}).count()
3
</pre>

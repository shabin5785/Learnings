 

Thursday, August 13, 2015

15:24

 

Create folders..

Create config file

Create log file

Start using mongod --auth --conifg &lt;config file&gt;

Run mongo tool to connect

 

First start with --noauth option. Select admin db and add admin user:

 

> &lt;&lt;mongodb ddls.txt&gt;&gt;

use admin\
db.createUser(\
{\
user: "siteUserAdmin",\
pwd: "password",\
roles: \[ { role: "userAdminAnyDatabase", db: "admin" } \]\
}\
)

 

From
&lt;<http://docs.mongodb.org/manual/tutorial/add-user-administrator/>&gt;

 

-- Grant root privilege as well. This can be done during creation as
well

use admin\
db.grantRolesToUser(\
"admin",\
\[\
{ role: "root", db: "admin" }\
\]

)

 

From
&lt;<http://docs.mongodb.org/manual/tutorial/manage-users-and-roles/>&gt;

 

 

 

Then restart with --auth

Login and try authenicate using db.auth('user'.'pass')

 

 

admin/moz9o

 

 

Tutorial

Tuesday, September 06, 2016

14:49

 

> MongoDB is an open-source document database that provides high
> performance, high availability, and automatic scaling. MongoDB
> obviates the need for an Object Relational Mapping (ORM) to facilitate
> development.
>
>  
>
> Documents
>
> A record in MongoDB is a document, which is a data structure composed
> of field and value pairs. MongoDB documents are similar to JSON
> objects. The values of fields may include other documents, arrays, and
> arrays of documents.
>
> Collections
>
> MongoDB stores documents in collections. Collections are analogous to
> tables in relational databases. Unlike a table, however, a collection
> does not require its documents to have the same schema. In MongoDB,
> documents stored in a collection must have a unique \_id field that
> acts as a [primary
> key](https://docs.mongodb.com/manual/reference/glossary/#term-primary-key)
>
> **Insert**
>
>  
>
> You can use the **insert**() method to add documents to
> a [collection](https://docs.mongodb.com/manual/reference/glossary/#term-collection) in
> MongoDB. If you attempt to add documents to a collection that does not
> exist, MongoDB will create the collection for you.
>
>  
>
> MongoDB provides the following methods for
> inserting [documents](https://docs.mongodb.com/manual/core/document/#bson-document-format) into
> a collection:

-   [db.collection.insertOne()](https://docs.mongodb.com/manual/tutorial/insert-documents/#write-op-insertone)

-   [db.collection.insertMany()](https://docs.mongodb.com/manual/tutorial/insert-documents/#write-op-insertmany)

-   [db.collection.insert()](https://docs.mongodb.com/manual/tutorial/insert-documents/#write-op-insert-method)

>  
>
> **\_id Field**
>
>  
>
> In MongoDB, documents stored in a collection require a unique \_id
> field that acts as a primary key. If the \_id field is unspecified in
> the documents, MongoDB uses ObjectIds as the default value for the
> \_id field; i.e. if a document does not contain a top-level \_id field
> during an insert, the MongoDB driver adds the \_id field that holds an
> ObjectId.
>
>  
>
> In addition, if the mongod receives a document to insert that does not
> contain an \_id field (e.g. through an update operation with an upsert
> option) mongod will add the \_id field that holds an ObjectId.
>
>  
>
>  
>
> [db.collection.insertOne()](https://docs.mongodb.com/manual/reference/method/db.collection.insertOne/#db.collection.insertOne) inserts
> a *single* [document](https://docs.mongodb.com/manual/core/document/#bson-document-format) into
> a collection.
>
>  
>
> [db.collection.insertMany()](https://docs.mongodb.com/manual/reference/method/db.collection.insertMany/#db.collection.insertMany) inserts *multiple* [documents](https://docs.mongodb.com/manual/core/document/#bson-document-format) into
> a collection.
>
>  
>
> db.users.insertMany(\
> \[\
> { name: "bob", age: 42, status: "A", },\
> { name: "ahn", age: 22, status: "A", },\
> { name: "xi", age: 34, status: "D", }\
> \]\
> )
>
>  
>
> [db.collection.insert()](https://docs.mongodb.com/manual/reference/method/db.collection.insert/#db.collection.insert) inserts
> a single document or multiple documents into a collection. To insert a
> single document, pass a document to the method; to insert multiple
> documents, pass an array of documents to the method.
>
>  
>
>  
>
> **Query**
>
>  
>
> You can use the **find**() method to issue a query to retrieve data
> from a collection in MongoDB. All queries in MongoDB have the scope of
> a single collection. Queries can return all documents in a collection
> or only the documents that match a specified filter or criteria. You
> can specify the filter or criteria in a document and pass as a
> parameter to the find() method. The find() method returns query
> results in a cursor, which is an iterable object that yields
> documents.
>
>  
>
> To return all documents in a collection, call the find() method
> without a criteria document : db.restaurants.find()
>
> The query condition for an equality match on a field has the following
> form:
>
> { &lt;field1&gt;: &lt;value1&gt;, &lt;field2&gt;: &lt;value2&gt;, ...
> }\
> If the &lt;field&gt; is a top-level field and not a field in an
> embedded document or an array, you can either enclose the field name
> in quotes or omit the quotes.If the &lt;field&gt; is in an embedded
> document or an array, use [dot
> notation](https://docs.mongodb.com/manual/reference/glossary/#term-dot-notation) to
> access the field. With dot notation, you must enclose the dotted name
> in quotes.
>
>  
>
> db.restaurants.find( { "borough": "Manhattan" } )
>
>  
>
> db.restaurants.find( { "address.zipcode": "10075" } )
>
>  
>
>  

  ------------------------------------------------------------------------------------------------------------------------------------------------
  Greater Than Operator (\$gt),   db.restaurants.find( { "grades.score": { \$gt: 30 } } )
  ------------------------------- ----------------------------------------------------------------------------------------------------------------
  Less Than Operator (\$lt),      db.restaurants.find( { "grades.score": { \$lt: 10 } } )

  Logical AND                     db.restaurants.find( { "cuisine": "Italian", "address.zipcode": "10075" } )

  Logical OR                      db.restaurants.find(
                                  
                                  { \$or: \[ { "cuisine": "Italian" }, { "address.zipcode": "10075" } \] }
                                  
                                  )

  IN                              The following example retrieves all documents from the users collection where status equals either "P" or "D":
                                  
                                   
                                  
                                  db.users.find( { status: { \$in: \[ "P", "D" \] } } )
  ------------------------------------------------------------------------------------------------------------------------------------------------

>  
>
>  
>
> Although you can express this query using
> the [\$or](https://docs.mongodb.com/manual/reference/operator/query/or/#op._S_or) operator,
> use
> the [\$in](https://docs.mongodb.com/manual/reference/operator/query/in/#op._S_in) operator
> rather than
> the [\$or](https://docs.mongodb.com/manual/reference/operator/query/or/#op._S_or)operator
> when performing equality checks on the same field.
>
>  
>
> In the following example, the compound query document selects all
> documents in the collection where the\`\`status\`\`
> equals "A" **and** *either* age is less than than
> ([\$lt](https://docs.mongodb.com/manual/reference/operator/query/lt/#op._S_lt)) 30 *or* type equals 1:
>
> db.users.find(\
> {\
> status: "A",\
> \$or: \[ { age: { \$lt: 30 } }, { type: 1 } \]\
> }\
> )
>
>  
>
> **Exact Match on the Embedded Document**
>
>  
>
> To specify an exact equality match on the whole embedded document, use
> the query document { &lt;field&gt;: &lt;value&gt; } where
> &lt;value&gt; is the document to match. Equality matches on an
> embedded document require an exact match of the specified
> &lt;value&gt;, including the field order.
>
>  
>
> In the following example, the query matches all documents where the
> favorites field is an embedded document that contains only the fields
> artist equal to "Picasso" and food equal to "pizza", in that order:
>
>  
>
> db.users.find( { favorites: { artist: "Picasso", food: "pizza" } } )
>
>  
>
>  
>
> **Equality Match on Fields within an Embedded Document**
>
>  
>
> Use the dot notation to match by specific fields in an embedded
> document. Equality matches for specific fields in an embedded document
> will select documents in the collection where the embedded document
> contains the specified fields with the specified values. The embedded
> document can contain additional fields.
>
>  
>
> In the following example, the query uses the dot notation to match all
> documents where the favorites field is an embedded document that
> includes the field artist equal to "Picasso" and may contain other
> fields:
>
>  
>
> db.users.find( { "favorites.artist": "Picasso" } )
>
>  
>
> **Exact Match on an Array**
>
>  
>
> To specify equality match on an array, use the query document {
> &lt;field&gt;: &lt;value&gt; } where &lt;value&gt; is the array to
> match. Equality matches on the array require that the array field
> match exactly the specified &lt;value&gt;, including the element
> order.
>
>  
>
> The following example queries for all documents where the field badges
> is an array that holds exactly two elements, "blue", and "black", in
> this order:
>
>  
>
> db.users.find( { badges: \[ "blue", "black" \] } )
>
>  
>
>  
>
> **Match an Array Element**
>
>  
>
> Equality matches can specify a single element in the array to match.
> These specifications match if the array contains at least one element
> with the specified value.
>
>  
>
> The following example queries for all documents where badges is an
> array that contains "black" as one of its elements:
>
>  
>
> db.users.find( { badges: "black" } )
>
>  
>
>  
>
> **Match a Specific Element of an Array**
>
>  
>
> Equality matches can specify equality matches for an element at a
> particular index or position of the array using the dot notation.
>
>  
>
> In the following example, the query uses the dot notation to match all
> documents where the badges is an array that contains "black" as the
> first element:
>
>  
>
> db.users.find( { "badges.0": "black" } )
>
>  
>
>  
>
> **Single Element Satisfies the Criteria**
>
>  
>
> Use \$elemMatch operator to specify multiple criteria on the elements
> of an array such that at least one array element satisfies all the
> specified criteria.
>
>  
>
> The following example queries for documents where the finished array
> contains at least one element that is greater than (\$gt) 15 and less
> than (\$lt) 20:
>
>  
>
> db.users.find( { finished: { \$elemMatch: { \$gt: 15, \$lt: 20 } } } )
>
>  
>
>  
>
> **Combination of Elements Satisfies the Criteria**
>
>  
>
> The following example queries for documents where the finished array
> contains elements that in some combination satisfy the query
> conditions; e.g., one element can satisfy the greater than 15
> condition and another element can satisfy the less than 20 condition,
> or a single element can satisfy both:
>
>  
>
> db.users.find( { finished: { \$gt: 15, \$lt: 20 } } )
>
>  
>
>  
>
> **Match a Field in the Embedded Document Using the Array Index**
>
>  
>
> If you know the array index of the embedded document, you can specify
> the document using the embedded document’s position using the dot
> notation.
>
>  
>
> The following example selects all documents where the points contains
> an array whose first element (i.e. index is 0) is a document that
> contains the field points whose value is less than or equal to 55:
>
>  
>
> db.users.find( { 'points.0.points': { \$lte: 55 } } )
>
>  
>
>  
>
> **Match a Field Without Specifying Array Index**
>
>  
>
> If you do not know the index position of the document in the array,
> concatenate the name of the field that contains the array, with a dot
> (.) and the name of the field in the embedded document.
>
>  
>
> The following example selects all documents where the points is an
> array with at least one embedded document that contains the field
> points whose value is less than or equal to 55:
>
>  
>
> db.users.find( { 'points.points': { \$lte: 55 } } )
>
>  
>
>  
>
> **Single Element Satisfies the Criteria**
>
>  
>
> Use \$elemMatch operator to specify multiple criteria on an array of
> embedded documents such that at least one embedded document satisfies
> all the specified criteria.
>
>  
>
> The following example queries for documents where the points array has
> at least one embedded document that contains both the field points
> less than or equal to 70 and the field bonus equal to 20:
>
>  
>
> db.users.find( { points: { \$elemMatch: { points: { \$lte: 70 },
> bonus: 20 } } } )
>
>  
>
> **Combination of Elements Satisfies the Criteria**
>
>  
>
> The following example queries for documents where the points array
> contains elements that in some combination satisfy the query
> conditions; e.g. one element satisfies the points less than or equal
> to 70 condition and another element satisfies the bonus equal to 20
> condition, or a single element satisfies both criteria:
>
>  
>
> db.users.find( { "points.points": { \$lte: 70 }, "points.bonus": 20 }
> )
>
>  
>
>  
>
> Projection Document
>
> By default, queries in MongoDB return all fields in matching
> documents. To limit the amount of data that MongoDB sends to
> applications, you can include a projection document in the query
> operation.
>
>  
>
> The projection document limits the fields to return for all matching
> documents. The projection document can specify the inclusion of fields
> or the exclusion of field and has the following form:
>
> { field1: &lt;value&gt;, field2: &lt;value&gt; ... }
>
> The &lt;value&gt; can be any of the following:

-   1 or true to include the field in the return documents.

-   0 or false to exclude the field.

-   Expression using a [Projection
    > Operators](https://docs.mongodb.com/manual/reference/operator/projection/).

>  
>
> For the \_id field, you do not have to explicitly specify \_id: 1 to
> return the \_id field. The db.collection.find() method always returns
> the \_id field unless you specify \_id: 0 to suppress the field. A
> projection cannot contain both include and exclude specifications,
> except for the exclusion of the \_id field. In projections that
> explicitly include fields, the \_id field is the only field that you
> can explicitly exclude.
>
>  
>
> A projection can explicitly include several fields. In the following
> operation,
> the [db.collection.find()](https://docs.mongodb.com/manual/reference/method/db.collection.find/#db.collection.find)method
> returns all documents that match the query. In the result set, only
> the name, status and, by default, the \_id fields return in the
> matching documents.
>
> db.users.find( { status: "A" }, { name: 1, status: 1 } )
>
>  
>
>  
>
> Use the [dot
> notation](https://docs.mongodb.com/manual/core/document/#document-dot-notation) to
> return specific fields in an embedded document.
>
> The following example specifies a projection to return:
> the \_id field, name field, status field, and the foodfield inside
> the favorites document; the food field remains embedded in
> the favorites document.
>
> db.users.find(\
> { status: "A" },\
> { name: 1, status: 1, "favorites.food": 1 }\
> )
>
>  
>
>  

-   The { name : null } query matches documents that either contain
    > the name field whose value is null*or* that do not
    > contain the name field.

-   The { name : { \$type: 10 } } query matches documents that contains
    > the name field whose value is null only; i.e. the value of the
    > item field is of BSON Type Null (i.e. 10) :

-   The { name : { \$exists: false } } query matches documents that do
    > not contain the item field:

>  
>
>  
>
>  
>
>  
>
>  
>
>  
>
> **Sort**
>
>  
>
> To specify an order for the result set, append the sort() method to
> the query. Pass to sort() method a document which contains the
> field(s) to sort by and the corresponding sort type, e.g. 1 for
> ascending and -1 for descending.
>
>  
>
> db.restaurants.find().sort( { "borough": 1, "address.zipcode": 1 } )
>
>  
>
>  
>
> **Update**
>
> You can use the update() method to update documents of a collection.
> The method accepts as its parameters:

-   a filter document to match the documents to update,

-   an update document to specify the modification to perform, and

-   an options parameter (optional).

>  
>
> By default, the update() method updates a single document. Use the
> multi option to update all documents that match the criteria. You
> cannot update the \_id field.
>
>  
>
> **Update Top-Level Fields**
>
>  
>
> db.restaurants.update(\
> { "name" : "Juni" },\
> {\
> \$set: { "cuisine": "American (New)" },\
> \$currentDate: { "lastModified": **true** }\
> }\
> )
>
>  
>
> Update multi:
>
>  
>
> db.restaurants.update(\
> { "address.zipcode": "10016", cuisine: "Other" },\
> {\
> \$set: { cuisine: "Category To Be Determined" },\
> \$currentDate: { "lastModified": **true** }\
> },\
> { multi: **true**}\
> )
>
>  
>
> To replace the entire document except for the \_id field, pass an
> entirely new document as the second argument to the update() method.
> The replacement document can have different fields from the original
> document. In the replacement document, you can omit the \_id field
> since the \_id field is immutable. If you do include the \_id field,
> it must be the same value as the existing value.
>
>  
>
> If no document matches the update condition, the default behavior of
> the update method is to do nothing. By specifying the upsert option to
> true, the update operation either updates matching document(s) or
> inserts a new document if no matching document exists. In the MongoDB
> Manual, see update().
>
>  
>
> In MongoDB, write operations are atomic on the level of a single
> document. If a single update operation modifies multiple documents of
> a collection, the operation can interleave with other write operations
> on that collection.
>
>  
>
> MongoDB provides the following methods for updating documents in a
> collection:

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  [db.collection.updateOne()](https://docs.mongodb.com/manual/reference/method/db.collection.updateOne/#db.collection.updateOne)      Updates at most a single document that match a specified filter even though multiple documents may match the specified filter.
                                                                                                                                      
                                                                                                                                      *New in version 3.2.*
  ----------------------------------------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  [db.collection.updateMany()](https://docs.mongodb.com/manual/reference/method/db.collection.updateMany/#db.collection.updateMany)   Update all documents that match a specified filter.
                                                                                                                                      
                                                                                                                                      *New in version 3.2.*

  [db.collection.replaceOne()](https://docs.mongodb.com/manual/reference/method/db.collection.replaceOne/#db.collection.replaceOne)   Replaces at most a single document that match a specified filter even though multiple documents may match the specified filter.
                                                                                                                                      
                                                                                                                                      *New in version 3.2.*

  [db.collection.update()](https://docs.mongodb.com/manual/reference/method/db.collection.update/#db.collection.update)               Either updates or replaces a single document that match a specified filter or updates all documents that match a specified filter.
                                                                                                                                      
                                                                                                                                      By default, the [db.collection.update()](https://docs.mongodb.com/manual/reference/method/db.collection.update/#db.collection.update) method updates a **single**document. To update multiple documents, use the [multi](https://docs.mongodb.com/manual/reference/method/db.collection.update/#multi-parameter) option.
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

>  
>
>  
>
>  
>
>  
>
> **Remove**
>
>  
>
> You can use the remove() method to remove documents from a collection.
> The method takes a conditions document that determines the documents
> to remove.
>
>  
>
> db.restaurants.remove( { "borough": "Manhattan" } )
>
>  
>
>  
>
> By default, the remove() method removes all documents that match the
> remove condition. Use the justOne option to limit the remove operation
> to only one of the matching documents.
>
>  
>
> db.restaurants.remove( { "borough": "Queens" }, { justOne: **true** }
> )
>
>  
>
> To remove all documents from a collection, pass an empty conditions
> document {} to the remove()method.
>
>  
>
>  
>
> The remove all operation only removes the documents from the
> collection. The collection itself, as well as any indexes for the
> collection, remain. To remove all documents from a collection, it may
> be more efficient to drop the entire collection, including the
> indexes, and then recreate the collection and rebuild the indexes. Use
> the drop() method to drop a collection, including any indexes.
>
>  
>
> db.restaurants.drop()
>
>  
>
>  
>
> **Bulk Write Operations**
>
>  
>
> Bulk write operations can be either ordered or unordered.
>
>  
>
> With an ordered list of operations, MongoDB executes the operations
> serially. If an error occurs during the processing of one of the write
> operations, MongoDB will return without processing any remaining write
> operations in the list.
>
>  
>
> With an unordered list of operations, MongoDB can execute the
> operations in parallel, but this behavior is not guaranteed. If an
> error occurs during the processing of one of the write operations,
> MongoDB will continue to process remaining write operations in the
> list.
>
>  
>
> Executing an ordered list of operations on a sharded collection will
> generally be slower than executing an unordered list since with an
> ordered list, each operation must wait for the previous operation to
> finish.
>
>  
>
> By default, bulkWrite() performs ordered operations. To specify
> unordered write operations, set ordered : false in the options
> document.
>
>  
>
> [bulkWrite()](https://docs.mongodb.com/manual/reference/method/db.collection.bulkWrite/#db.collection.bulkWrite) supports
> the following write operations:

-   [insertOne](https://docs.mongodb.com/manual/reference/method/db.collection.bulkWrite/#bulkwrite-write-operations-insertone)

-   [updateOne](https://docs.mongodb.com/manual/reference/method/db.collection.bulkWrite/#bulkwrite-write-operations-updateonemany)

-   [updateMany](https://docs.mongodb.com/manual/reference/method/db.collection.bulkWrite/#bulkwrite-write-operations-updateonemany)

-   [replaceOne](https://docs.mongodb.com/manual/reference/method/db.collection.bulkWrite/#bulkwrite-write-operations-replaceone)

-   [deleteOne](https://docs.mongodb.com/manual/reference/method/db.collection.bulkWrite/#bulkwrite-write-operations-deleteonemany)

-   [deleteMany](https://docs.mongodb.com/manual/reference/method/db.collection.bulkWrite/#bulkwrite-write-operations-deleteonemany)

>  
>
>  
>
>  
>
>  
>
> **Data Aggregation **
>
>  
>
> MongoDB can perform aggregation operations, such as grouping by a
> specified key and evaluating a total or a count for each distinct
> group.
>
> Use the aggregate() method to perform a stage-based aggregation. The
> aggregate() method accepts as its argument an array of stages, where
> each stage, processed sequentially, describes a data processing step.
>
>  
>
> Use the \$group stage to group by a specified key. In the \$group
> stage, specify the group by key in the \_id field. \$group accesses
> fields by the field path, which is the field name prefixed by a dollar
> sign \$. The \$group stage can use accumulators to perform
> calculations for each group
>
>  
>
> The following example groups the documents in
> the restaurants collection by the borough field and uses
> the \$sumaccumulator to count the documents for each group.
>
> db.restaurants.aggregate(\
> \[\
> { \$group: { "\_id": "\$borough", "count": { \$sum: 1 } } }\
> \]\
> );
>
>  
>
> Use the \$match stage to filter documents. \$match uses the MongoDB
> query syntax. The following pipeline uses \$match to query the
> restaurants collection for documents with borough equal to "Queens"
> and cuisine equal to Brazilian. Then the \$group stage groups the
> matching documents by the address.zipcode field and uses the \$sum
> accumulator to calculate the count. \$group accesses fields by the
> field path, which is the field name prefixed by a dollar sign \$.
>
>  
>
> db.restaurants.aggregate(\
> \[\
> { \$match: { "borough": "Queens", "cuisine": "Brazilian" } },\
> { \$group: { "\_id": "\$address.zipcode" , "count": { \$sum: 1 } } }\
> \]\
> );
>
>  
>
>  
>
> **Indexes **
>
>  
>
> Indexes can support the efficient execution of queries. Without
> indexes, MongoDB must perform a collection scan, i.e. scan every
> document in a collection, to select those documents that match the
> query statement. If an appropriate index exists for a query, MongoDB
> can use the index to limit the number of documents it must inspect.
>
>  
>
> Use the createIndex() method to create an index on a collection.
> Indexes can support the efficient execution of queries. MongoDB
> automatically creates an index on the \_id field upon the creation of
> a collection.
>
>  
>
> To create an index on a field or fields, pass to the createIndex()
> method an index key specification document that lists the fields to
> index and the index type for each field:
>
>  
>
> { &lt;field1&gt;: &lt;type1&gt;, ...}
>
>  

-   For an ascending index type, specify 1 for &lt;type&gt;.

-   For a descending index type, specify -1 for &lt;type&gt;.

>  
>
> createIndex() only creates an index if the index does not exist.
>
>  
>
> Create an ascending index on the "cuisine" field of
> the restaurants collection.
>
> db.restaurants.createIndex( { "cuisine": 1 } )
>
> MongoDB supports [compound
> indexes](https://docs.mongodb.com/manual/core/index-compound/#index-type-compound) which
> are indexes on multiple fields. The order of the fields determine how
> the index stores its keys. For example, the following operation
> creates a compound index on the "cuisine" field and
> the "address.zipcode" field. The index orders its entries first by
> ascending"cuisine" values, and then, within each "cuisine", by
> descending "address.zipcode" values.
>
> db.restaurants.createIndex( { "cuisine": 1, "address.zipcode": -1 } )
>
>  
>
>  
>
>  
>
>  
>
>  

 

 

Mongo University Course

Tuesday, September 06, 2016

16:53

-   Mongd is the process started for the database. Mongo.exe from our
    > machine connects to db through tcp

>  

-   Mongo supports transctions in single document. That operations
    > are atomic. Txns across documents is not supported.

>  

-   From console to edit a document..

> Var j = db.users.find({name:'s'})
>
> j.color = 'red';
>
> Db.users.save(j);
>
>  

-   Json has only arrays and dictionaries within that. Only these two
    > are possible :( \[\] and {} )

>  

-   Document cannot be more than 16MB

>  

-   Create =&gt; Insert , Update =&gt; Update , Read =&gt; Find , Delete
    > =&gt; Remove

>  

-   All mongo db operations exist as functions in language. There is no
    > sql statements to be used in mongo db

>  

-   Mongodb uses a wire protocol to send data over network

>  

-   Mongo shell is an interactive javascript shelll that can connecct to
    > mongo db. So can write js statements in the shell..:)

>  

-   Tab auto completes in the shell

>  

-   Mongdb uses a binary representation (BSON ) for storing
    > data internally. BSON supports more data types than json. We can
    > use js fns from shell (constructors ) or similar data types in
    > languages like java to insert these types of mongo..(ie not
    > supported by json)

>  

-   Db.find returns all docs. Docs are returned in batches. Default
    > of 20. enter it to view next batch. The cursor is kept open for
    > only 10 mins in server side.to save resources.

>  

-   If a field has string and number values, then a comparison of it is
    > lexographically correct.. Will compare either strings or numbers
    > as per query. Not both of them.

>  

-   Comparisons are case sensitive.

>  

-   \$exist =&gt; check for presence, \$type =&gt; check for field type
    > (but types are given as bson number representation of type)

>  

-   Score:{\$lt:50},score:{\$gt:40 } =&gt; wont find docs between 50 and
    > 40, cause, js parser replaces score lt 50 with score gt 40 and so
    > docs gt 40 is returned. For the and effect we need to combine lt
    > and gt in one doc. Like score:{\$lt:50 , \$gt:40}

>  

-   Db.user.find({a:"new"}) =&gt; will check new inside an array a as
    > well a string a. ie query is polymorphic.

>  

-   No recursion for finding values. Will check only specified fields.
    > In above example, a will not be checked in a doc with a doc unless
    > we use dot notation. An exception is checking inside top
    > level arrays.

>  

-   \$all =&gt; takes an array of values and returns doc with all those
    > values in an array. Order of values in query is not important

>  

-   \$in takes an array and returns doc with fields having any of
    > these values. Fields can be array or any fields

>  

-   C = db.a.find();null; here c is a cursor variable. Also appending
    > null is to prevent printing the results till we need it.

>  

-   Cursor operations can be chained. Like c.sort.limit

>  

-   Cursor options should be set before querying db.

>  
>
>  
>
>  
>
> ----------------------------------------------
>
>  
>
> mongoimport -d students -c grades &lt; grades.json
>
> mongoimport --db population --collection zips --file zips.json
>
>  
>
> update command with a doc as second argument will replace the matched
> document but with same id.
>
>  
>
> use \$set to update a field.also \$inc can increase the field value.
> if the field in \$inc is not present, then a new field will be created
> with value as the increment step given
>
>  
>
> \$unset to remove field. can give any value for unset.. mongo infact
> ignores it. value needed for correct doc syntax
>
>  
>
> \$set can be used to edit single element in array. like \$set ("a.2")
> to change third element in array a
>
>  
>
> update has push and pop to add and remove elements from an array
>
>  
>
> pop:1 removes right most element and pop:-1 removes left most element
>
>  
>
> pushall is used to add multiple elements to an array. pushall
> :{a:\[2,3\]}
>
>  
>
> pull will remove the element by value. so we can remove any element.
>
>  
>
> pullAll removes multiple elements by value
>
>  
>
> addtoset in an array adds element if it doesnt exist. else it acts
> like push
>
>  
>
> {upsert:true}: passed as third arg to update, will create doc it
> doesnt exist. upsert will leave out fields without concrete value,
> like giving a greater than query as update arg
>
>  
>
> to use updateall, give an empty query,just like find. But even with an
> empty query, update affects only one doc. Need to set {multi:true} to
> affect multiple docs. Infact empty query wihtout multi true will
> affect some random doc. Which doc is not specified.
>
>  
>
> mongo operations run in a thread. But writes to multipe docs are not
> transctin bounded. They occasinaly yield to other operations. So a 10
> doc insert or update might yield in between and so reads between them
> can be stale data. BUt a single doc update is guarnateed to be atomic
>
>  
>
> remove to delete docs. empty arg removes all docs. multi remove are
> not isolated transactions. same as the write above . single doc
> removal is atomic
>
>  
>
> drop to delete collections. Its faster than remove all
>
>  
>
> one to one relation: choose embed or link based on how frequent docs
> are accessed, size of docs, requirement for atomicity etc
>
>  
>
> One to many: If many side is large, we have to go for linking due to
> size limit. But if many side is few, we can do embedding
>
>  
>
> Many to many: Link if too large. Else if few to few can be
> embedded.but prefer linking here
>
>  
>
> add index to columns for one that we need to be quried.
>
>  
>
> append explain() to end of query for details of query execution
>
>  
>
> java driver, mongodb object is immutable. So once created, we need to
> create new to reconfigure
>
>  
>
> we can remove id field added by mongo to a document. Then add the same
> doc means new id will be generated
>
>  
>
> projection: with a query like x=a, the result docs will all have the x
> field. But as we know that x will be a, we can omit x field. For that
> we use a projection, passing x=0 to omit x from output. This is the
> select concept of choosing columns during querying. We can pass value
> 1 to select columns and 0 to omit. id is always selcted unless we give
> 0
>
>  
>
> for full doc replacement ids of new and old have to match
>
>  
>
> benefits of embedding: Improved read perf. Data is located nearby in
> disks. This causes faster access. Also with embedding we can avoid
> round trips to the database.
>
>  
>
> for tree relationship ( like ecommerce prod category hierarchy), its
> better to store all ancestors of a category in an array and link prod
> to that category.
>
>  
>
> Object Document Mapper : Concept similar to hibernate orm (Morphia for
> mongo. anything else?)
>
>  
>
> Morphia iterators can be re used after calling fetch again
>
>  
>
> Morphia quries can take java field name or doc field name
>
>  
>
> Storage engine is between the mongodb process and the disk storage.
> Storage Engine (SE) decides how to store data to disk. SE decides what
> to store in memory, write to disk etc.mongo 3.0 has pluggable SE
>
>  
>
> There are two major SE: MMAP and WiredTiger. 3.2 onwards its
> WiredTiger by default
>
>  
>
> MMAP: Original SE of Mongo. It uses mmap system call in backend. Any
> unix machine has mmap call.mmap uses the os to decide what to keep in
> memory and in disk. So we/db have little control. Mmap allocates space
> by nearest power of 2 to avoid too much moving aroud. So 3 bytes is 4
> bytes alloted. 9 is 16 and so on. It has collection level sorting
>
>  
>
> minimum alloted space in mongo 3.0 is 32 bytes
>
>  
>
>  
>
> WiredTiger: it has doc level concurrency. Not locking. its lock free
> and optimistic. its also offers compression of data and index. WT
> itself manages the memory, whihch to keep in memory and which to disk.
> So we can keep data uncompressed in memory and before write compress
> and write
>
> its an append only SE, no inplace updates. the doc updated is marked
> as not used, a new doc is written and old one is later reclaimed. This
> can cause too many writes if we continously update a large doc. But
> this is needed for doc level concurrency
>
>  
>
>  
>
> db.&lt;collname&gt;.stats() : info abt colelction
>
>  
>
> indexs are constructed as Btree in mongo (mmap). WT uses b+tree
>
>  
>
> consider an index of (a,b,c): indexs are stores like a1b1c1 , a2b2c2
> etc. So we can use btree to find a query with a and b and c. But
> querying with just b will be slow as btree cannot be used. Same for c.
> So we have stick to left most rule. Either abc or ab or a like that.
> For sorting the order of sort should be same as index or the reverse
> of index .. this is needed for tree walk
>
>  
>
> index slows down write and speeds up reads. But this is give and take.
> Find and updates will be faster,same for reads, find and replace etc.
> though writes will be slower. Decide based on data and usage.
>
>  
>
> pass true to explain query to run the query and see the stats as well
>
>  
>
> while creating indexs we can specify the sort order, asc or desc. This
> can affect teh queries that sort data based on a query on index
>
>  
>
> getindexes command to fetch indexes.
>
>  
>
> can create index of arrays. arra :\[b,n,m\] creates indexes on b,n and
> m . They are known as multi key indexes
>
> {color:red, arr:\[n.b.m\]}
>
> here index on arr and color will create indexes on n:red, b:red
> etc                 
>
>  
>
> u cannot have multi index with all of them arrays. only one can be an
> array. If allowed this cause a lot of indexes.
>
>  
>
> While createing docs, data is not there.. only field . like above arr.
> When we add a doc and give value to arr, and if its an array, index
> becomes multi key. Check multi key
>
>  
>
> We can create index on sub docs as well.        
>
>  
>
> \$elemmatch to check a single field in an array
>
>  
>
> sparse indexes that can be used when docs miss the index field. For
> missing field if only one doc has a missing field, index works. BUt
> multiple docs, results in multipe fields with null. So we can give
> sparse option telling db not to index docs with missing fields. No
> idea waht is the advantage
>
>  
>
> index createion in foreground, blocks reads and writes. we can use
> background createion
>
>  
>
> another strategey in a cluster of servers, is to take one offline
> create index and put back and then repeat.                
>
>  
>
>  
>
> db.coll.explain() retursn an explainable object. We can reuse that.
>
>  
>
> old format of explain (whihc still works) db.coll.find.explain works
> on methods that return a cursor. So it wont work on count, remove etc
>
>  
>
> pass executionstats to explain() to get details of time taken, doc
> examined etc..
>
>  
>
> pass allplanexectuionstats to get details of rejected plans as well.
>
>  
>
> rejection works like this: compare different plans and the moment one
> plan is costlier than other reject it. for eg: plan a takes 100 scans
> and b takes 500, moment b reaches 101 its rejected..
>
>  
>
>  
>
> covered quries are thoes that can be satisfied from index alone. So no
> doc needs to be scanned
>
>  
>
> if we have an index on i and j , we have two indexes . one for \_id
> and one for i,j. If we query with i,j and we get 20 docs, 20 keys were
> examined.BUt it also examined 20 docs, as we asked for id and its not
> part of used index. So for a complete covered query, we need to avoid
> the fields not in index.                  
>
>  
>
> now if we omit only id, then mongo again need to scan all docs to
> ensure that any other fields are present. So for complete covered
> query, we need to project exactly wat we want. here i:1, j:1 and
> \_id:0
>
>  
>
>  
>
> if we have multiple indexes, the query will take the index with fields
> in for clause. Now if we project we need fields in another index, it
> not going to use second index on returned docs frmo first index query.
> It will be a scan and so nto a covered query.        
>
>  
>
>  
>
> mongodb caches winning query plans for some time to be used later. the
> deletion form cache can happen with a lot of writes, change of index
> etc        
>
>  
>
> indexes shld be in memory. As pulling it from disk is a waste.So we
> need to consider the memory and size of index and make sure index fits
> in memory. Run stats command on collection to get index size along
> with other details. Also can run the totalIndexSize to get the
> details..With wiredTiger we can enable index compression
>
>  
>
>  
>
> no of index points: regular index its 1:1, sparse its less than no of
> docs (no for null) and multi key its more than no of docs,. So when a
> doc moves , may be due to size change, index points needs to be
> updated. This is for MMAp. In the WiredTiger storage engine, index
> entries don't contain pointers to actual disk locations. Instead, in
> WiredTiger, the index points to an internal document identifier (the
> RecordId) that is immutable. Therefore, when a document is updated,
> its index does not need to be updated at all.        
>
>  
>
> create index with type 2d, and can use near operator to query. Special
> purpose.         for that we need field with location valus(loc and
> lat), 2d.
>
> db.places.find( { location : { \$near : \[74,140\] } }).limit(3)
>
> find 3 places near give loca. WHere location is the field having hte
> values
>
>  
>
> also geo spatial for 3d.. check videos saved.
>
>  
>
>  
>
> text search: For this to work entire text needed to be searched. Else
> a tedious way is to put each word in an array and serach.or use regex.
>          mongo has a text index to solve this problem
>
> db.coll.ensureindex({'fieldname':'text'}) create text index
>
> db.coll.find({\$text:{\$search:'word'}}) to serach above created
> index. where word can be part of a document
>
> we can use \$score and \$meta to find the match level and get exact
> match
>
>  
>
>  
>
> index selection : minimize doc sacnned, how sorts are handled        
>
>  
>
> in sort in executionstat output shows that mongo was not able to sort
> data in db and had to do a memory sort. So this may be rejected as
> another one can return sorted data from db         , in memory sort is
> generally to be avoided
>
>  
>
> can use hint fn to ask mongo to use a particular index. use with
> caution of overiding the index use
>
>  
>
> so major idea in choosign an index is selectivity of index.
> Selectivity is the primary factor that determines how efficiently an
> index can be used. Ideally, the index enables us to select only those
> records required to complete the result set, without the need to scan
> a substantially larger number of index keys (or documents) in order to
> complete the query. Selectivity determines how many records any
> subsequent operations must work with. Fewer records means less
> execution time.
>
>  
>
> mongo automatically logs the slow quries that take over 100ms into the
> log
>
>  
>
> profiler writes to db.system.profile the slow queries. We can run a
> find to get data. it has three levels 0 is off, 1 is slow quries and 2
> is
>
> all queries. Need to start profile while starting mongod
>
> db.getProfilingstatus to get current status
>
> db.setprofilelevel(1,4) . first is level and second is slower time
> here 4 ms        
>
> db.system.profile.find({millis:{\$gt:1000}}).sort({ts:-1}) : find
> slower than 1s query and sort by timestmap
>
>  
>
> mongostat command will sample db in 1sec and give output about insert
> update etc. Its similar to iostat
>
>  
>
> mongotop is similar to top
>
>  
>
> sharding: for sharding we hav multiple servers running mongod and a
> mongo server (mongos) on top of that. MOngos is waht our application
> connect to. Each mongod can be a cluster of servers like a replica
> set. Different mongod are shards here. First we need to choose a shard
> key. mongos routes request based on shard key
>
> insert must include a shard key (entire in case of multi key).
>
> update,remove,find without a shardkey, mongos will broadcast to all
> shards for data.So better perf with specifying hte shard key
>
>  
>
> mongos is usually on same machine as application and can have multiple
> instances
>
> below is same as sql for finding no of prods per manufacture..
>
> db.coll.aggregate : for aggregation
>
> (\[
>
> \$group: //group by. We ar effectively creating a new collection with
> aggregation results
>
>  
>
> {
>
> \_id :"\$manufacturer", //manufacturer name group by. here we are
> referring one of the fields in the document
>
> num\_prod : {\$sum:1} //also find the no of each manufactures
>
> }
>
> \])
>
>  
>
> above id can be written as
>
> \_id:{
>
> "manu":"\$manufacturer"
>
> }
>
> this creates an id as doc. Its easier to read. than just having \_id.
> We can name as we want
>
> aggregation query is an array.. note..
>
>  
>
>  
>
> agg uses a pipe line .. similar to unix pipe line. Docs are piped thru
> hte pipe line. the pipe line is given as elements in the array.
>
> \$project pipe line stage: its going to reshape..selcet some fieds
> (from inner doc and bring to front as well). So one doc comes in one
> goes out.. 1:1 relation.
>
>  
>
> \$match: filtering step.so its n:1
>
>  
>
> \$group: allows aggregate: inside we can use sum, count etc which will
> group together docs. so n:1
>
>  
>
> \$sort: 1:1
>
>  
>
> \$skip : skips docs (like skip first 20 docs): so n:1
>
>  
>
> \$limit: n:1
>
>  
>
> \$unwind: wen we have to flatten data.. like an array. for eg:
> tags\[r,b,n\] to tags:r, tags:b, tags:n. so its 1:n stage. this helps
> in aggregation.
>
>  
>
> \$out: redirect docs to another colleciton.1:1
>
>  
>
> \$redact and \$geonear:
>
>  
>
>  
>
> the above query explained:
>
> mongo takes each doc. Output we wanted has an id equal to manufactur.
> So mongo checks if a doc exits with id same the current doc.if no
> create a new one in output section. It also creates a num\_prod key.
> Then its asks to add 1 (sum:1). This process is repeated.
>
>  
>
> compound grouping: like gruop by manufacture and category. So we give
> a combined \_id in gruop by. Rest is same as above
>
> \_id:{
>
> "manu":"\$manufacturer",
>
> "cat": "\$category"
>
> }
>
> we are createing a new combined key for the doc in the aggregation.
>
>  
>
>  
>
> note: we can have a document as \_id in mongodb. Not jsut a sinlge
> value. Only requirement is to be that \_id is to be unique. So the doc
> used shold be uniqe
>
>  
>
> expressions:
>
> \$sum, \$avg, \$min, \$max (all word on aggregated docs), \$push and
> \$addtoset (works on arrays)
>
> \$first and \$last ( requires us to sort). These find find or last
> values for a key in aggregation output
>
>  
>
> \$sum: \$sum:1 will add one. To add field values we use it like
>
> sum\_prices :{\$sum: "\$price"}, where price is the field name having
> prices
>
>  
>
> \$avg: same as sum. replace \$sum with \$avg
>
>  
>
> \$addToSet: more like for each doc, and id we specify , add the value
> we tell to a set . So we can find the unique set of elements.
>
> (\[
>
> \$group:
>
>  
>
> {
>
> \_id :"\$manufacturer",
>
> categoryset : {\$addToSet:"\$category"} //find unique category values
> for the manufactures
>
> }
>
> \])
>
>  
>
>  
>
> \$push: same as addtoset, but does not guantee uniquenes of a set.so
> cna have duplicates. So if we run this and above query on an unique
> field (say like id,) then the result will be same
>
>  
>
>  
>
> \$max and \$min: max find the max of the values. like the sum of a
> field values, max finds the max values from that field values. Min
> does the reverse
>
>  
>
> db.zips.aggregate(\[{\$group:{\_id:"\$state","pop":{\$max:"\$pop"}}}\]);
>
>  
>
> above query,first find groupd docs by state. Now a state can have
> multiple zips within it. We can sum hte pop within all docs having
> same state or find the max or min as shown above.
>
>  
>
> we can aggregate more than once in a query
>
> assume students in a class having scores. We need to find average
> scores per class.
>
> So first we average for each class and student, and then on the result
> we average over the class in the first result
>
> db.grades.aggregate(\[
>
> {\$group:{\_id:{c\_id:"\$class\_id",s\_id:"\$student\_id},average:{\$avg:"\#score"}}},
>
> {\$group:{\_id:"\$\_id.c\_id",aver:{\$avg:"\$average"}}}
>
> \])
>
>  
>
> we cant jus average over entire class, as different students have
> different no of scores. Special cases like this its useful
>
>  
>
> \$project: we can do like remove , add , re shape keys etc. also do
> uppercase, lowercase changes etc. Also add , divide etc on values etc
>
> {
>
> \$project:{
>
> \_id:0, //if we dont want id in docs
>
> 'mak':{\$tolower:'manufacturer'}, //change manufacture value to lower
> case
>
> 'det':{'category':'\$category','price':{\$multiply:{'\$price',10}}},
> //create sub doc with category and price multipled by 10
>
> 'item':'\$name'
>
> }
>
> }
>
> original fields are not included after this. we dont need to explicity
> omit fields other than id. If we want to include the key from original
> , we shld wirte key:1 id is includede by default.
>
> db.zips.aggregate(\[{'\$project':{\_id:0,'city':{'\$toLower':'\$city'},'pop':1,'state':1,'zip':'\$\_id'}}\])
>
>  
>
> \$match: does filtering. goes to each doc. matches and if true, pushes
> to next stage.
>
> {
>
> \$match:{
>
> state:'CA' //only aggregate values in state CA
>
> }
>
>  
>
>  
>
> }
>
>  
>
> we link another stage after this to aggreage data only from CA
>
>  
>
> \$sort:agg supports memoery and disk sorting. by default its memory.
> there is a limit of 100MB per stage. So if we dont use disk based sort
> for latege data, we are in trouble. we can sort before and after
> grouping
>
> \$sort:{'field':1}
>
>  
>
>  
>
> \$limit and \$skip :
>
> \$skip:10
>
> \$limit:4
>
>  
>
> \$first and \$last:
>
> a 0 b 4
>
> a 0 b 7
>
> a1 b 6
>
> a1 b 5
>
>  
>
> sort by a,b
>
> then group by a.
>
> first of b then gives first of each group : 4 and 5
>
> same for last
>
> example like largest city in every state. So sort, group by state and
> take first.
>
>  
>
> we use \$ operator wen keys or fields are on right side
>
>  
>
> first and last are run inside \$group
>
> \$group:{
>
> city:{\$first:'field from above'}
>
> popluation:{\$first: 'field from above'}
>
> }
>
>  
>
> here first gives the first above from above stage and we take values
> from that
>
>  
>
> \$unwind: to make it easy to group, we faltten the array. un wind on a
> doc with array creates new docs with old data minus array and each
> element of array. so if array has 3 elemsn. 3 new docs will be created
>
>  
>
> so if we have 5 docs, each with an array of 4, we get 20 new docs
> after unwind
>
> \$unwind: 'field name'
>
>  
>
> we can reverse unwind using push operator. addotset works if array had
> only unique fields initially
>
>  
>
> if we have two arrays, we can unwind on both.Creates cartesian prod of
> two arrays size docs
>
> \$unwind:a
>
> \$unwind:b                  
>
>  
>
> so array a of 3 , b of 5 adn we have 4 docs.
>
> total = 4\*3 = 12 \* 5 = 60
>
>  
>
> again we can reverse using two push statements
>
>  
>
> sql to aggregation framework chart has mapping between sql and mongo
>
>  
>
> while writing group by, we can have \_id:null to have only the
> aggregatin result in output
>
>  
>
> limitations:
>
> 100mb limit per state, use disk to overcome this
>
> for sharded aggregation query, the mongos will send request to all
> shards.now if we ask for data,like for group or sort, it wil be
> fetched from all shards, Now the processing will be done in the
> primary shard only.requests that doesnt need to look into all shards,
> like match or projection can happen in parallel.
>
>  
>
> So for large aggreatatinsn mongo is less performacne. So we can get
> data to hadoop and do there.
>
>  
>
> find states with pop over 1M. First group by zip in states and find
> sum of pop aggreagatins. Then do a match aggregation for pop sum above
> 1m
>
>  
>
> in java driver, aggregation pipeline is a list.
>
>  
>
>  
>
> Document.parse in java can parse the query from console to java query
>
> colleciton.aggregate instead of find in java for aggregation
>
>  
>
> \$ne : not equal to operator
>
>  
>
> mongoimport -d test -c zips --drop zips.json : import and drop any
> prev collection
>
>  
>
> {\$substr : \["\$city",0,1\]}, substring . extract first char.
>
> Check simialr operators in mongo
>
>  
>
> Final:4
>
> db.posts.update({'permalink': 'cxzdzjkztkqraoqlgcru'},
>
> {'\$inc': {'comments.2.num\_likes': 1}})
>
>  
>
> String commentIdentifier = "comments." + ordinal + ".num\_likes";
>
>  
>
> postsCollection.updateOne(
>
> eq("permalink", permalink),
>
> new Document("\$inc", new Document(commentIdentifier, 1)));
>
>  
>
>  
>
>  
>
>  
>
> Journal is a log of every single txn in the db. Data is read and
> written from memory cache. Now eveything in memory cache is writen to
> journal as well. Now journal is in memory as well. So the real
> peristance of data happens when journal is written to disk
>
> So for an update, data is written to memory cahce pages and journal.
> By default mongo runs with value w=1 meaning wait for acknowledge from
> mongo server. (This means just wait for ack from server which is
> usually just writing to memory and not disk). Now the value j= false
> by default .this means don’t wait for journal to be written to disk
>
> So this means when an update happends, we are really updating in
> memory and disk write happens later.
>
> So if server crashes before journal is wriiten to disk, data is lost.
>
>  
>
> Now memory cache pages are primary data source which are written to
> disk and read Journal is a backup mechanism like a failover. We can
> set j=true, so that journal is always wriiten to disk before ack. So
> after a crash, mongod can read journal and re create the writes and
> updates.
>
>  
>
> Now ack from server may be lost due to nw errors. So we might try
> again and for cases like increment field updates, this cause errors.
> So need to handle this. Either check data before trying again or
> covnert update to insert( read doc ,update it inline, delete old one
> and insert)
>
>  
>
> Replication: for availability and fault tolerance. Set to nodes
> together. One primary and more secondary's. Data from prim async go to
> secondary. App connects to primary. If primary goes down, secondary
> nodes elect a primary. When primary comes back up, it can become a
> seconday. Minimum nodes for a cluster replica is 3, Because if prim
> goes down we need a majority vote and with only 2 nodes and if 1 goes
> down only one remain and there is no majority.
>
>  
>
> Types of replica set nodes:

-   Regular: normal node that has data and can be primary or secondary

-   Arbiter: Just for voting purposes. For eg if we have even no of
    > nodes, we can use arbitor to meet majority condition. Above
    > example of 2 nodes with arbitror. It has no data

-   Delayed : Some time delayed node for disaster. Can vote but can nto
    > be a primary. (priority =0)

-   Hidden: Cannot be primary but can vote. (priority =0) . For
    > analytics

>  
>
> Write consistency: There is always a single primary. Writes have to go
> to primary. But reads can go to secondary. If reads also go to primary
> we have strong consistency between write ad read. Read from sec may be
> stale. Lag between prim and sec is not consistent as replication is
> async. Durnig failover, we lose primary and so for a short time no
> write can occur. Consistency in mongo is better than eventual
> consistency, (when read and write is from primary). But if we go for
> sec read, we are using eventual consistency.
>
>  
>
> Create replica set by giving the same name to all process started.
> After starting the process, we have to create a config with mongod
> details, with details of al hosts, ip, ports which is the primary(
> priority 1) etc. and initiate the cluster with this config. We can run
> config only from a node that become primary.
>
>  
>
> To enable read from secondary in a replica cluster, we need to set
> rs.slaveOk(). Rs.status() for details of replica
>
>  
>
> Each replica node has an oplog. Sec are constantly reading oplogs of
> primary. It's true that the oplog entries originally come from the
> primary, but secondaries can sync from another secondary, as long as
> at least there is a chain of oplog syncs that lead back to the
> primary.
>
>  
>
> Use local : switch to internal db
>
> One collection is oplog.rs
>
> Check that to see the commands being replicated across nodes
>
> Oplog is capped at a size limit. So we need big enough size to handel
> large failures.
>
> We can have replica set with one node in wiredTiger and one in MMAP
>
>  
>
> Failover: Consider three nodes and with two secs, both lagging behind
> primary by few seconds. Now when primary goes down and one of the sec
> becomes primary, some data is not there. Now when old prim comes back
> up, it finds it has some data not in current primary and it rolls
> back. This causes data loss. To avoid this, we need to wait toll
> majority of nodes have the write.
>
>  
>
> Even if oplog has looped( like rotation), a node coming back up will
> copy all the oplog It will use its time stamp and the logs timestamp
> for this.
>
>  
>
> From java driver, pass a list of mongo servers to enable automatic
> choosing of primary and failovers. We can also specify a replica set
> option while connectin to ensure we connet to correct replica set
>
>  
>
> Even with a list of servers from java, we will get execptions from
> mongo server, like node down durnig insert etc. we have to handle
> this.
>
>  
>
> W param determines how many nodes we want the data to be written
> before we confirm. So for 3 nodes, w=1 will wait only for prim, w=2
> will wait for prim and a sec .
>
> Wtimeout : how long we wait for sec to ack the writes
>
> Both of the above and j are called write concerns
>
> W can be set to "majority" instead of manully finding majority . This
> avoid the scenario of roll backs mentioned above.
>
> j=true is only on primary. We wait for j to commit in primary. No
> guarantee that its written in secondary
>
>  
>
> Readpreferences: options are 1) primary 2) primary preferred 3)
> secondary 4) secondary preferred 5) nearest
>
> 2 preferres primary but goes to sec if prim not there. 5 choose one
> with lowest ping
>
>  
>
> Issues on reading from secondary:
>
>  

-   If the secondary hardware has insufficient memory to keep the read
    > working set in memory, directing reads to it will likely slow
    > it down.

    -   True.

    -   This could really go either way. If the secondary has excess
        > capacity, beyond what it needs to take writes, then directing
        > reads to it would cause it to work more, but perhaps it would
        > still be able to keep up with the oplog. On the other hand, if
        > the primary is taking writes faster than the secondary can
        > keep up, then this scenario would definitely slow it down.

    -   Generally, your secondary should be on the same hardware as your
        > primary, so if that's the case, and your primary *would* be
        > able to keep up with the reads, then this shouldn't be
        > a problem. Of course, if your primary can handle both the read
        > and write loads, then there's really no compelling reason to
        > send the reads to the secondary.

-   If your write traffic is great enough, and your secondary is less
    > powerful than the primary, you may overwhelm the secondary, which
    > must process all the writes as well as the reads. Replication lag
    > can result.

    -   True.

    -   This is a design anti-pattern that we sometimes see.

    -   A similar anti-pattern occurs when reads are routed to the
        > primary, but the secondary is underpowered and unable to
        > handle the full read + write load. In this case, if the
        > secondary becomes primary, it will be unable to fulfill
        > its job.

-   You may not read what you previously wrote to MongoDB on a secondary
    > because it will lag behind by some amount.

    -   True.

    -   This is pretty straightforward. Unless you are reading from the
        > primary, the secondary will not necessarily have the most
        > current version of the documents you need to read.

    -   Whether this is a problem or not depends on your application's
        > requirements and business concerns, so it goes a bit outside
        > the scope of development.

>  
>
> From
> &lt;<https://university.mongodb.com/courses/MongoDB/M101J/2015_ondemand_v3/courseware/Week_6_Application_Engineering_/52b36d18e2d423678d3b9d79>&gt;
>
>  
>
> Sharding: Works on basis on mongos service router. Uses a range based
> approach (though new mongo versions suports hash based sharding ).
>
> With sharding, any insert should have the shard key. We can have
> shards at collection and db level. Not sharded collections are at
> shard zero. There can be more than one mongos instances. Similar to
> replica. In shard, our app connect to mongos.
>
>  
>
> Sharding also have a set of config servers which hold how data is
> sharded. (typically 3 config servers)
>
> In sharding data is broken into chunks, whichh are mapped to different
> shards. Config server knows about these chunks and their mappings.
> Config servers are not a replica set. They use a two phase commit in
> the background
>
>  
>
> Shard key doesn’t need to be unique ( not a prim key). It needs to
> have an index on that field and included in all inserts. It is just
> used to find the shard. Queryign can then happen on another fields
>
>  
>
> To shard, we create one shard with replica, repeat for all other
> shards and the create the config servers. We then start mongos by
> passing it details of the config servers, then like createing replica,
> we pass a config about the shards to mongos
>
> Sh.status() gives shard status
>
> Index on shard key cannot be multi key. It has to be on the shard key
> or a multi key starting with shard key. So if we use shard key
> (studnetid, classid), then there shld be an index on (studentid,
> classid, somethng else).
>
> With sharding we cannot have unique indexes other than shard key , or
> part of shard key (like multi above). Reason is that we cannot enforce
> uniqueness in sharded cases as data is spread across.
>
>  
>
> Shard key is immutable. So once we set it . It cannot be changed.
>
>  
>
> Doing updates, give either shard key or multi true. Multi will send
> request to all shards.
>
>  
>
> With shards, the write concerns (see above) still holds true. True for
> even multi shard updates.
>
>  
>
> Monogs is usually sharded (usually run on same machine)
>
>  
>
> Shard key: Choose one wit sufficent variety of values. Not somethnig
> that will ever have only 3 values. Also we can add a secondary part of
> key to add more cardinality.
>
> Avoid hot spotting of writes: means majority of writes always going to
> same shard. Due to the way how shard is split. Like last shard having
> the data from x: max value. So if our key increase above x, all writes
> go to last shard. So shard key shouldn’t ideally be monotonically
> increasing to avoid these problems
>
>  
>
> For eg: sharding on order id: order id is increasing monotonically. So
> avoid that. Combine it with date or vendor or both to get sufficient
> variety
>
>  
>
> Final: Question 2
>
> Please use the Enron dataset you imported for the previous problem.
> For this question you will use the aggregation framework to figure out
> pairs of people that tend to communicate a lot. To do this, you will
> need to unwind the To list for each message. 
>
>  
>
> This problem is a little tricky because a recipient may appear more
> than once in the To list for a message. You will need to fix that in a
> stage of the aggregation before doing your grouping and counting of
> (sender, recipient) pairs. 
>
>  
>
> From
> &lt;<https://university.mongodb.com/courses/MongoDB/M101J/2015_ondemand_v3/courseware/Final_Exam/52b88246e2d42307189eef2e>&gt;
>
>  
>
> db.sample.aggregate(\[{\$unwind:'\$tags'},{\$group:{\_id:'\$\_id',name:{\$first:'\$name'},tags:{\$addToSet:'\$tags'}}},{\$unwind:'\$tags'},{\$group:{\_id:{name:'\$name',tags:'\$tags'},count:{\$sum:1}}}\]);
>
>  
>
> db.messages.aggregate(\[{\$unwind:'\$headers.To'},{\$group:{\_id:'\$\_id',name:{\$first:'\$headers.From'},tags:{\$addToSet:'\$headers.To'}}},{\$unwind:'\$headers.To'},{\$group:{\_id:{name:'\$headers.From',tags:'\$headers.To'},count:{\$sum:1}}},{\$limit:5}\]);
>
>  
>
> 3:
>
>  
>
> db.messages.update({'headers.Message-ID':'&lt;8147308.1075851042335.JavaMail.evans@thyme&gt;'},{\$push:{'headers.To':'mrpotatohead@10gen.com'}});
>
>

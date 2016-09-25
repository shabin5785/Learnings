Basics

Wednesday, January 20, 2016

15:18

 

To be able to store Point objects in the database using JPA we need to
define an entity class. A JPA entity class is a POJO (Plain Old Java
Object) class, i.e. an ordinary Java class that is marked (annotated) as
having the ability to represent objects in the database. Conceptually
this is similar to serializable classes, which are marked as having the
ability to be serialized.

 

The only unique JPA addition is the @Entity annotation, which marks the
class as an entity class. An attempt to persist Point objects in the
database without marking the Point class as an entity class will cause a
PersistenceException.

 

Storing an entity object in the database does not store methods and
code. Only the persistent state of the entity object, as reflected by
its persistent fields is stored. By default, any field that is not
declared as static or transient is a persistent field.

 

 

In JPA a database connection is represented by
the [EntityManager](http://www.objectdb.com/api/java/jpa/EntityManager) interface.
Therefore, in order to manipulate an ObjectDB database we need
an EntityManager instance. Operations that modify database content also
require
an [EntityTransaction](http://www.objectdb.com/api/java/jpa/EntityTransaction) instance.

 

Obtaining
an [EntityManager](http://www.objectdb.com/api/java/jpa/EntityManager) instance
consists of two steps. First we need to obtain an instance
of[EntityManagerFactory](http://www.objectdb.com/api/java/jpa/EntityManagerFactory) that
represents the relevant database and then we can use that factory
instance to get an EntityManager instance. JPA requires the definition
of a [persistence
unit](http://www.objectdb.com/java/jpa/entity/persistence-unit) in an
XML file in order to be able to generate an EntityManagerFactory

 

The EntityManager instance represents a connection to the database. When
using JPA, every operation on a database is associated with
an EntityManager. Further, in a multithreaded application every thread
usually has its own EntityManager instance while at the same time
sharing a single application-wide EntityManagerFactory.

 

Closing an EntityManager does not close the database itself (that is the
job of the factory as previously explained). Once
the EntityManager object is closed it cannot be reused. But, the
owning EntityManagerFactory instance may preserve
the EntityManager's resources (such as a database file pointer or a
socket to a remote server) in a connection pool and use them to speed up
future EntityManager construction.

 

 

**EntityTransaction**

Operations that modify database content, such as store, update, and
delete should only be performed within an active transaction.

Given
an [EntityManager](http://www.objectdb.com/api/java/jpa/EntityManager),
em, it is very easy to begin a transaction:

em.[getTransaction](http://www.objectdb.com/api/java/jpa/EntityManager/getTransaction)().[begin](http://www.objectdb.com/api/java/jpa/EntityTransaction/begin)();

There is a one to one relationship between an EntityManager instance and
its
associated [EntityTransaction](http://www.objectdb.com/api/java/jpa/EntityTransaction) instances
that
the [getTransaction](http://www.objectdb.com/api/java/jpa/EntityManager/getTransaction) method
returns.

When a transaction is active you can invoke EntityManager methods that
modify the database content, such
as [persist](http://www.objectdb.com/api/java/jpa/EntityManager/persist_Object) and [remove](http://www.objectdb.com/api/java/jpa/EntityManager/remove_Object).
Database updates are collected and managed in memory and applied to the
database when the transaction is committed:

em.[getTransaction](http://www.objectdb.com/api/java/jpa/EntityManager/getTransaction)().[commit](http://www.objectdb.com/api/java/jpa/EntityTransaction/commit)();

 

**CRUD**

 

em.[getTransaction](http://www.objectdb.com/api/java/jpa/EntityManager/getTransaction)().[begin](http://www.objectdb.com/api/java/jpa/EntityTransaction/begin)();\
for (int i = 0; i &lt; 1000; i++) {\
Point p = new Point(i, i);\
em.[persist](http://www.objectdb.com/api/java/jpa/EntityManager/persist_Object)(p);\
}\
em.[getTransaction](http://www.objectdb.com/api/java/jpa/EntityManager/getTransaction)().[commit](http://www.objectdb.com/api/java/jpa/EntityTransaction/commit)();

 

Operations that modify the content of the database (such as storing new
objects) require an active transaction. In the example above, every
Point object is first constructed as an ordinary Java object. It then
becomes associated with an EntityManager and with its transaction (as a
managed entity) by the persist method. The new Point objects are
physically stored in the database only when the transaction is
committed.

 

**Updating and Deleting Entities**

JPA refers to entity objects that are associated with
an [EntityManager](http://www.objectdb.com/api/java/jpa/EntityManager) as
'managed'. A newly constructed entity object becomes managed by
an EntityManager when
the [persist](http://www.objectdb.com/api/java/jpa/EntityManager/persist_Object) method
is invoked. Objects that are retrieved from the database are managed by
the EntityManager that was used to retrieve them

 

To delete an object from the database, you need to obtain a managed
object (usually by retrieval) and invoke
the [remove](http://www.objectdb.com/api/java/jpa/EntityManager/remove_Object) method
within the context of an active transaction:

em.[getTransaction](http://www.objectdb.com/api/java/jpa/EntityManager/getTransaction)().[begin](http://www.objectdb.com/api/java/jpa/EntityTransaction/begin)();\
em.[remove](http://www.objectdb.com/api/java/jpa/EntityManager/remove_Object)(p);
// delete entity\
em.[getTransaction](http://www.objectdb.com/api/java/jpa/EntityManager/getTransaction)().[commit](http://www.objectdb.com/api/java/jpa/EntityTransaction/commit)();

In the above code, p must be a managed entity object of
the EntityManager em. The entity object is marked for deletion by
the remove method and is physically deleted from the database when the
transaction is committed.

Updating an existing database object is similar. You have to obtain a
managed entity object (e.g. by retrieval) and modify it within an active
transaction:

 

You may notice that em, the managing EntityManager of p, is not
mentioned explicitly when p is being updated. The EntityManager that
manages an entity is responsible for automatically detecting changes to
the entity object and applying them to the database when the transaction
is committed.

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

Entity Classes

Wednesday, January 20, 2016

15:30

 

> A portable JPA entity class:

-   should be a top-level class (i.e. not a nested / inner class).

-   should have a public or protected no-arg constructor.

-   cannot be final and cannot have final methods
    > or final instance variables.

>  
>
> **Entity Class Names**
>
> Entity classes are represented [in
> queries](http://www.objectdb.com/java/jpa/query/jpql/from) by *entity
> names*. By default, the entity name is the unqualified name of the
> entity class (i.e. the short class name excluding the package name). A
> different entity name can be set explicitly by using
> the [name](http://www.objectdb.com/api/java/jpa/Entity/name) attribute
> of
> the [Entity](http://www.objectdb.com/api/java/jpa/Entity) annotation:
>
> [@Entity](http://www.objectdb.com/api/java/jpa/Entity)([name](http://www.objectdb.com/api/java/jpa/Entity/name)="MyName")\
> public class MyEntity {\
>  \
> }
>
> Entity names must be unique. When two entity classes in different
> packages share the same class name, explicit entity name setting is
> required to avoid collision.
>
>  
>
> **Transient Fields**
>
> Transient entity fields are fields that do not participate in
> persistence and their values are never stored in the database .
>
> Static and final entity fields are always considered to be transient.
> Other fields can be declared explicitly as transient using either the
> Java transient modifier (which also affects serialization) or the
> JPA [@Transient](http://www.objectdb.com/api/java/jpa/Transient) annotation
>
>  
>
> **Persistent Fields**
>
> Every non-static non-final entity field is persistent by default
> unless explicitly specified otherwise (e.g. by using
> the [@Transient](http://www.objectdb.com/api/java/jpa/Transient) annotation).
>
> Storing an entity object in the database does not store methods or
> code. Only the persistent state of the entity object, as reflected by
> its persistent fields (including persistent fields that are inherited
> from ancestor classes), is stored.
>
> When an entity object is stored in the database every persistent field
> must contain either null or a value of one of the
> supported [persistable
> types](http://www.objectdb.com/java/jpa/entity/types)
>
>  
>
>  
>
> Every persistent field can be marked with one of the following
> annotations:

-   [OneToOne](http://www.objectdb.com/api/java/jpa/OneToOne), [ManyToOne](http://www.objectdb.com/api/java/jpa/ManyToOne) -
    > for references of entity types.

-   [OneToMany](http://www.objectdb.com/api/java/jpa/OneToMany), [ManyToMany](http://www.objectdb.com/api/java/jpa/ManyToMany) -
    > for collections and maps of entity types.

-   [Basic](http://www.objectdb.com/api/java/jpa/Basic) - for any other
    > persistable type.

> In JPA only [Basic](http://www.objectdb.com/api/java/jpa/Basic) is
> optional while the other annotations above are required when
> applicable. 
>
>  
>
> **Inverse Fields**
>
> Inverse (or mapped by) fields contain data that is not stored as part
> of the entity in the database, but is still available after retrieval
> by a special automatic query.
>
> JPA Primary Key
>
> Every entity object that is stored in the database has a primary key.
> Once assigned, the primary key cannot be modified. It represents the
> entity object as long as it exists in the database.
>
> Every entity object in the database is uniquely identified (and can
> be [retrieved](http://www.objectdb.com/java/jpa/persistence/retrieve) from
> the database) by the combination of its type and its primary key.
> Primary key values are unique per entity class. Instances of different
> entity classes, however, may share the same primary key value.
>
> Only entity objects have primary keys. Instances of other [persistable
> types](http://www.objectdb.com/java/jpa/entity/types) are always
> stored as part of their containing entity objects and do not have
> their own separate identity.
>
>  
>
> **Automatic Primary Key**
>
> By default the primary key is a sequential 64 bit number (long) that
> is set automatically by ObjectDB for every new entity object that is
> stored in the database. The primary key of the first entity object in
> the database is 1, the primary key of the second entity object is 2,
> etc. Primary key values are **not** recycled when entity objects are
> deleted from the database.
>
>  
>
> The [@Id](http://www.objectdb.com/api/java/jpa/Id) annotation marks a
> field as a primary key field. When a primary key field is defined the
> primary key value is automatically injected into that field by
> ObjectDB.
>
>  
>
> If an entity has a primary key field that is not marked
> with [@GeneratedValue](http://www.objectdb.com/api/java/jpa/GeneratedValue),
> automatic primary key value is not generated and the application is
> responsible to set a primary key by initializing the primary key
> field. That must be done before any attempt to persist the entity
> object:
>
>  
>
> **Composite Primary Key**
>
> A composite primary key consist of multiple primary key fields. Each
> primary key field must be one of the supported types listed above.
>
>  
>
> [@Entity](http://www.objectdb.com/api/java/jpa/Entity)
> [@IdClass](http://www.objectdb.com/api/java/jpa/IdClass)(ProjectId.class)\
> public class Project {\
> [@Id](http://www.objectdb.com/api/java/jpa/Id) int departmentId;\
> [@Id](http://www.objectdb.com/api/java/jpa/Id) long projectId;\
> :\
> }
>
> When an entity has multiple primary key fields, JPA requires defining
> a special ID class that is attached to the entity class using
> the [@IdClass](http://www.objectdb.com/api/java/jpa/IdClass) annotation.
> The ID class reflects the primary key fields and its objects can
> represent primary key values:
>
> Class ProjectId {\
> int departmentId;\
> long projectId;\
> }
>
>  
>
> **Obtaining the Primary Key**
>
> JPA 2 provides a generic method for getting the object ID (primary
> key) of a specified managed entity object. For example:
>
> [PersistenceUnitUtil](http://www.objectdb.com/api/java/jpa/PersistenceUnitUtil)
> util =
> emf.[getPersistenceUnitUtil](http://www.objectdb.com/api/java/jpa/EntityManagerFactory/getPersistenceUnitUtil)();\
> Object projectId =
> util.[getIdentifier](http://www.objectdb.com/api/java/jpa/PersistenceUnitUtil/getIdentifier_Object)(project);
>
> A [PersistenceUnitUtil](http://www.objectdb.com/api/java/jpa/EntityManagerFactory/getPersistenceUnitUtil) instance
> is obtained from
> the [EntityManagerFactory](http://www.objectdb.com/api/java/jpa/EntityManagerFactory).
> The [getIdentifier](http://www.objectdb.com/api/java/jpa/PersistenceUnitUtil/getIdentifier_Object)method
> takes one argument, a managed entity object, and returns the primary
> key. In case of a composite primary key - an instance of the ID class
> or the embeddable class is returned.
>
>  
>
> **Using Primary Keys for Object Clustering**
>
> Entity objects are physically stored in the database ordered by their
> primary key. Sometimes it is useful to choose a primary key that helps
> clustering entity objects in the database in an efficient way. This is
> especially useful when using queries that return large result sets.
>
>  
>
>  
>
> Auto Generated Values
>
> Marking a field with
> the [@GeneratedValue](http://www.objectdb.com/api/java/jpa/GeneratedValue) annotation
> specifies that a value will be automatically generated for that field.
>
>  
>
> From &lt;<http://www.objectdb.com/java/jpa/entity/generated>&gt;
>
>  
>
> **The Auto Strategy**
>
>  
>
> AUTO is the default strategy, During a commit the AUTO strategy uses
> the global number generator to generate a primary key for every new
> entity object. These generated values are unique at the database level
> and are never recycled
>
>  
>
> The **IDENTITY** strategy also generates an automatic value during
> commit for every new entity object. The difference is that a separate
> identity generator is managed per type hierarchy, so generated values
> are unique only per type hierarchy.
>
>  
>
> **The Sequence Strategy**
>
> The sequence strategy consists of two parts - defining a named
> sequence and using the named sequence in one or more fields in one or
> more classes.
> The [@SequenceGenerator](http://www.objectdb.com/api/java/jpa/SequenceGenerator) annotation
> is used to define a sequence and accepts a name, an initial value (the
> default is 1) and an allocation size (the default is 50). A sequence
> is global to the application and can be used by one or more fields in
> one or more classes.
>
> Unlike AUTO and IDENTITY, the SEQUENCE strategy generates an automatic
> value as soon as a new entity object is persisted (i.e. before
> commit). This may be useful when the primary key value is needed
> earlier. To minimize round trips to the database server, IDs are
> allocated in groups. The number of IDs in each allocation is specified
> by the allocationSize attribute. It is possible that some of the IDs
> in a given allocation will not be used. Therefore, this strategy does
> not guarantee there will be no gaps in sequence values.
>
>  
>
> ORM-based JPA providers (such as Hibernate, TopLink, EclipseLink,
> OpenJPA, JPOX, etc.) simulate a sequence using a **table** to support
> this **strategy**
>
> A tiny difference is related to the initial value attribute. Whereas
> the SEQUENCE strategy maintains the next sequence number to be used
> the TABLE strategy maintains the last value that was used. The
> implication for the initialValue attribute is that if you want
> sequence numbers to start with 1 in the TABLE strategy initialValue=0
> has to be specified in the @SequenceGenerator annotation.
>
>  
>
>  
>
>  
>
> Index Definition
>
>  
>
> Querying without indexes requires iteration over entity objects in the
> database one by one.
>
> This may take a significant amount of time if many entity objects have
> to be examined. Using proper indexes the iteration can be avoided and
> complex queries over millions of objects can be executed quickly.
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
>
>  
>
>  
>
>  
>
>  

 

 

Query Syntax

Wednesday, January 20, 2016

12:25

> The syntax of the Java Persistence Query Language (JPQL) is very
> similar to the syntax of SQL. Having a SQL like syntax in JPA queries
> is an important advantage because SQL is a very powerful query
> language and many developers are already familiar with it.
>
>  
>
> The main difference between SQL and JPQL is that SQL works with
> relational database tables, records and fields, whereas JPQL works
> with Java classes and objects. For example, a JPQL query can retrieve
> and return entity objects rather than just field values from database
> tables, as with SQL. That makes JPQL more object oriented friendly and
> easier to use in Java.
>
>  
>
> **JPQL Query Structure**
>
> As with SQL, a JPQL SELECT query also consists of up to 6 clauses in
> the following format:
>
> SELECT ... FROM ...\
> \[WHERE ...\]\
> \[GROUP BY ... \[HAVING ...\]\]\
> \[ORDER BY ...\]
>
>  
>
> The first two
> clauses, [SELECT](http://www.objectdb.com/java/jpa/query/jpql/select) and [FROM](http://www.objectdb.com/java/jpa/query/jpql/from) are
> required in every retrieval query (update and delete queries have a
> slightly different form). The other JPQL
> clauses, [WHERE](http://www.objectdb.com/java/jpa/query/jpql/where), [GROUP
> BY](http://www.objectdb.com/java/jpa/query/jpql/group), [HAVING](http://www.objectdb.com/java/jpa/query/jpql/group#GROUP_BY_with_HAVING) and[ORDER
> BY](http://www.objectdb.com/java/jpa/query/jpql/order) are optional.
>
> The structure of
> JPQL [DELETE](http://www.objectdb.com/java/jpa/query/jpql/delete) and [UPDATE](http://www.objectdb.com/java/jpa/query/jpql/update) queries
> is simpler:
>
> DELETE FROM ... \[WHERE ...\]\
>  \
> UPDATE ... SET ... \[WHERE ...\]
>
>  
>
> Besides a few exceptions, JPQL is case insensitive. JPQL keywords, for
> example, can appear in queries either in upper case (e.g. SELECT) or
> in lower case (e.g. select). The few exceptions in which JPQL is case
> sensitive include mainly Java source elements such as names of entity
> classes and persistent fields, which are case sensitive. In addition,
> string literals are also case sensitive 
>
>  
>
> **A Minimal JPQL Query**
>
>  
>
> SELECT c FROM Country AS c
>
>  
>
> The FROM clause declares one or more query variables (also known as
> identification variables). Query variables are similar to loop
> variables in programing languages. Each query variable represents
> iteration over objects in the database. A query variable that is bound
> to an entity class is referred to as a range variable. Range variables
> define iteration over all the database objects of a binding entity
> class and its descendant classes. In the query above, c is a range
> variable that is bound to the Country entity class and defines
> iteration over all the Country objects in the database.
>
>  
>
> . Notice that query results must always be specified explicitly - JPQL
> does not support the "SELECT \*" expression (which is commonly used in
> SQL).
>
>  
>
> **SELECT**
>
>  
>
> JPQL queries can also return results which are not entity objects. For
> example, the following query returns country names as String
> instances, rather than Country objects:
>
> SELECT c.name FROM Country AS c
>
> Using [path
> expressions](http://www.objectdb.com/java/jpa/query/jpql/path#Navigation_through_Path_Expressions),
> such as c.name, in query results is referred to as projection. The
> field values are extracted from (or projected out of) entity objects
> to form the query results.
>
>  
>
> Nested path expressions are also supported. For example, the following
> query retrieves the name of the capital city of a specified country:
>
> SELECT c.capital.name FROM Country AS c WHERE c.name = :name
>
>  
>
> Because construction of managed entity objects has some overhead,
> queries that return non entity objects, as the two queries above, are
> usually more efficient. Such queries are useful mainly for displaying
> information efficiently. They are less productive with operations that
> update or delete entity objects, in which managed entity objects are
> needed.
>
>  
>
>  
>
> The SELECT clause may also define composite results:
>
> SELECT c.name, c.capital.name FROM Country AS c
>
>  
>
> [TypedQuery](http://www.objectdb.com/api/java/jpa/TypedQuery)&lt;Object\[\]&gt;
> query =
> em.[createQuery](http://www.objectdb.com/api/java/jpa/EntityManager/createQuery_String_Class_)(\
> "SELECT c.name, c.capital.name FROM Country AS c", Object\[\].class);\
> List&lt;Object\[\]&gt; results =
> query.[getResultList](http://www.objectdb.com/api/member/getResultList)();\
> for (Object\[\] result : results) {\
> System.out.println("Country: " + result\[0\] + ", Capital: " +
> result\[1\]);\
> }
>
>  
>
>  
>
> JPA supports wrapping JPQL query results with instances of custom
> result classes. This is mainly useful for queries with multiple SELECT
> expressions, where custom result objects can provide an object
> oriented alternative to representing results as Object\[\] elements.
>
> The result class must have a compatible constructor that matches the
> SELECT result expressions, The fully qualified name of the result
> class is specified in a NEW expression, as follows:
>
> SELECT NEW example.CountryAndCapital(c.name, c.capital.name)\
> FROM Country AS c
>
> If an entity class is used as a result class, the result entity
> objects are created in the [NEW
> state](http://www.objectdb.com/java/jpa/persistence/managed#Entity_Object_Life_Cycle),
> which means that they are not managed. Such entity objects are missing
> the JPA functionality of managed entity objects (e.g. transparent
> navigation and transparent update detection), but they are more
> lightweight, they are built faster and they consume less memory
>
>  
>
> Duplicate results can be eliminated easily in JPQL by using the
> DISTINCT keyword:
>
> SELECT DISTINCT c.currency FROM Country AS c WHERE c.name LIKE 'I%'
>
>  
>
> **FROM**
>
> For example, in the following query, c iterates over all
> the Country objects in the database:
>
> SELECT c FROM Country AS c
>
> The AS keyword is optional, and the same query can also be written as
> follows:
>
> SELECT c FROM Country c
>
>  
>
> By default, the name of an entity class in a JPQL query is the
> unqualified name of the class (e.g. just Country with no package
> name). The default name can be overridden by specifying another name
> explicitly in the @Entity's name annotation element.
>
>  
>
> Multiple range variables are allowed. For example, the following query
> returns all the pairs of countries that share a common border:
>
> SELECT c1, c2 FROM Country c1, Country c2\
> WHERE c2 MEMBER OF c1.neighbors
>
> Multiple variables are equivalent to nested loops in a program. The
> FROM clause above defines two loops. The outer loop uses c1 to iterate
> over all the Country objects. The inner loop uses c2 to also iterate
> over all the Country objects. A similar query with no WHERE clause
> would return all the possible combinations of two countries. The WHERE
> clause filters any pair of countries that do not share a border,
> returning as results only neighbor countries.
>
>  
>
> The following query uses one range variable and one join variable:
>
> SELECT c1, c2 FROM Country c1 INNER JOIN c1.neighbors c2
>
> In JPQL, JOIN can only appear in a FROM clause. The INNER keyword is
> optional (i.e. INNER JOIN is equivalent to JOIN). c1 is declared as a
> range variable that iterates over all the Country objects in the
> database. c2 is declared as a join variable that is bound to
> the c1.neighbors path and iterates only over objects in that
> collection.
>
>  
>
> **WHERE **
>
>  
>
> The following query retrieves only countries with population size that
> exceeds a specified limit, which is represented by the parameter p:
>
> SELECT c FROM Country c WHERE c.population &gt; :p
>
>  
>
> The FROM clause of this query defines an iteration over all the
> Country objects in the database using the c range variable. Before
> passing these Country objects to the SELECT clause for collecting as
> query results, the WHERE clause gets an opportunity to function as a
> filter
>
>  
>
> Formally, the WHERE clause functions as a filter between the FROM and
> the SELECT clauses. Practically, if a proper index is available,
> filtering is done earlier during FROM iteration. In the above
> population query, if an index is defined on the population field
> ObjectDB can use that index to iterate directly on Country objects
> that satisfy the WHERE predicate. For entity classes with millions of
> objects in the database there is a huge difference in query execution
> time if proper indexes are defined.
>
>  
>
> **GROUP BY and HAVING**
>
>  
>
> The GROUP BY clause enables grouping of query results. A JPQL query
> with a GROUP BY clause returns properties of generated groups instead
> of individual objects and fields. The position of a GROUP BY clause in
> the query execution order is after the FROM and WHERE clauses, but
> before the SELECT clause. When a GROUP BY clause exists in a JPQL
> query, database objects (or tuples of database objects) that are
> generated by the FROM clause iteration and pass the WHERE clause
> filtering (if any) are sent to grouping by the GROUP BY clauses before
> arriving at the SELECT clause
>
>  
>
> JPQL supports the five aggregate functions of SQL:

-   COUNT** **- returns a long value representing the number
    > of elements.

-   SUM** **- returns the sum of numeric values.

-   AVG** **- returns the average of numeric values as a double value.

-   MIN** **- returns the minimum of comparable values (numeric,
    > strings, dates).

-   MAX** **- returns the maximum of comparable values (numeric,
    > strings, dates).

>  
>
> Groups in JPQL grouping queries can be filtered using the HAVING
> clause. The HAVING clause for the GROUP BY clause is like the WHERE
> clause for the FROM clause.
>
> The HAVING clause stands as a filter between the GROUP BY clause and
> the SELECT clause in such a way that only groups that are accepted by
> the HAVING filter are passed to the SELECT clause. The same
> restrictions on SELECT clause in grouping queries also apply to the
> HAVING clause, which means that individual object fields are
> inaccessible. Only group properties which are the expressions that are
> used for grouping (e.g. c.currency) and aggregate expressions are
> allowed in the HAVING clause.
>
>  
>
> **ORDER BY**
>
>  
>
> The ORDER BY clause specifies a required order for the query results.
> Any JPQL query that does not include an ORDER BY clause produces
> results in an undefined and non-deterministic order.
>
>  
>
> The following query returns names of countries whose population size
> is at least one million people, ordered by the country name:
>
> SELECT c.name FROM Country c WHERE c.population &gt; 1000000 ORDER BY
> c.name
>
>  
>
> When an ORDER BY clause exists it is the last to be executed. First
> the FROM clause produces objects for examination and the WHERE clause
> selects which objects to collect as results. Then the SELECT clause
> builds the results by evaluating the result expressions. Finally the
> results are ordered by evaluation of the the ORDER BY expressions.
>
>  
>
> Only expressions that are derived directly from expressions in the
> SELECT clause are allowed in the ORDER BY clause. The following query,
> for example, is invalid because the ORDER BY expression is not part of
> the results:
>
> SELECT c.name\
> FROM Country c\
> WHERE c.population &gt; 1000000\
> ORDER BY c.population
>
>  
>
> On the other hand, the following query is valid because, given
> a Country c, the c.populationexpression can be evaluated from c:
>
> SELECT c\
> FROM Country c\
> WHERE c.population &gt; 1000000\
> ORDER BY c.population
>
>  
>
> Query results can also be ordered by multiple order expressions. In
> this case, the first expression is the primary order expression. Any
> additional order expression is used to order results for which all the
> previous order expressions produce the same values.
>
>  
>
> The default ordering direction is ascending.
>
>  
>
>  
>
> The ORDER BY clause is always the last in the query processing chain.
> If a query contains both an ORDER BY clause and a GROUP BY clause the
> SELECT clause receives groups rather than individual objects and ORDER
> BY can order these groups.
>
>  
>
> **DELETE**
>
>  
>
>  Entity objects can be deleted from the database by:

-   Retrieving the entity objects into an EntityManager.

-   Removing these objects from the EntityManager within an active
    > transaction, either explicitly by calling the remove method or
    > implicitly by a cascading operation.

-   Applying changes to the database by calling the commit method.

>  
>
> JPQL DELETE queries provide an alternative way for deleting entity
> object.
> Unlike [SELECT](http://www.objectdb.com/java/jpa/query/jpql/select)queries,
> which are used to retrieve data from the database, DELETE queries do
> not retrieve data from the database, but when executed, delete
> specified entity objects from the database.
>
>  
>
> As with any operation that modifies the database, DELETE queries can
> only be executed within an active transaction and the changes are
> visible to other users (which use other EntityManagerinstances) only
> after commit
>
>  
>
> **UPDATE**
>
>  
>
> The simpler form of UPDATE queries acts on all the instances of a
> specified entity class in the database. The UPDATE clause defines
> exactly one range variable (with or without an explicit variable name)
> for iteration. Multiple variables and JOIN are not supported
>
>  
>
> The SET clause defines one or more field update expressions (using the
> range variable name - if defined).
>
>  
>
> UPDATE queries cannot include the GROUP BY, HAVING and ORDER BY
> clauses, but the WHERE clause, which is essential for updating
> selected entity objects, is supported.
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

 

 

Expressions

Wednesday, January 20, 2016

14:47

 

> Query expressions are the foundations on which JPQL and criteria
> queries are built.
>
>  
>
> JPQL / Criteria queries support the following operators (in order of
> decreasing precedence):

-   [Navigation
    > operator (.)](http://www.objectdb.com/java/jpa/query/jpql/path#Navigation_through_Path_Expressions)

-   [Arithmetic
    > operators](http://www.objectdb.com/java/jpa/query/jpql/arithmetic#Arithmetic_Operators):\
    > \* (multiplication), / (division), +
    > (addition) and - (subtraction).

-   [Comparison
    > operators](http://www.objectdb.com/java/jpa/query/jpql/comparison):\
    > =, &lt;&gt;, &lt;, &lt;=,&gt;, &gt;=, IS \[NOT\] NULL, \[NOT\]
    > BETWEEN,\
    > including [Collection](http://www.objectdb.com/java/jpa/query/jpql/collection) operators: \[NOT\]
    > IN, IS \[NOT\] EMPTY, \[NOT\] MEMBER \[OF\]\
    > and the [\[NOT\]
    > LIKE](http://www.objectdb.com/java/jpa/query/jpql/string) operator.

-   [Logical
    > operators](http://www.objectdb.com/java/jpa/query/jpql/logical):
    > AND, OR, NOT.

>  
>
>  
>
> The **NULL** literal represents a null value, similarly to null in
> Java and SQL. Since JPQL is case insensitive, NULL, null and Null are
> equivalent. Notice that comparison with NULL in JPQL follows the SQL
> rules for NULL comparison rather than the Java rules
>
>  
>
> Similarly to Java and SQL, JPQL supports two **boolean** literals -
> TRUE and FALSE
>
>  
>
> JPQL follows the syntax of SQL for **string** literals in which
> strings are always enclosed in single quotes (e.g. 'Adam', '') and a
> single quote character in a string is represented by two single quotes
> (e.g. 'Adam''s').
>
>  
>
> JPQL follows the syntax of SQL and JDBC for **date** literals:
>
>  
>
> JPA 2 adds support for **enum** literals. Enum literals in JPQL
> queries use the ordinary Java syntax for enum values, but the fully
> qualified name of the enum type should always be specified.
>
>  
>
> **Entity type** literals represent entity types in JPQL, similar to
> the way that java.lang.Class instances in Java represent Java types.
> Entity type literals have been added in JPA 2 to enable selective
> retrieval by type.
>
>  
>
> Paths and Types 
>
>  
>
>  
>
> Instances of user defined persistable classes (entity classes, mapped
> super classes and embeddable classes) are represented in JPQL by the
> following types of expressions:

-   [Variables](http://www.objectdb.com/java/jpa/query/jpql/from) - FROM
    > identification variables and SELECT result variables.

-   [Parameters](http://www.objectdb.com/java/jpa/query/parameter) -
    > when instances of these classes are assigned as arguments.

-   Path expressions that navigate from one object to another.

>  
>
> Instances of user defined persistable classes can participate in
> direct comparison using the = and &lt;&gt; operators. But more often
> they are used in JPQL path expressions that navigate to values of
> simple types. A path expression always starts with an instance of a
> user defined class (represented by a variable, parameter or prefix
> path expression) and uses the dot (.) operator to navigate through
> persistent fields to other objects and values.
>
> For a path expression to be valid the user defined persistable class
> must contain a persistent field (or property) with a matching name.
> The path expression, however, is valid even if the persistent field is
> declared as **private** 
>
>  
>
> In Java, a NullPointerException is thrown on any attempt to access a
> field or a method via a null reference. In JPQL, the current FROM
> variable (or FROM tuple when there are multiple variables) is simply
> skipped.
>
>  
>
> The **TYPE** operator (which is new in JPA 2) returns the type of a
> specified argument, similarly to java.lang.Object's getClass method in
> Java
>
>  
>
>  
>
> The \[NOT\] LIKE operator checks if a specified string matches a
> specified pattern. The pattern  may include ordinary characters as
> well as the following wildcard characters:

-   The percent character (%) - which matches **zero or more** of
    > any character.

-   The underscore character (\_) - which matches
    > any **single** character.

>  
>
>  
>
> The LOCATE(str, substr \[, start\]) function searches a substring and
> returns its position.
>
>  
>
>  
>
> The LOWER(str) and UPPER(str) functions return a string after
> conversion to lowercase or uppercase (respectively).
>
>  
>
> **TRIM - Stripping Leading and Trailing Characters**
>
> The TRIM(\[\[LEADING|TRAILING|BOTH\] \[char\] FROM\] str) function
> returns a string after removing leading and/or trailing characters
> (usually space characters).
>
> For example:

-   TRIM(' UK ') is evaluated to 'UK'.

-   TRIM(LEADING FROM ' UK ') is evaluated to 'UK '.

-   TRIM(TRAILING FROM ' UK ') is evaluated to ' UK'.

-   TRIM(BOTH FROM ' UK ') is evaluated to 'UK'.

> By default, space characters are removed, but any other character can
> also be specified:

-   TRIM('A' FROM 'ARGENTINA') is evaluated to 'RGENTIN.

-   TRIM(LEADING 'A' FROM 'ARGENTINA') is evaluated to 'RGENTINA'.

-   TRIM(TRAILING 'A' FROM 'ARGENTINA') is evaluated to 'ARGENTIN'

>  
>
> JPA defines special JPQL expressions that are evaluated to the **date
> and time** on the database server when the query is executed:

-   CURRENT\_DATE - is evaluated to the current
    > date (a java.sql.Date instance).

-   CURRENT\_TIME - is evaluated to the current
    > time (a java.sql.Time instance).

-   CURRENT\_TIMESTAMP - is evaluated to the current timestamp, i.e.
    > date and time\
    > (a java.sql.Timestamp instance).

>  
>
>  
>
> **Collections** may appear in JPQL queries:

-   as [parameters ](http://www.objectdb.com/java/jpa/query/parameter)-
    > when collections are assigned as arguments.

-   as [path
    > expressions](http://www.objectdb.com/java/jpa/query/jpql/path) -
    > in navigation to persistent collection fields.

>  
>
>  
>
> **Comparable Data Types**
>
>  
>
> Instances of user defined classes (entity classes and embeddable
> classes) can be compared by using the equality operators (=,
> &lt;&gt;, ==, !=). For entities, e1 = e2 if e1 and e2 have the same
> type and the same primary key value. For embeddable
> objects, e1 = e2 if e1 and e2have exactly the same content.
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
>
>  

 

 

Queries

Wednesday, January 20, 2016

12:01

 

The JPA Query Language (JPQL) can be considered as an object oriented
version of SQL. Queries are represented in JPA 2 by two interfaces - the
old Query interface, which was the only interface available for
representing queries in JPA 1, and the new TypedQuery interface that was
introduced in JPA 2. The TypedQuery interface extends the Query
interface. In JPA 2 the Query interface should be used mainly when the
query result type is unknown or when a query returns polymorphic results
and the lowest known common denominator of all the result objects is
Object. When a more specific result type is expected queries should
usually use the TypedQuery interface. It is easier to run queries and
process the query results in a type safe manner when using the
TypedQuery interface.

 

 

As with most other operations in JPA, using queries starts with an
EntityManager (represented by em in the following code snippets), which
serves as a factory for both Query and TypedQuery:

 

[Query](http://www.objectdb.com/api/java/jpa/Query) q1 =
em.[createQuery](http://www.objectdb.com/api/java/jpa/EntityManager/createQuery_String)("SELECT
c FROM Country c");\
 \
[TypedQuery](http://www.objectdb.com/api/java/jpa/TypedQuery)&lt;Country&gt;
q2 =
em.[createQuery](http://www.objectdb.com/api/java/jpa/EntityManager/createQuery_String_Class_)("SELECT
c FROM Country c", Country.class);

 

There is another advantage of using TypedQuery in ObjectDB. In the
context of the queries above, if there are no Country instances in the
database yet and the Country class is unknown as [a managed entity
class](http://www.objectdb.com/java/jpa/entity/persistence-unit#Managed_Persistable_Classes) -
only the TypedQuery variant is valid because it introduces
the Countryclass to ObjectDB.

 

TypedQuery.getSingleResult - for use when exactly one result object is
expected.

TypedQuery.getResultList - for general use in any other case.

Query.executeUpdate - for running only DELETE and UPDATE queries.

 

The following query retrieves all the Country objects in the database.
Because multiple result objects are expected, the query should be run
using
the [getResultList](http://www.objectdb.com/api/java/jpa/TypedQuery/getResultList) method:

[TypedQuery](http://www.objectdb.com/api/java/jpa/TypedQuery)&lt;Country&gt;
query =\
em.[createQuery](http://www.objectdb.com/api/java/jpa/EntityManager/createQuery_String_Class_)("SELECT
c FROM Country c", Country.class);\
List&lt;Country&gt; results =
query.[getResultList](http://www.objectdb.com/api/java/jpa/TypedQuery/getResultList)();

 

If the database contains multiple Country objects with the name 'Canada'
(e.g. due to a bug)
a[NonUniqueResultException](http://www.objectdb.com/api/java/jpa/NonUniqueResultException) is
thrown. On the other hand, if there are no results at all
a[NoResultException](http://www.objectdb.com/api/java/jpa/NoResultException) is
thrown. Therefore,
using [getSingleResult](http://www.objectdb.com/api/java/jpa/TypedQuery/getSingleResult) requires
some caution and if there is any chance that these exceptions might be
thrown they have to be caught and handled

 

int count =
em.[createQuery](http://www.objectdb.com/api/java/jpa/EntityManager/createQuery_String)("DELETE
FROM
Country").[executeUpdate](http://www.objectdb.com/api/java/jpa/Query/executeUpdate)();

int count =
em.[createQuery](http://www.objectdb.com/api/java/jpa/EntityManager/createQuery_String)("UPDATE
Country SET area =
0").[executeUpdate](http://www.objectdb.com/api/java/jpa/Query/executeUpdate)();

 

On success - the executeUpdate method returns the number of objects that
have been updated or deleted by the query.

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

Query params

Wednesday, January 20, 2016

12:05

 

Query parameters enable the definition of reusable queries. Such queries
can be executed with different parameter values to retrieve different
results. Running the same query multiple times with different parameter
values (arguments) is more efficient than using a new query string for
every query execution, because it eliminates the need for repeated query
compilations.

 

public Country
getCountryByName([EntityManager](http://www.objectdb.com/api/java/jpa/EntityManager)
em, String name) {\
[TypedQuery](http://www.objectdb.com/api/java/jpa/TypedQuery)&lt;Country&gt;
query =
em.[createQuery](http://www.objectdb.com/api/java/jpa/EntityManager/createQuery_String_Class_)(\
"SELECT c FROM Country c WHERE c.name = :name", Country.class);\
return
query.[setParameter](http://www.objectdb.com/api/java/jpa/TypedQuery/setParameter_String_Object)("name",
name).[getSingleResult](http://www.objectdb.com/api/java/jpa/TypedQuery/getSingleResult)();\
}

 

Before the query can be executed a parameter value has to be set using
the [setParameter](http://www.objectdb.com/api/java/jpa/TypedQuery/setParameter_String_Object) method.
The [setParameter](http://www.objectdb.com/api/java/jpa/TypedQuery/setParameter_String_Object)method
supports method chaining (by returning the
same [TypedQuery](http://www.objectdb.com/api/java/jpa/TypedQuery) instance
on which it was invoked).Queries can include multiple parameters and
each parameter can have one or more occurrences in the query string. A
query can be run only after setting values for all its parameters (in no
matter in which order).

 

In addition to named parameter, whose form is :name, JPQL supports also
ordinal parameter, whose form is ?index.

 

public Country
getCountryByName([EntityManager](http://www.objectdb.com/api/java/jpa/EntityManager)
em, String name) {\
[TypedQuery](http://www.objectdb.com/api/java/jpa/TypedQuery)&lt;Country&gt;
query =
em.[createQuery](http://www.objectdb.com/api/java/jpa/EntityManager/createQuery_String_Class_)(\
"SELECT c FROM Country c WHERE c.name = ?1", Country.class);\
return
query.[setParameter](http://www.objectdb.com/api/java/jpa/TypedQuery/setParameter_int_Object)(1,
name).[getSingleResult](http://www.objectdb.com/api/java/jpa/TypedQuery/getSingleResult)();\
}

 

There are a few drawbacks to using literals rather than parameters in
queries. First, the query is not reusable. Different literal values lead
to different query strings and each query string requires its own query
compilation, which is very inefficient. On the other hand, when using
parameters, even if a
new [TypedQuery](http://www.objectdb.com/api/java/jpa/TypedQuery) instance
is constructed on every query execution, ObjectDB can identify repeating
queries with the same query string and use a [cached compiled query
program](http://www.objectdb.com/java/jpa/setting/database#The_query-cache_element),
if available. Second, embedding strings in queries is unsafe and can
expose the application to JPQL injection attacks. In addition,
parameters are more flexible and support elements that are unavailable
as literals, such as entity objects.

 

Date and Calendar parameter values require special methods in order to
specify what they represent, such as a pure date, a pure time or a
combination of date and time,

query.[setParameter](http://www.objectdb.com/api/java/jpa/TypedQuery/setParameter_String_Date_TemporalType)("date",
new java.util.Date(),
[TemporalType](http://www.objectdb.com/api/java/jpa/TemporalType).[DATE](http://www.objectdb.com/api/java/jpa/TemporalType/DATE));

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

Named Query

Wednesday, January 20, 2016

12:10

 

A named query is a statically defined query with a predefined
unchangeable query string. Using named queries instead of dynamic
queries may improve code organization by separating the JPQL query
strings from the Java code. It also enforces the use of
query [parameters](http://www.objectdb.com/java/jpa/query/parameter) rather
than embedding literals dynamically into the query string and results in
more efficient queries.

 

[@NamedQuery](http://www.objectdb.com/api/java/jpa/NamedQuery)([name](http://www.objectdb.com/api/java/jpa/NamedQuery/name)="Country.findAll",
[query](http://www.objectdb.com/api/java/jpa/NamedQuery/query)="SELECT c
FROM Country c")

 

Every [@NamedQuery](http://www.objectdb.com/api/java/jpa/NamedQuery) annotation
is attached to exactly one entity class or mapped superclass - usually
to the most relevant entity class. But since the scope of named queries
is the entire persistence unit, names should be selected carefully to
avoid collision

 

Attaching multiple named queries to the same entity class requires
wrapping them in
a [@NamedQueries](http://www.objectdb.com/api/java/jpa/NamedQueries) annotation

 

@NamedQueries({\
[@NamedQuery](http://www.objectdb.com/api/java/jpa/NamedQuery)([name](http://www.objectdb.com/api/java/jpa/NamedQuery/name)="Country.findAll",\
[query](http://www.objectdb.com/api/java/jpa/NamedQuery/query)="SELECT c
FROM Country c"),\
[@NamedQuery](http://www.objectdb.com/api/java/jpa/NamedQuery)([name](http://www.objectdb.com/api/java/jpa/NamedQuery/name)="Country.findByName",\
[query](http://www.objectdb.com/api/java/jpa/NamedQuery/query)="SELECT c
FROM Country c WHERE c.name = :name"),\
})

 

 

Named queries are represented at runtime by the
same [Query](http://www.objectdb.com/api/java/jpa/Query) and [TypedQuery](http://www.objectdb.com/api/java/jpa/TypedQuery) interfaces
but
different [EntityManager](http://www.objectdb.com/api/java/jpa/EntityManager) factory
methods are used to instantiate them.
The [createNamedQuery](http://www.objectdb.com/api/java/jpa/EntityManager/createNamedQuery_String_Class_)method
receives a query name and a result type and returns
a [TypedQuery](http://www.objectdb.com/api/java/jpa/TypedQuery) instance:

 

[TypedQuery](http://www.objectdb.com/api/java/jpa/TypedQuery)&lt;Country&gt;
query =\
em.[createNamedQuery](http://www.objectdb.com/api/java/jpa/EntityManager/createNamedQuery_String_Class_)("Country.findAll",
Country.class);\
List&lt;Country&gt; results =
query.[getResultList](http://www.objectdb.com/api/java/jpa/TypedQuery/getResultList)();

 

One of the reasons that JPA requires the listing of managed classes in a
persistence unit definition is to support named queries. Notice that
named queries may be attached to any entity class or mapped superclass.
Therefore, to be able to always locate any named query at runtime a list
of all these managed persistable classes must be available

 

 

 

 

Criteria Query

Wednesday, January 20, 2016

12:13

 

The JPA Criteria API provides an alternative way for defining JPA
queries, which is mainly useful for building dynamic queries whose exact
structure is only known at runtime.

 

JPQL queries are defined as strings, similarly to SQL. JPA criteria
queries, on the other hand, are defined by instantiation of Java objects
that represent query elements. A major advantage of using the criteria
API is that errors can be detected earlier, during compilation rather
than at runtime. On the other hand, for many developers string based
JPQL queries, which are very similar to SQL queries, are easier to use
and understand.

For simple static queries - string based JPQL queries (e.g. as [named
queries](http://www.objectdb.com/java/jpa/query/named)) may be
preferred. For dynamic queries that are built at runtime - the criteria
API may be preferred.

 

 

SELECT c FROM Country c

 

An equivalent query can be built using the JPA criteria API as follows:

[CriteriaBuilder](http://www.objectdb.com/api/java/jpa/criteria/CriteriaBuilder)
cb =
em.[getCriteriaBuilder](http://www.objectdb.com/api/java/jpa/EntityManager/getCriteriaBuilder)();\
 \
[CriteriaQuery](http://www.objectdb.com/api/java/jpa/criteria/CriteriaQuery)&lt;Country&gt;
q =
cb.[createQuery](http://www.objectdb.com/api/java/jpa/criteria/CriteriaBuilder/createQuery_Class_)(Country.class);\
[Root](http://www.objectdb.com/api/java/jpa/criteria/Root)&lt;Country&gt;
c =
q.[from](http://www.objectdb.com/api/java/jpa/criteria/AbstractQuery/from_Class_)(Country.class);\
q.[select](http://www.objectdb.com/api/java/jpa/criteria/CriteriaQuery/select_Selection_)(c);

 

In the example above a CriteriaQuery instance is created for
representing the built query. Then a Root instance is created to define
a range variable in the FROM clause. Finally, the range variable, c, is
also used in the SELECT clause as the query result expression.

 

A CriteriaQuery instance is equivalent to a JPQL string and not to
a [TypedQuery](http://www.objectdb.com/api/java/jpa/TypedQuery) instance.

Therefore, running the query still requires a TypedQuery instance:

[TypedQuery](http://www.objectdb.com/api/java/jpa/TypedQuery)&lt;Country&gt;
query =
em.[createQuery](http://www.objectdb.com/api/java/jpa/EntityManager/createQuery_CriteriaQuery_)(q);\
List&lt;Country&gt; results =
query.[getResultList](http://www.objectdb.com/api/java/jpa/Query/getResultList)();

 

 

**Parameters in Criteria Queries**

The following query string represents a JPQL query with a parameter:

SELECT c FROM Country c WHERE c.population &gt; :p

An equivalent query can be built using the JPA criteria API as follows:

[CriteriaBuilder](http://www.objectdb.com/api/java/jpa/criteria/CriteriaBuilder)
cb =
em.[getCriteriaBuilder](http://www.objectdb.com/api/java/jpa/EntityManager/getCriteriaBuilder)();\
 \
[CriteriaQuery](http://www.objectdb.com/api/java/jpa/criteria/CriteriaQuery)&lt;Country&gt;
q =
cb.[createQuery](http://www.objectdb.com/api/java/jpa/criteria/CriteriaBuilder/createQuery_Class_)(Country.class);\
[Root](http://www.objectdb.com/api/java/jpa/criteria/Root)&lt;Country&gt;
c =
q.[from](http://www.objectdb.com/api/java/jpa/criteria/AbstractQuery/from_Class_)(Country.class);\
[ParameterExpression](http://www.objectdb.com/api/java/jpa/criteria/ParameterExpression)&lt;Integer&gt;
p =
cb.[parameter](http://www.objectdb.com/api/java/jpa/criteria/CriteriaBuilder/parameter_Class_)(Integer.class);\
q.[select](http://www.objectdb.com/api/java/jpa/criteria/CriteriaQuery/select_Selection_)(c).[where](http://www.objectdb.com/api/java/jpa/criteria/CriteriaQuery/where_Expression_)(cb.[gt](http://www.objectdb.com/api/java/jpa/criteria/CriteriaBuilder/gt_Expression__Expression_)(c.[get](http://www.objectdb.com/api/java/jpa/criteria/Path/get_String)("population"),
p));

 

 

 

 

 

 

 

 

 

 

 

Query Tuning

Wednesday, January 20, 2016

12:19

 

> The [Query](http://www.objectdb.com/api/java/jpa/Query) and [TypedQuery](http://www.objectdb.com/api/java/jpa/TypedQuery) interfaces
> define various setting and tuning methods that may affect[query
> execution ](http://www.objectdb.com/java/jpa/query/execute)if invoked
> before a query is run
> using [getResultList](http://www.objectdb.com/api/java/jpa/TypedQuery/getResultList) or [getSingleResult](http://www.objectdb.com/api/java/jpa/TypedQuery/getSingleResult).
>
>  
>
>  
>
> The [setFirstResult](http://www.objectdb.com/api/java/jpa/TypedQuery/setFirstResult_int) and [setMaxResults](http://www.objectdb.com/api/java/jpa/TypedQuery/setMaxResults_int) methods
> enable defining a result window that exposes a portion of a large
> query result list (hiding anything outside that window).
> The [setFirstResult](http://www.objectdb.com/api/java/jpa/TypedQuery/setFirstResult_int)method
> is used to specify where the result window begins, i.e. how many
> results at the beginning of the complete result list should be skipped
> and ignored.
> The [setMaxResults](http://www.objectdb.com/api/java/jpa/TypedQuery/setMaxResults_int) method
> is used to specify the result window size. Any result after hitting
> that specified maximum is ignored.
>
>  
>
> These methods support the implementation of efficient result paging.
> For example, if each result page should show exactly pageSize results,
> and pageId represents the result page number (0 for the first page),
> the following expression retrieves the results for a specified page:
>
> List&lt;Country&gt; results =\
> query.[setFirstResult](http://www.objectdb.com/api/java/jpa/TypedQuery/setFirstResult_int)(pageIx
> \* pageSize)\
> .[setMaxResults](http://www.objectdb.com/api/java/jpa/TypedQuery/setMaxResults_int)(pageSize)\
> .[getResultList](http://www.objectdb.com/api/java/jpa/TypedQuery/getResultList)();
>
>  
>
> Changes made to a database using
> an [EntityManager](http://www.objectdb.com/api/java/jpa/EntityManager)
> em can be visible to anyone who uses em, even before committing the
> transaction (but not to users of other EntityManager instances). JPA
> implementations can easily make uncommitted changes visible in simple
> JPA operations, such
> as [find](http://www.objectdb.com/api/java/jpa/EntityManager/find_Class__Object).
> However, query execution is much more complex. Therefore, before a
> query is executed, uncommitted database changes (if any) have to be
> flushed to the database in order to be visible to the query.
>
>  
>
> Flush policy in JPA is represented by
> the [FlushModeType](http://www.objectdb.com/api/java/jpa/FlushModeType) enum,
> which has two values:

-   [AUTO](http://www.objectdb.com/api/java/jpa/FlushModeType/AUTO) -
    > changes are flushed before query execution and on commit/flush.

-   [COMMIT](http://www.objectdb.com/api/java/jpa/FlushModeType/COMMIT) -
    > changes are flushed only on explicit commit/flush.

>  
>
> **Lock Mode (setLockMode)**
>
> ObjectDB uses automatic [optimistic
> locking](http://www.objectdb.com/java/jpa/persistence/lock#Optimistic_Locking) to
> prevent concurrent changes to entity objects by multiple users. JPA 2
> adds support for [pessimistic
> locking](http://www.objectdb.com/java/jpa/persistence/lock#Pessimistic_Locking).
> The [setLockMode](http://www.objectdb.com/api/java/jpa/TypedQuery/setLockMode_LockModeType) method
> sets a lock mode that has to be applied on all the result objects that
> the query retrieves.
>
>  
>
> **Query Hints**
>
>  
>
> javax.persistence.query.timeout" ,
>
> "javax.persistence.lock.timeout"
>
>  
>
> Etc
>
>  
>
> **Setting Query Hint (Scopes)**
>
>  
>
> For the entire [persistence
> unit](http://www.objectdb.com/java/jpa/entity/persistence-unit) -
> using
> a [persistence.xml](http://www.objectdb.com/java/jpa/entity/persistence-unit#persistence.xml) property:
>
>  
>
> For
> an [EntityManagerFactory](http://www.objectdb.com/api/java/jpa/EntityManagerFactory) -
> using
> the [createEntityManagerFacotory](http://www.objectdb.com/api/java/jpa/Persistence/createEntityManagerFactory_String_Map) method:
>
>  
>
> For
> an [EntityManager](http://www.objectdb.com/api/java/jpa/EntityManager) -
> using
> the [createEntityManager](http://www.objectdb.com/api/java/jpa/EntityManagerFactory/createEntityManager_Map) method:
>
>  
>
> For a [named
> query](http://www.objectdb.com/java/jpa/query/named) definition -
> using
> the [hints](http://www.objectdb.com/api/java/jpa/NamedQuery/hints) element:
>
>  
>
> For a specific query execution - using
> the [setHint](http://www.objectdb.com/api/java/jpa/TypedQuery/setHint_String_Object) method
> (before query execution):
>
>  
>
> A hint that is set in a global scope affects all the queries in that
> scope (unless it is overridden in a more local scope). For example,
> setting a query hint in an EntityManager affects all the queries that
> are created in that EntityManager (except queries with explicit
> setting of the same hint).
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
>
>  
>
>  
>
>  

 

 

Relations

Wednesday, January 20, 2016

17:00

 

> **One-to-One (one direction)**
>
> ![](media/image1.png){width="4.020833333333333in"
> height="0.6666666666666666in"}
>
> Domain model of an one-to-one unidirectional relationship
>
> @Entity\
> class A {\
>    @Id int id;
>
>    [**@OneToOne**](http://download.oracle.com/javaee/6/api/javax/persistence/OneToOne.html)\
>    B b;\
> }
>
> @Entity\
> class B {\
>    @Id int id;\
> }
>
> ![](media/image2.png){width="3.3333333333333335in" height="1.25in"}
>
> Relation model of an one-to-one unidirectional relationship
>
> **Example 1, One-to-One unidirectional relationship in JPA**
>
> An employee has one desk.
>
> @Entity\
> public class Employee implements Serializable {
>
>    @Id\
>    private int id;
>
>    private String name;
>
>    [**@OneToOne**](http://download.oracle.com/javaee/6/api/javax/persistence/OneToOne.html)\
>    private Desk desk;
>
> }
>
> @Entity\
> public class Desk implements Serializable {
>
>    @Id\
>    private int id;
>
>    private String position;
>
> }
>
> ![](media/image3.png){width="4.6875in" height="2.0833333333333335in"}
>
> Physical description of an one-to-one unidirectional relationship
>
> ![](media/image4.png){width="3.8958333333333335in"
> height="1.1979166666666667in"}
>
> ER diagram of an one-to-one unidirectional relationship
>
> **One-to-One (both directions)**
>
> ![](media/image5.png){width="4.010416666666667in"
> height="0.6770833333333334in"}
>
> Domain model of an one-to-one birectional relationship
>
> In this case we would like to keep a reference between both sides.
>
> @Entity\
> class A {\
>    @Id int id;
>
>    [**@OneToOne**](http://download.oracle.com/javaee/6/api/javax/persistence/OneToOne.html)\
>    B **b**;\
> }
>
> @Entity\
> class B {\
>    @Id int id;
>
>    **[@OneToOne](http://download.oracle.com/javaee/6/api/javax/persistence/OneToOne.html)(mappedBy="b")**\
>    A a;\
> }
>
> ![](media/image6.png){width="3.3333333333333335in"
> height="1.2291666666666667in"}
>
> Relation model of an one-to-one bidirectional relationship
>
> Since the relation concerns both directions, we may change the owning
> side.
>
> @Entity\
> class A {\
>    @Id int id;
>
>    **[@OneToOne](http://download.oracle.com/javaee/6/api/javax/persistence/OneToOne.html)(mappedBy="a")**\
>    B b;\
> }
>
> @Entity\
> class B {\
>    @Id int id;
>
>    [**@OneToOne**](http://download.oracle.com/javaee/6/api/javax/persistence/OneToOne.html)\
>    A **a**;\
> }
>
> ![](media/image7.png){width="3.3229166666666665in"
> height="1.2395833333333333in"}
>
> Relation model of an one-to-one bidirectional relationship
>
> **Example 2, One-to-One bidirectional relationship in JPA**
>
> A husband has exactly one wife. A wife has exactly one husband.
>
> @Entity\
> public class Husband implements Serializable {
>
>    @Id\
>    private int id;
>
>    private String name;
>
>    [**@OneToOne**](http://download.oracle.com/javaee/6/api/javax/persistence/OneToOne.html)\
>    private Wife **wife**;
>
> }
>
> @Entity\
> public class Wife implements Serializable {
>
>    @Id\
>    private int id;
>
>    private String name;
>
>    **[@OneToOne](http://download.oracle.com/javaee/6/api/javax/persistence/OneToOne.html)(mappedBy="wife")**\
>    private Husband husband;
>
> }
>
> We assume husband is the owning side, so he will hold the foreign key.
>
> ![](media/image8.png){width="4.6875in" height="2.0416666666666665in"}
>
> Physical description of an one-to-one bidirectional relationship
>
> ![](media/image9.png){width="3.6770833333333335in"
> height="1.1770833333333333in"}
>
> ER diagram of a bidirection one-to-one relationship
>
> Now we can ask the wife “Who is your husband?”, as well as, ask the
> husband “Who is your wife?”.
>
> **Many-to-One (one direction)**
>
> ![](media/image10.png){width="4.0in" height="0.625in"}
>
> Domain model of a many-to-one unidirectional relationship
>
> @Entity\
> class A {\
>    @Id int id;
>
>    [**@ManyToOne**](http://download.oracle.com/javaee/6/api/javax/persistence/ManyToOne.html)\
>    B b;\
> }
>
> @Entity\
> class B {\
>    @Id int id;\
> }
>
> ![](media/image11.png){width="3.3333333333333335in"
> height="1.2395833333333333in"}
>
> Relation model of a many-to-one unidirectional relationship
>
> **Example 3, Many-to-One unidirectional relationship in JPA**
>
> There are millions of music fans out there. Each fan has his favorite
> singer. Of course, a signer is not able to keep detailed records of
> his fans.
>
> @Entity\
> public class Fan implements Serializable {
>
>    @Id\
>    private int id;
>
>    private String name;
>
>    [**@ManyToOne**](http://download.oracle.com/javaee/6/api/javax/persistence/ManyToOne.html)\
>    private Singer favoriteSinger;
>
> }
>
> @Entity\
> public class Singer implements Serializable {
>
>    @Id\
>    private int id;
>
>    private String name;
>
> }
>
> As a result, the foreign key goes to the fan.
>
> ![](media/image12.png){width="4.6875in" height="1.84375in"}
>
> Physical description of a many-to-one unidirectional relationship
>
> ![](media/image13.png){width="4.09375in" height="1.1875in"}
>
> ER diagram of a many-to-one unidirectional relationship
>
> Now we may ask any fan “Who is your favorite signer?”.
>
> **Many-to-One (both directions)**
>
> ![](media/image14.png){width="4.010416666666667in" height="0.65625in"}
>
> Domain model of a many-to-one bidirectional relationship
>
> @Entity\
> class A {\
>    @Id int id;
>
>    [**@ManyToOne**](http://download.oracle.com/javaee/6/api/javax/persistence/ManyToOne.html)\
>    B **b**;\
> }
>
> @Entity\
> class B {\
>    @Id int id;
>
>    **[@OneToMany](http://download.oracle.com/javaee/6/api/javax/persistence/OneToMany.html)(mappedBy="b")**\
>    Collection&lt;A&gt; listOfA;\
> }
>
> ![](media/image11.png){width="3.3333333333333335in"
> height="1.2395833333333333in"}
>
> Relation model of a many-to-one bidirectional relationship
>
> **Example 4, Many-to-One bidirectional relationship in JPA**
>
> The children of a father: A child knows his father and the father
> knows his children.
>
> @Entity\
> public class Child implements Serializable {
>
>    @Id\
>    private int id;
>
>    private String name;
>
>    [**@ManyToOne**](http://download.oracle.com/javaee/6/api/javax/persistence/ManyToOne.html)\
>    private Father **father**;
>
> }
>
> @Entity\
> public class Father implements Serializable {
>
>    @Id\
>    private int id;
>
>    private String surname;
>
>    **[@OneToMany](http://download.oracle.com/javaee/6/api/javax/persistence/OneToMany.html)(mappedBy="father")**\
>    private Collection&lt;Child&gt; children;
>
> }
>
> ![](media/image15.png){width="4.6875in" height="2.0625in"}
>
> Physical description of a many-to-one bidirectional relationship
>
> ![](media/image16.png){width="3.8541666666666665in"
> height="1.1979166666666667in"}
>
> ER diagram of a many-to-one bidirectional relationship
>
> **One-to-Many (one direction)**
>
> ![](media/image17.png){width="3.9895833333333335in"
> height="0.6458333333333334in"}
>
> Domain model of a one-to-many unidirectional relationship
>
> It is the case when an entity has a set of characteristics.
>
> @Entity\
> class A {\
> @Id int id;
>
> // A join table is assumed.\
> [**@OneToMany**](http://download.oracle.com/javaee/6/api/javax/persistence/OneToMany.html)\
> Collection&lt;B&gt; listOfB;\
> }
>
> @Entity\
> class B {\
> @Id int id;\
> }
>
> ![](media/image18.png){width="4.6875in" height="1.1666666666666667in"}
>
> Relation model of a one-to-many unidirectional relationship
>
> Thus, when declaring an OneToMany annotation *without* a mappedBy
> element, then a join table is assumed.
>
> **Example 5, One-to-Many unidirectional relationship in JPA**
>
> A library which provides facilities.
>
> @Entity\
> public class Library implements Serializable {
>
> @Id\
> private int id;
>
> private String name;
>
> [**@OneToMany**](http://download.oracle.com/javaee/6/api/javax/persistence/OneToMany.html)\
> private Collection&lt;Facility&gt; facilities;
>
> }
>
> @Entity\
> public class Facility implements Serializable {
>
> @Id\
> private String code;
>
> private String description;
>
> }
>
> ![](media/image19.png){width="4.6875in" height="2.7291666666666665in"}
>
> Physical description of a one-to-many unidirectional relationship
>
> ![](media/image20.png){width="3.6041666666666665in" height="2.75in"}
>
> ER diagram of an one-to-many unidirectional relationship
>
> Now we can ask a library “What facilities do you provide?”. The answer
> could be “Scanning, Printing and Photocopying”. This set of facilities
> may be provided by one or more libraries at the same time.
>
> If using a join table is not what you want, then you should use the
> next relationship.
>
> **One-to-Many (both directions)**
>
> It is exactly the same with Many-to-One (both directions), looking via
> a mirror.
>
> ![](media/image21.png){width="4.0in" height="0.6354166666666666in"}
>
> Domain model of a one-to-many bidirectional relationship
>
> @Entity\
> class A {\
>    @Id int id;
>
>    [**@OneToMany**](http://download.oracle.com/javaee/6/api/javax/persistence/OneToMany.html)(mappedBy="a")\
>    Collection&lt;B&gt; listOfB;\
> }
>
> @Entity\
> class B {\
>    @Id int id;
>
>    [**@ManyToOne**](http://download.oracle.com/javaee/6/api/javax/persistence/ManyToOne.html)\
>    A a;\
> }
>
> ![](media/image7.png){width="3.3229166666666665in"
> height="1.2395833333333333in"}
>
> Relation model of an one-to-many bidirectional relationship
>
> **Example 6, One-to-Many bidirectional relationship in JPA**
>
> A manager who manages projects.
>
> @Entity\
> public class Manager implements Serializable {
>
>    @Id\
>    private int id;
>
>    private String name;
>
>    **[@OneToMany](http://download.oracle.com/javaee/6/api/javax/persistence/OneToMany.html)(mappedBy="manager")**\
>    private Collection&lt;Project&gt; projects;
>
> }
>
> @Entity\
> public class Project implements Serializable {
>
>    @Id\
>    private int id;
>
>    private String title;
>
>    [**@ManyToOne**](http://download.oracle.com/javaee/6/api/javax/persistence/ManyToOne.html)\
>    private Manager manager;
>
> }
>
> ![](media/image22.png){width="4.6875in" height="2.0208333333333335in"}
>
> Physical description of a one-to-many bidirectional relationship
>
> ![](media/image23.png){width="3.6770833333333335in"
> height="1.1979166666666667in"}
>
> ER diagram of an one-to-many bidirectional relationship
>
> **Many-to-Many (both directions)**
>
> ![](media/image24.png){width="4.0in" height="0.6458333333333334in"}
>
> Domain model of a many-to-many bidirectional relationship
>
> @Entity\
> class A {\
>    @Id int id;
>
>    [**@ManyToMany**](http://download.oracle.com/javaee/6/api/javax/persistence/ManyToMany.html)\
>    Collection&lt;B&gt; **listOfB**;\
> }
>
> @Entity\
> class B {\
>    @Id\
>    int id;
>
>    **[@ManyToMany](http://download.oracle.com/javaee/6/api/javax/persistence/ManyToMany.html)(mappedBy="listOfB")**\
>    Collection listOfA; }
>
> Of course, a join table is used.
>
> ![](media/image25.png){width="4.6875in" height="1.1770833333333333in"}
>
> Relation model of a many-to-many bidirectional relationship
>
> Note: In a birectional many-to-many relationship we
> should *always* include the mappedBy element to either of the sides.
> This ensures that exactly one join table is used.
>
> **Example 7, Many-to-Many bidirectional relationship in JPA**
>
> An engineer works in many projects. A project occupies many engineers.
> This is a classic many-to-many relationship. Moreover it expands to
> both directions, as:

-   An engineer should in which projects he is working.

-   The project should know the engineers it occupies.

> @Entity\
> public class Engineer implements Serializable {
>
>    @Id\
>    private int id;
>
>    private String name;
>
>    [**@ManyToMany**](http://download.oracle.com/javaee/6/api/javax/persistence/ManyToMany.html)\
>    @JoinTable(name="ENGINEER\_PROJECT",\
>               joinColumns=@JoinColumn(name="ENGINEER\_ID"),\
>               inverseJoinColumns=@JoinColumn(name="PROJECT\_ID"))\
>    private Collection&lt;Project&gt; **projects**;
>
> }
>
> @Entity\
> public class Project implements Serializable {
>
>    @Id\
>    private int id;
>
>    private String title;
>
>    **[@ManyToMany](http://download.oracle.com/javaee/6/api/javax/persistence/ManyToMany.html)(mappedBy="projects")**\
>    private Collection&lt;Engineer&gt; engineers;
>
> }
>
> ![](media/image26.png){width="4.6875in" height="3.1770833333333335in"}
>
> Physical description of a many-to-many bidirectional relationship
>
> ![](media/image27.png){width="4.6875in" height="0.9270833333333334in"}
>
> ER diagram of a many-to-many bidirectional relationship
>
> **Pitfall: Many-to-Many (one direction)**
>
> Not specifying the mappedBy element in a many-to-many relationship,
> assumes two join tables and should be avoided.
>
> @Entity\
> class A {\
>    @Id int id;
>
>    [**@ManyToMany**](http://download.oracle.com/javaee/6/api/javax/persistence/ManyToMany.html)\
>    Collection&lt;B&gt; listOfB;\
> }
>
> @Entity\
> class B {\
>    @Id int id;
>
>    [**@ManyToMany**](http://download.oracle.com/javaee/6/api/javax/persistence/ManyToMany.html)\
>    Collection&lt;A&gt; listOfA;\
> }
>
> The same happens when the ManyToMany annotation is ommitted on one
> side.
>
> @Entity\
> class A {\
>    @Id int id;
>
>    [**@ManyToMany**](http://download.oracle.com/javaee/6/api/javax/persistence/ManyToMany.html)\
>    Collection&lt;B&gt; listOfB;\
> }
>
> @Entity\
> class B {\
>    @Id int id;
>
>    Collection&lt;A&gt; listOfA;\
> }
>
> ![](media/image28.png){width="4.6875in" height="3.0520833333333335in"}
>
> Relation model of two many-to-many unidirectional relationship
>
> To avoid this pitfall, I would follow the instructions
> of [Many-to-Many (both
> directions)](https://nikojava.wordpress.com/2011/08/04/essential-jpa-relationships/#jpa-relations-7) relationship.
>
>  
>
> From
> &lt;<https://nikojava.wordpress.com/2011/08/04/essential-jpa-relationships/>&gt;

 

 

Spring JPA Config

Thursday, January 21, 2016

10:18

 

If you want to configure Spring Data JPA by using XML configuration (and
use the configuration described in the book), you have to follow these
steps:

1.  Configure the data source bean.

2.  Configure the entity manager factory bean.

3.  Configure the transaction manager bean.

4.  Enable annotation driven transaction management.

5.  Configure Spring Spring Data JPA.

The application context configuration
(*applicationContext-persistence.xml*) file looks as follows:

&lt;?xml version="1.0" encoding="UTF-8"?&gt;\
&lt;beans xmlns="http://www.springframework.org/schema/beans"\
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"\
xmlns:jpa="http://www.springframework.org/schema/data/jpa"\
xmlns:tx="http://www.springframework.org/schema/tx"\
xmlns:context="http://www.springframework.org/schema/context"\
xsi:schemaLocation="http://www.springframework.org/schema/beans\
<http://www.springframework.org/schema/beans/spring-beans.xsd>\
<http://www.springframework.org/schema/data/jpa>\
<http://www.springframework.org/schema/data/jpa/spring-jpa-1.0.xsd>\
<http://www.springframework.org/schema/tx>\
<http://www.springframework.org/schema/tx/spring-tx-3.1.xsd>\
<http://www.springframework.org/schema/context>\
<http://www.springframework.org/schema/context/spring-context-3.1.xsd>"&gt;

&lt;!-- Configure the data source bean --&gt;\
&lt;jee:jndi-lookup id="dataSource"
jndi-name="java:comp/env/jdbc/CustomerSupport"/&gt;

&lt;!-- Create default configuration for Hibernate --&gt;\
&lt;bean id="hibernateJpaVendorAdapter"\
class="org.springframework.orm.jpa.vendor.HibernateJpaVendorAdapter"/&gt;

&lt;!-- Configure the entity manager factory bean --&gt;\
&lt;bean id="entityManagerFactory"\
class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean"&gt;\
&lt;property name="dataSource" ref="dataSource"/&gt;\
&lt;property name="jpaVendorAdapter"
ref="hibernateJpaVendorAdapter"/&gt;\
&lt;!-- Set JPA properties --&gt;\
&lt;property name="jpaProperties"&gt;\
&lt;props&gt;\
&lt;prop
key="hibernate.dialect"&gt;org.hibernate.dialect.MySQL5InnoDBDialect&lt;/prop&gt;\
&lt;prop
key="javax.persistence.schema-generation.database.action"&gt;none&lt;/prop&gt;\
&lt;prop key="hibernate.ejb.use\_class\_enhancer"&gt;true&lt;/prop&gt;\
&lt;/props&gt;\
&lt;/property&gt;\
&lt;!-- Set base package of your entities --&gt;\
&lt;property name="packagesToScan" value="foo.bar.model"/&gt;\
&lt;!-- Set share cache mode --&gt;\
&lt;property name="sharedCacheMode" value="ENABLE\_SELECTIVE"/&gt;\
&lt;!-- Set validation mode --&gt;\
&lt;property name="validationMode" value="NONE"/&gt;\
&lt;/bean&gt;

&lt;!-- Configure the transaction manager bean --&gt;\
&lt;bean id="transactionManager"\
class="org.springframework.orm.jpa.JpaTransactionManager"&gt;\
&lt;property name="entityManagerFactory"
ref="entityManagerFactory"/&gt;\
&lt;/bean&gt;

&lt;!-- Enable annotation driven transaction management --&gt;\
&lt;tx:annotation-driven/&gt;

&lt;!--\
Configure Spring Data JPA and set the base package of the\
repository interfaces\
--&gt;\
&lt;jpa:repositories base-package="foo.bar.repository"/&gt;\
&lt;/beans&gt;

 

From
&lt;<http://stackoverflow.com/questions/25049778/how-to-configure-spring-data-jpa-using-xml>&gt;

 

 

Spring Data JPA

Thursday, January 21, 2016

10:30

The goal of Spring Data repository abstraction is to significantly
reduce the amount of boilerplate code required to implement data access
layers for various persistence stores

 

The central interface in Spring Data repository abstraction
is Repository (probably not that much of a surprise). It takes the
domain class to manage as well as the id type of the domain class as
type arguments. This interface acts primarily as a marker interface to
capture the types to work with and to help you to discover interfaces
that extend this one. TheCrudRepository provides sophisticated CRUD
functionality for the entity class that is being managed.

 

On top of the CrudRepository there is
a PagingAndSortingRepository abstraction that adds additional methods to
ease paginated access to entities:

 

Accessing the second page of User by a page size of 20 you could simply
do something like this:

PagingAndSortingRepository&lt;User, Long&gt; repository = // … get
access to a bean\
Page&lt;User&gt; users = repository.findAll(new PageRequest(1, 20));

 

Defining repository interfaces

As a first step you define a domain class-specific repository interface.
The interface must extend Repository and be typed to the domain class
and an ID type. If you want to expose CRUD methods for that domain type,
extend CrudRepositoryinstead of Repository.

 

Typically, your repository interface will extend Repository,
CrudRepository or PagingAndSortingRepository. Alternatively, if you do
not want to extend Spring Data interfaces, you can also annotate your
repository interface with @RepositoryDefinition. Extending
CrudRepository exposes a complete set of methods to manipulate your
entities. If you prefer to be selective about the methods being exposed,
simply copy the ones you want to expose from CrudRepository into your
domain repository.

 

 

*Selectively exposing CRUD methods*

@NoRepositoryBean\
interface MyBaseRepository&lt;T, ID extends Serializable&gt; extends
Repository&lt;T, ID&gt; {

T findOne(ID id);

T save(T entity);\
}

interface UserRepository extends MyBaseRepository&lt;User, Long&gt; {\
User findByEmailAddress(EmailAddress emailAddress);\
}

In this first step you defined a common base interface for all your
domain repositories and exposed findOne(…) as well as save(…).These
methods will be routed into the base repository implementation of the
store of your choice provided by Spring Data ,e.g. in the case if
JPA SimpleJpaRepository, because they are matching the method signatures
inCrudRepository. So the UserRepository will now be able to save users,
and find single ones by id, as well as triggering a query to
find Users by their email address.

  Note, that the intermediate repository interface is annotated with @NoRepositoryBean. Make sure you add that annotation to all repository interfaces that Spring Data should not create instances for at runtime.
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

Complete reference is in the pdf below

 

 

&lt;&lt;Spring Data JPA - Reference Documentation.pdf&gt;&gt;

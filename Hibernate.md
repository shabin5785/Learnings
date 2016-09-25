Basics

Thursday, January 21, 2016

12:07

 

> Hibernate is also a JPA provider, that means it implements the [Java
> Persistence API
> (JPA)](http://www.javacodegeeks.com/2015/02/jpa-tutorial.html). JPA is
> a vendor independent specification for mapping Java objects to the
> tables of relational databases. 
>
>  
>
> Hibernate consists of three different components:

-   **Entities**: The classes that are mapped by Hibernate to the tables
    > of a relational database system are simple Java classes (Plain Old
    > Java Objects).

-   **Object-relational metadata**: The information how to map the
    > entities to the relational database is either provided by
    > annotations (since Java 1.5) or by legacy XML-based
    > configuration files. The information in these files is used at
    > runtime to perform the mapping to the data store and back to the
    > Java objects.

-   **Hibernate Query Language (HQL)**: When using Hibernate, queries
    > send to the database do not have to be formulated in native SQL
    > but can be specified using Hibernate’s query language. As these
    > queries are translated at runtime into the currently used dialect
    > of the chose product, queries formulated in HQL are independent
    > from the SQL dialect of a specific vendor

>  
>
> Configuration configuration = new Configuration();
>
> configuration.configure("hibernate.cfg.xml");
>
>  
>
> ServiceRegistry serviceRegistry = new
> StandardServiceRegistryBuilder().applySettings(configuration.getProperties()).build();
>
>  
>
> sessionFactory = configuration.buildSessionFactory(serviceRegistry);
>
>  
>
> session = sessionFactory.openSession();
>
>  
>
>  
>
>  
>
> &lt;!--?xml version='1.0' encoding='utf-8'?--&gt;
>
> &lt;hibernate-configuration&gt;\
> &lt;session-factory&gt;\
> &lt;property
> name="connection.driver\_class"&gt;org.h2.Driver&lt;/property&gt;\
> &lt;property
> name="connection.url"&gt;jdbc:h2:\~/hibernate;AUTOCOMMIT=OFF&lt;/property&gt;\
> &lt;property name="connection.username"&gt;&lt;/property&gt;\
> &lt;property name="connection.password"&gt;&lt;/property&gt;\
> &lt;property name="connection.pool\_size"&gt;1&lt;/property&gt;\
> &lt;property
> name="dialect"&gt;org.hibernate.dialect.H2Dialect&lt;/property&gt;\
> &lt;property
> name="current\_session\_context\_class"&gt;thread&lt;/property&gt;\
> &lt;property
> name="cache.provider\_class"&gt;org.hibernate.cache.internal.NoCacheProvider&lt;/property&gt;\
> &lt;property name="show\_sql"&gt;true&lt;/property&gt;\
> &lt;property name="format\_sql"&gt;true&lt;/property&gt;\
> &lt;property name="hbm2ddl.auto"&gt;create&lt;/property&gt;\
> &lt;mapping resource="Project.hbm.xml"&gt;\
> &lt;/mapping&gt;&lt;/session-factory&gt;\
> &lt;/hibernate-configuration&gt;
>
>  
>
> From
> &lt;<http://www.javacodegeeks.com/2015/03/hibernate-tutorial.html>&gt;
>
>  
>
>  
>
>  
>
> The following code demonstrates how to obtain a new transaction from
> the session and how to start and commit it:
>
>  
>
> try {\
>         Transaction transaction = session.getTransaction();\
>         transaction.begin();\
>         ...\
>         transaction.commit();\
> } catch (Exception e) {\
>         if (session.getTransaction().isActive()) {\
>                 session.getTransaction().rollback();\
>         }\
>         throw e;\
> }
>
>  
>
>  Hibernate supports the following mapping strategies:

-   **Single table per class**: Both superclass and subclass are mapped
    > to the same table. An additional column marks whether the row is
    > an instance of the superclass or subclass and fields that are not
    > present in the superclass are left empty.

-   **Joined subclass**: This strategy uses a separate table for each
    > class whereas the table for the subclass only stores the fields
    > that are not present in the superclass. To retrieve all values for
    > an instance of the subclass, a join between the two tables has to
    > be performed.

-   **Table per class**: This strategy also uses a separate table for
    > each class but stores in the table for the subclass also the
    > fields of the superclass. With this strategy one row in the
    > subclass table contains all values and in order to retrieve all
    > values no join statement is necessary.

>  
>
> **Single table per class**
>
> The first difference is the introduction of the **discriminator**
> column. As mentioned above this column stores the information of which
> type the current instance is. In our case we call it PERSON\_TYPE and
> let for better readability a string denote the actual type.
>
>  
>
> &lt;!--?xml version="1.0"?--&gt;
>
> &lt;hibernate-mapping package="hibernate.entity"&gt;\
> &lt;class name="Person" table="T\_PERSON"&gt;\
> &lt;id name="id" column="ID"&gt;\
> &lt;generator class="native"&gt;\
> &lt;/generator&gt;&lt;/id&gt;\
> &lt;discriminator column="PERSON\_TYPE" type="string"&gt;\
> &lt;property name="firstName" column="FIRST\_NAME"&gt;\
> &lt;property name="lastName" column="LAST\_NAME"&gt;\
> &lt;subclass name="Geek" extends="Person"&gt;\
> &lt;property name="favouriteProgrammingLanguage"
> column="FAV\_PROG\_LANG"&gt;\
> &lt;/property&gt;&lt;/subclass&gt;\
> &lt;/property&gt;&lt;/property&gt;&lt;/discriminator&gt;&lt;/class&gt;\
> &lt;/hibernate-mapping&gt;
>
>  
>
>  
>
>  
>
> sql&gt; select \* from t\_person;\
> ID | PERSON\_TYPE | FIRST\_NAME | LAST\_NAME | FAV\_PROG\_LANG\
> 1 | hibernate.entity.Person | Homer | Simpson | null\
> 2 | hibernate.entity.Geek | Gavin | Coffee | Java\
> 3 | hibernate.entity.Geek | Thomas | Micro | C\#\
> 4 | hibernate.entity.Geek | Christian | Cup | Java
>
>  
>
> **Joined subclass**
>
> Changing the mapping definition in a way that it looks like the
> following one, Hibernate will create for the superclass and the
> subclass a separate table:
>
>  
>
> &lt;!--?xml version="1.0"?--&gt;
>
> &lt;hibernate-mapping package="hibernate.entity"&gt;\
> &lt;class name="Person" table="T\_PERSON"&gt;\
> &lt;id name="id" column="ID"&gt;\
> &lt;generator class="native"&gt;\
> &lt;/generator&gt;&lt;/id&gt;\
> &lt;property name="firstName" column="FIRST\_NAME"&gt;\
> &lt;property name="lastName" column="LAST\_NAME"&gt;\
> &lt;joined-subclass name="Geek" table="T\_GEEK"&gt;\
> &lt;key column="ID\_PERSON"&gt;\
> &lt;property name="favouriteProgrammingLanguage"
> column="FAV\_PROG\_LANG"&gt;\
> &lt;/property&gt;&lt;/key&gt;&lt;/joined-subclass&gt;\
> &lt;/property&gt;&lt;/property&gt;&lt;/class&gt;\
> &lt;/hibernate-mapping&gt;
>
>  
>
> The XML element joined-subclass tells Hibernate to create the table
> T\_GEEK for the subclass Geek with the additional column ID\_PERSON.
> This additional key column stores a foreign key to the table T\_PERSON
> in order to assign each row in T\_GEEK to its parent row in T\_PERSON.
>
>  
>
> **Table per class**
>
>  
>
> in contrast the table for the subclass contains also all columns of
> the superclass. Therewith one row in such a table contains all values
> to construct an instance of this type without the need to join
> additional data from the parent table. On huge data set this can
> improve the performance of queries as joins need to find additionally
> the corresponding rows in the parent table. This additional lookup
> costs time that is circumvented with this approach.
>
>  
>
> &lt;!--?xml version="1.0"?--&gt;
>
> &lt;hibernate-mapping package="hibernate.entity"&gt;\
> &lt;class name="Person" table="T\_PERSON"&gt;\
> &lt;id name="id" column="ID"&gt;\
> &lt;generator class="sequence"&gt;\
> &lt;/generator&gt;&lt;/id&gt;\
> &lt;property name="firstName" column="FIRST\_NAME"&gt;\
> &lt;property name="lastName" column="LAST\_NAME"&gt;\
> &lt;union-subclass name="Geek" table="T\_GEEK"&gt;\
> &lt;property name="favouriteProgrammingLanguage"
> column="FAV\_PROG\_LANG"&gt;\
> &lt;/property&gt;&lt;/union-subclass&gt;\
> &lt;/property&gt;&lt;/property&gt;&lt;/class&gt;\
> &lt;/hibernate-mapping&gt;
>
>  
>
> Another important change with regard to the other approaches is
> contained in the line that defines the id generator. As the other
> approaches use a native generator, which falls back on H2 to an
> identity column, this approach requires an id generator that creates
> identities that are unique for both tables (T\_PERSON and T\_GEEK).
>
> The identity column is just a special type of column that
> automatically creates for each row a new id. But with two tables we
> have also two identity columns and therewith the ids in the T\_PERSON
> table can be the same as in the T\_GEEK table. This conflicts with the
> requirement that an entity of type Geek can be created just by reading
> one row of the table T\_GEEK and that the identifiers for all persons
> and geeks are unique. Therefore we are using a sequence instead of an
> identity column by switching the value for the class attribute from
> native to sequence
>
>  
>
>  
>
> Relationships
>
>  

-   **One to one**: This denotes a simple relationship in which one
    > entity of type A belongs exactly to one entity of type B.

-   **Many to one**: As the name indicates, this relationship
    > encompasses the case that an entity of type A has many child
    > entities of type B.

-   **Many to many**: In this case there can be many entities of type A
    > that belong to many entities of type B.

>  
>
> **One to one**
>
>  
>
> public class IdCard
>
>  
>
> public class Person {
>
> private IdCard idCard;
>
> }
>
> &lt;hibernate-mapping package="hibernate.entity"&gt;
>
> &lt;class name="IdCard" table="T\_ID\_CARD"&gt;
>
> &lt;id name="id" column="ID"&gt;
>
> &lt;generator class="sequence"&gt;
>
> &lt;/generator&gt;&lt;/id&gt;
>
> &lt;/class&gt;
>
> &lt;class name="Person" table="T\_PERSON"&gt;
>
> &lt;id name="id" column="ID"&gt;
>
> &lt;generator class="sequence"&gt;
>
> &lt;/generator&gt;&lt;/id&gt;
>
> &lt;property name="firstName" column="FIRST\_NAME"&gt;
>
> &lt;property name="lastName" column="LAST\_NAME"&gt;
>
> &lt;many-to-one name="idCard" column="ID\_ID\_CARD" unique="true"&gt;
>
> &lt;union-subclass name="Geek" table="T\_GEEK"&gt;
>
> &lt;property name="favouriteProgrammingLanguage"
> column="FAV\_PROG\_LANG"&gt;
>
> &lt;/property&gt;&lt;/union-subclass&gt;
>
> &lt;/many-to-one&gt;&lt;/property&gt;&lt;/property&gt;&lt;/class&gt;
>
> &lt;/hibernate-mapping&gt;
>
>  
>
>  
>
> On the other hand the Person mapping now contains the new XML element
> many-to-one and references with its attribute name the field of the
> class Person that stores the reference to the IdCard. The optional
> attribute column lets us specify the exact name of the foreign key
> column in the table T\_PERSON that links to the person’s id card. As
> this relation should be of type “one to one” we have to set the
> attribute unique to true
>
>  
>
> one might argue why we have to pass both instances to the save()
> method of the session. This point is justified, as Hibernate allows to
> define that certain operation should be “cascaded” when processing a
> complete entity graph. To enable cascading for the relationship to the
> IdCard we can simply add the attribute cascade to the many-to-one
> element in the mapping file
>
>  
>
> &lt;many-to-one name="idCard" column="ID\_ID\_CARD" unique="true"
> cascade="all"&gt;&lt;/many-to-one&gt;
>
>  
>
> Using the value all tells Hibernate to cascade all types of
> operations. As this is not always the preferred way to handle
> relationships between entities, one can also select only specific
> operations
>
>  
>
> &lt;many-to-one name="idCard" column="ID\_ID\_CARD" unique="true"
> cascade="save-update,refresh"&gt;
>
> &lt;/many-to-one&gt;
>
>  
>
>  
>
> Instead of using the method save() one could also use in this use case
> the method **saveOrUpdate**(). The purpose of the method
> saveOrUpdate() is that it can be also used to update an existing
> entity. A subtle difference between both implementations is the fact
> that the save() methods returns the created identifier of the new
> entity:
>
> *Long personId = (Long) session.save(person);*
>
> This is helpful when writing for example server side code that should
> return this identifier to the caller of the method. On the other hand
> the method update() does not return the identifier as it assumes that
> the entity has already been stored to the data store and therefore
> must have an identifier. Trying to update an entity without an
> identifier will throw an exception:
>
> org.hibernate.TransientObjectException: The given object has a null
> identifier: ...
>
> Therefore saveOrUpdate() helps in cases where one wants to omit code
> that decides whether the entity has already been stored or not.
>
>  
>
>  
>
> **One to Many**
>
> public class Phone
>
> public class Person {
>
>         private Set&lt;phone&gt; phones = new HashSet&lt;phone&gt;();
>
> }
>
>  
>
>  
>
>  
>
> &lt;hibernate-mapping package="hibernate.entity"&gt;
>
> ...
>
> &lt;class name="Phone" table="T\_PHONE"&gt;
>
> &lt;id name="id" column="ID"&gt;
>
> &lt;generator class="sequence"&gt;
>
> &lt;/generator&gt;&lt;/id&gt;
>
> &lt;property name="number" column="NUMBER"&gt;
>
> &lt;many-to-one name="person" column="ID\_PERSON" unique="false"
> cascade="all"&gt;
>
> &lt;/many-to-one&gt;&lt;/property&gt;&lt;/class&gt;
>
> &lt;class name="Person" table="T\_PERSON"&gt;
>
> &lt;id name="id" column="ID"&gt;
>
> &lt;generator class="sequence"&gt;
>
> &lt;/generator&gt;&lt;/id&gt;
>
> &lt;discriminator column="PERSON\_TYPE" type="string"&gt;
>
> &lt;property name="firstName" column="FIRST\_NAME"&gt;
>
> &lt;property name="lastName" column="LAST\_NAME"&gt;
>
> &lt;many-to-one name="idCard" column="ID\_ID\_CARD" unique="true"
> cascade="all"&gt;
>
> &lt;subclass name="Geek" extends="Person"&gt;
>
> &lt;property name="favouriteProgrammingLanguage"
> column="FAV\_PROG\_LANG"&gt;
>
> &lt;/property&gt;&lt;/subclass&gt;
>
> &lt;/many-to-one&gt;&lt;/property&gt;&lt;/property&gt;&lt;/discriminator&gt;&lt;/class&gt;
>
> &lt;/hibernate-mapping&gt;
>
>  
>
> **Many to Many**
>
> public class Project
>
> public class Geek extends Person {
>
> private String favouriteProgrammingLanguage;
>
> private Set&lt;project&gt; projects = new HashSet&lt;project&gt;();
>
> }
>
>  
>
>  
>
> &lt;hibernate-mapping package="hibernate.entity"&gt;
>
> ...
>
> &lt;class name="Project" table="T\_PROJECT"&gt;
>
> &lt;id name="id" column="ID"&gt;
>
> &lt;generator class="sequence"&gt;
>
> &lt;/generator&gt;&lt;/id&gt;
>
> &lt;property name="title" column="TITLE"&gt;
>
> &lt;set name="geeks" table="T\_GEEKS\_PROJECTS"&gt;
>
> &lt;key column="ID\_PROJECT"&gt;
>
> &lt;many-to-many column="ID\_GEEK" class="Geek"&gt;
>
> &lt;/many-to-many&gt;&lt;/key&gt;&lt;/set&gt;
>
> &lt;/property&gt;&lt;/class&gt;
>
> &lt;class name="Person" table="T\_PERSON"&gt;
>
> &lt;id name="id" column="ID"&gt;
>
> &lt;generator class="sequence"&gt;
>
> &lt;/generator&gt;&lt;/id&gt;
>
> &lt;discriminator column="PERSON\_TYPE" type="string"&gt;
>
> &lt;property name="firstName" column="FIRST\_NAME"&gt;
>
> &lt;property name="lastName" column="LAST\_NAME"&gt;
>
> &lt;many-to-one name="idCard" column="ID\_ID\_CARD" unique="true"
> cascade="all"&gt;
>
> &lt;subclass name="Geek" extends="Person"&gt;
>
> &lt;property name="favouriteProgrammingLanguage"
> column="FAV\_PROG\_LANG"&gt;
>
> &lt;set name="projects" inverse="true"&gt;
>
> &lt;key column="ID\_GEEK"&gt;
>
> &lt;many-to-many column="ID\_PROJECT" class="Project"&gt;
>
> &lt;/many-to-many&gt;&lt;/key&gt;&lt;/set&gt;
>
> &lt;/property&gt;&lt;/subclass&gt;
>
> &lt;/many-to-one&gt;&lt;/property&gt;&lt;/property&gt;&lt;/discriminator&gt;&lt;/class&gt;
>
> &lt;/hibernate-mapping&gt;
>
>  Component
>
> Object-Oriented design rules suggest to extract commonly used fields
> to a separate class. The Project class above for example misses still
> a start and end date. But as such a period of time can be used for
> other entities as well, we can create a new class called Period that
> encapsulates the two fields startDate and endDate:
>
>  
>
> But we do not want that Hibernate creates a separate table for the
> period as each Project should only have exactly one start and end date
> and we want to circumvent the additional join. In this case Hibernate
> can map the two fields in the embedded class Period to the same table
> as the class Project
>
>  
>
> &lt;hibernate-mapping package="hibernate.entity"&gt;
>
> ...
>
> &lt;class name="Project" table="T\_PROJECT"&gt;
>
> &lt;id name="id" column="ID"&gt;
>
> &lt;generator class="sequence"&gt;
>
> &lt;/generator&gt;&lt;/id&gt;
>
> &lt;property name="title" column="TITLE"&gt;
>
> &lt;set name="geeks" table="T\_GEEKS\_PROJECTS"&gt;
>
> &lt;key column="ID\_PROJECT"&gt;
>
> &lt;many-to-many column="ID\_GEEK" class="Geek"&gt;
>
> &lt;/many-to-many&gt;&lt;/key&gt;&lt;/set&gt;
>
> &lt;component name="period"&gt;
>
> &lt;property name="startDate" column="START\_DATE"&gt;
>
> &lt;property name="endDate" column="END\_DATE"&gt;
>
> &lt;/property&gt;&lt;/property&gt;&lt;/component&gt;
>
> &lt;/property&gt;&lt;/class&gt;
>
> ...
>
> &lt;/hibernate-mapping&gt;
>
>  
>
> Interceptors
>
> A project may come with the requirement that for each entity/table the
> timestamp of its creation and its last update should be tracked.
> Setting these two values for each entity on all insert and update
> operations is a fairly tedious task. Therefore Hibernate offers the
> ability to implement interceptors that are called before an insert or
> update operation is performed. This way the code to set the creation
> and update timestamp can be extracted to a single place in the code
> base and does not have to be copied to all locations where it would be
> necessary
>
> public class AuditInterceptor extends EmptyInterceptor {
>
> @Override\
>         public boolean onSave(Object entity, Serializable id,
> Object\[\] state,\
>                 String\[\] propertyNames, Type\[\] types) {\
>                 if (entity instanceof Auditable) {\
>                         for ( int i=0; i &lt; propertyNames.length;
> i++ ) {\
>                                 if ( "created".equals(
> propertyNames\[i\] ) ) {\
>                                         state\[i\] = new Date();\
>                                         return true;\
>                                 }\
>                         }\
>                         return true;\
>                 }\
>                 return false;\
>         }
>
> @Override\
>         public boolean onFlushDirty(Object entity, Serializable id,
> Object\[\] currentState,\
>                 Object\[\] previousState, String\[\] propertyNames,
> Type\[\] types) {\
>                 if (entity instanceof Auditable) {\
>                         for ( int i=0; i &lt; propertyNames.length;
> i++ ) {\
>                                 if ( "lastUpdate".equals(
> propertyNames\[i\] ) ) {\
>                                         currentState\[i\] = new
> Date();\
>                                         return true;\
>                                 }\
>                         }\
>                         return true;\
>                 }\
>                 return false;\
>         }\
> }
>
> As the class EmptyInterceptor already implements all methods defined
> in the interface Interceptor, we only have to override the methods
> onSave() and onFlushDirty(). In order to easily find all entities that
> have a field created and lastUpdate we extract the getter and setter
> methods for these entities into a separate interface called Auditable:
>
>  
>
> public interface Auditable {\
>         Date getCreated();\
>         void setCreated(Date created);\
>         Date getLastUpdate();\
>         void setLastUpdate(Date lastUpdate);\
> }
>
>  
>
> &lt;hibernate-mapping&gt;\
>         ...\
> &lt;class name="Project" table="T\_PROJECT"&gt;\
> &lt;id name="id" column="ID"&gt;\
> &lt;generator class="sequence"&gt;\
> &lt;/generator&gt;&lt;/id&gt;\
> &lt;property name="title" column="TITLE"&gt;\
> &lt;set name="geeks" table="T\_GEEKS\_PROJECTS"&gt;\
> &lt;key column="ID\_PROJECT"&gt;\
> &lt;many-to-many column="ID\_GEEK" class="Geek"&gt;\
> &lt;/many-to-many&gt;&lt;/key&gt;&lt;/set&gt;\
> &lt;component name="period"&gt;\
> &lt;property name="startDate" column="START\_DATE"&gt;\
> &lt;property name="endDate" column="END\_DATE"&gt;\
> &lt;/property&gt;&lt;/property&gt;&lt;/component&gt;\
> &lt;property name="created" column="CREATED" type="timestamp"&gt;\
> &lt;property name="lastUpdate" column="LAST\_UPDATE"
> type="timestamp"&gt;\
> &lt;/property&gt;&lt;/property&gt;&lt;/property&gt;&lt;/class&gt;\
>         ...\
> &lt;/hibernate-mapping&gt;
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

 

 

Basics2

Thursday, January 21, 2016

13:41

 

![](media/image1.jpg){width="5.802083333333333in" height="1.59375in"}

 

 

Advantages of Hibernate Framework

There are many advantages of Hibernate Framework. They are as follows:

**1) Opensource and Lightweight:** Hibernate framework is opensource
under the LGPL license and lightweight.

**2) Fast performance:** The performance of hibernate framework is fast
because cache is internally used in hibernate framework. There are two
types of cache in hibernate framework first level cache and second level
cache. First level cache is enabled bydefault.

**3) Database Independent query:** HQL (Hibernate Query Language) is the
object-oriented version of SQL. It generates the database independent
queries. So you don't need to write database specific queries. Before
Hibernate, If database is changed for the project, we need to change the
SQL query as well that leads to the maintenance problem.

**4) Automatic table creation:** Hibernate framework provides the
facility to create the tables of the database automatically. So there is
no need to create tables in the database manually.

**5) Simplifies complex join:** To fetch data form multiple tables is
easy in hibernate framework.

**6) Provides query statistics and database status:** Hibernate supports
Query cache and provide statistics about query and database status.

 

![](media/image2.jpg){width="3.9895833333333335in"
height="5.072916666666667in"}

 

 

![](media/image3.jpg){width="6.0in" height="4.177083333333333in"}

 

A simple Persistent class should follow some rules:

-   **A no-arg constructor:** It is recommended that you have a default
    > constructor at least package visibility so that hibernate can
    > create the instance of the Persistent class by newInstance()
    > method.

-   **Provide an identifier property (optional):** It is mapped to the
    > primary key column of the database.

-   **Declare getter and setter methods (optional):** The Hibernate
    > recognizes the method by getter and setter method names
    > by default.

-   **Prefer non-final class:** Hibernate uses the concept of proxies,
    > that depends on the persistent class. The application programmer
    > will not be able to use proxies for lazy association fetching.

>  

The mapping file name conventionally, should be class\_name.hbm.xml.
There are many elements of the mapping file.

-   **hibernate-mapping** is the root element in the mapping file.

-   **class** It is the sub-element of the hibernate-mapping element. It
    > specifies the Persistent class.

-   **id **It is the subelement of class. It specifies the primary key
    > attribute in the class.

-   **generator** It is the subelement of id. It is used to generate the
    > primary key. There are many generator classes such as assigned (It
    > is used if id is specified by the user), increment, hilo,
    > sequence, native etc. We will learn all the generator
    > classes later.

-   **property** It is the subelement of class that specifies the
    > property name of the Persistent class.

 

**@Entity** annotation marks this class as an entity.

**@Table** annotation specifies the table name where data of this entity
is to be persisted. If you don't use @Table annotation, hibernate will
use the class name as the table name bydefault.

**@Id** annotation marks the identifier for this entity.

**@Column** annotation specifies the details of the column for this
property or field. If @Column annotation is not specified, property name
will be used as the column name bydefault

 

**Generator**

The &lt;**generator**&gt; subelement of id used to generate the unique
identifier for the objects of persistent class. There are many generator
classes defined in the Hibernate Framework.

All the generator classes implements
the **org.hibernate.id.IdentifierGenerator [interface](http://www.javatpoint.com/interface-in-java)**.
The application programmer may create one's own generator classes by
implementing the IdentifierGenerator interface

 

assigned

It is the default generator strategy if there is no &lt;generator&gt;
element . In this case, application assigns the id.

 

 

increment

It generates the unique id only if no other process is inserting data
into this table. It generates **short**, **int** or **long** type
identifier. The first generated identifier is 1 normally and incremented
as 1

 

sequence

It uses the sequence of the database. if there is no sequence defined,
it creates a sequence automatically e.g. in case of Oracle database, it
creates a sequence named HIBERNATE\_SEQUENCE.

 

For defining your own sequence, use the param subelement of generator

 

hilo

It uses high and low algorithm to generate the id of type short, int and
long.

 

native

It uses identity, sequence or hilo depending on the database vendor

 

uuid

It uses 128-bit UUID algorithm to generate the id. The returned id is of
type String, unique within a network (because IP is used). The UUID is
represented in hexadecimal digits, 32 in length.

 

Hibernate Query Language (HQL)

 

 

Hibernate Query Language (HQL) is same as SQL (Structured Query
Language) but it doesn't depends on the table of the database. Instead
of table name, we use class name in HQL. So it is database independent
query language.

 

Advantage of HQL

There are many advantages of HQL. They are as follows:

-   database independent

-   supports polymorphic queries

-   easy to learn for Java Programmer

 

Caching in Hibernate

 

First Level Cache

Session object holds the first level cache data. It is enabled by
default. The first level cache data will not be available to entire
application. An application can use many session object.

Second Level Cache

SessionFactory object holds the second level cache data. The data stored
in the second level cache will be available to entire application. But
we need to enable it explicitely.

Second Level Cache implementations are provided by different vendors
such as:

-   EH (Easy Hibernate) Cache

-   Swarm Cache

-   OS Cache

-   JBoss Cache

 

 

Hibernate and Spring Integration

 

We can simply integrate hibernate application with spring application.

 

In hibernate framework, we provide all the database information
hibernate.cfg.xml file.

 

But if we are going to integrate the hibernate application with spring,
we don't need to create the hibernate.cfg.xml file. We can provide all
the information in the applicationContext.xml file.

The Spring framework provides HibernateTemplate class, so you don't need
to follow so many steps like create Configuration, BuildSessionFactory,
Session, beginning and committing transaction etc.

 

 

 

**applicationContext.xml**

In this file, we are providing all the informations of the database in
the **BasicDataSource** object. This object is used in
the**LocalSessionFactoryBean** class object, containing some other
informations such as mappingResources and hibernateProperties. The
object of **LocalSessionFactoryBean** class is used in the
HibernateTemplate class. Let's see the code of applicationContext.xml
file.

![](media/image4.png){width="3.9479166666666665in" height="4.78125in"}

 

 

 

&lt;?xml version="1.0" encoding="UTF-8"?&gt;

&lt;beans

xmlns="http://www.springframework.org/schema/beans"

xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

xmlns:p="http://www.springframework.org/schema/p"

xsi:schemaLocation="http://www.springframework.org/schema/beans

<http://www.springframework.org/schema/beans/spring-beans-3.0.xsd>"&gt;

&lt;bean id="dataSource"
class="org.apache.commons.dbcp.BasicDataSource"&gt;

&lt;property name="driverClassName"
value="oracle.jdbc.driver.OracleDriver"&gt;&lt;/property&gt;

&lt;property name="url"
value="jdbc:oracle:thin:@localhost:1521:xe"&gt;&lt;/property&gt;

&lt;property name="username" value="system"&gt;&lt;/property&gt;

&lt;property name="password" value="oracle"&gt;&lt;/property&gt;

&lt;/bean&gt;

&lt;bean id="mysessionFactory"
class="org.springframework.orm.hibernate3.LocalSessionFactoryBean"&gt;

&lt;property name="dataSource" ref="dataSource"&gt;&lt;/property&gt;

&lt;property name="mappingResources"&gt;

&lt;list&gt;

&lt;value&gt;employee.hbm.xml&lt;/value&gt;

&lt;/list&gt;

&lt;/property&gt;

&lt;property name="hibernateProperties"&gt;

&lt;props&gt;

&lt;prop
key="hibernate.dialect"&gt;org.hibernate.dialect.Oracle9Dialect&lt;/prop&gt;

&lt;prop key="hibernate.hbm2ddl.auto"&gt;update&lt;/prop&gt;

&lt;prop key="hibernate.show\_sql"&gt;true&lt;/prop&gt;

&lt;/props&gt;

&lt;/property&gt;

&lt;/bean&gt;

&lt;bean id="template"
class="org.springframework.orm.hibernate3.HibernateTemplate"&gt;

&lt;property name="sessionFactory"
ref="mysessionFactory"&gt;&lt;/property&gt;

&lt;/bean&gt;

&lt;bean id="d" class="com.javatpoint.EmployeeDao"&gt;

&lt;property name="template" ref="template"&gt;&lt;/property&gt;

&lt;/bean&gt;

&lt;/beans&gt;

 

 

 

 

 

You can enable many hibernate properties like automatic table creation
by hbm2ddl.auto etc. in applicationContext.xml file. Let's see the code:

 

&lt;property name="hibernateProperties"&gt;

&lt;props&gt;

&lt;prop
key="hibernate.dialect"&gt;org.hibernate.dialect.Oracle9Dialect&lt;/prop&gt;

&lt;prop key="hibernate.hbm2ddl.auto"&gt;update&lt;/prop&gt;

&lt;prop key="hibernate.show\_sql"&gt;true&lt;/prop&gt;

&lt;/props&gt;

 

 

 

 

 

 

 

 

 

 

 

 

Thursday, February 04, 2016

16:59

 

In an object-oriented application, persistence allows an object to
outlive the process that created it. The state of the object may be
stored to disk and an object with the same state re-created at some
point in the future. Modern relational databases provide a structured
representation of persistent data, enabling sorting, searching, and
aggregation of data. Database management systems are responsible for
managing concurrency and data integrity; they’re responsible for sharing
data between multiple users and multiple applications. A database
management system also provides data-level security.

 

An application with a domain model doesn’t work directly with the
tabular representation of the business entities; the applicatio n has
its own, object-oriented model of the business entities. If the database
has ITEM and BID tables, the Java application defines Item and Bid
classes. The business logic is never executed in the database (as an SQL
stored procedure), it’s implemented in Java. This allows business logic
to make use of sophisticated object-oriented concepts such as
inheritance and polymorphism

 

*Problem of granularity*

Classes in our domain object model come in a range of different levels
of granularity—from coarse-grained entity classes like User, to finer
grained classes like Address, right down to simple String-valued
properties such as zipcode. In contrast, just two levels of granularity
are visible at the level of the database: tables such as USER, along
with scalar columns such as ADDRESS\_ZIPCODE. This obviously isn’t as
flexible as our Java type system.

 

*problem of subtypes*

SQL provides no direct support for inheritance. as soon as we introduce
inheritance into the object model, we have the possibility of
polymorphism. as soon as we introduce

inheritance into the object model, we have the possibility of
polymorphism. Since SQL databases don’t provide a notion of inheritance,
it’s hardly surprising that they also lack an obvious way to represent a
polymorphic association

 

*problem of identity*

 

This problem can be seen when we consider two objects (for example, two
Users) and check if they’re identical. There are three ways to tackle
this problem, two in the

Java world and one in our SQL database.

 

*Problems relating to associations*

Object-oriented languages represent associations using object references
and collections of object references. In the relational world, an
association is represented

as a foreign key column, with copies of key values in several tables.
There are subtle differences between the two representations. Object
references are inherently directional; the association is from one
object to the other. If an association between objects should be
navigable in both directions, you must define the association twice,
once in each of the associated classes. On the other hand, foreign key
associations aren’t by nature directional. In fact, navigation has no
meaning for a relational data model, because you can create arbitrary
data associations with table joins and projection.

 

*problem of object graph navigation*

There is a fundamental difference in the way you access objects in Java
and in a relational database. In Java, when you access the billing
information of a user, you call
aUser.getBillingDetails().getAccountNumber(). This is the most natural
way to access object-oriented data and is often described as walking the
object graph. This mismatch in the way we access objects in Java and in
a relational database is perhaps the single most common source of
performance problems in Java applications

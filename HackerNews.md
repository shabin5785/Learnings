Concepts

Tuesday, June 16, 2015

10:06

Spring Boot

Spring Boot makes it easy to create stand-alone, production-grade Spring
based Applications that you can "just run". We take an opinionated view
of the Spring platform and third-party libraries so you can get started
with minimum fuss. Most Spring Boot applications need very little Spring
configuration

 

From &lt;<http://projects.spring.io/spring-boot/>&gt;

What is Docker?

Docker is an open platform for developers and sysadmins to build, ship,
and run distributed applications. Consisting of Docker Engine, a
portable, lightweight runtime and packaging tool, and Docker Hub, a
cloud service for sharing applications and automating workflows, Docker
enables apps to be quickly assembled from components and eliminates the
friction between development, QA, and production environments. As a
result, IT can ship faster and run the same app, unchanged, on laptops,
data center VMs, and any cloud.

 

From &lt;<https://www.docker.com/whatisdocker/>&gt;

 

> CAP theorem
>
> In [theoretical computer
> science](https://en.wikipedia.org/wiki/Theoretical_computer_science),
> the **CAP theorem**, also known as **Brewer's theorem**, states that
> it is impossible for a [distributed computer
> system](https://en.wikipedia.org/wiki/Distributed_computing) to
> simultaneously provide all three of the following
> guarantees:^[\[1\]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-Gilbert_Lynch-1)[\[2\]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-2)[\[3\]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-3)^

-   [*Consistency*](https://en.wikipedia.org/wiki/Consistency_(database_systems)) (all
    > nodes see the same data at the same time)

-   [*Availability*](https://en.wikipedia.org/wiki/Availability) (a
    > guarantee that every request receives a response about whether it
    > succeeded or failed)

-   [*Partition
    > tolerance*](https://en.wikipedia.org/wiki/Network_partitioning) (the
    > system continues to operate despite arbitrary partitioning due to
    > network failures)

>  
>
> From &lt;<https://en.wikipedia.org/wiki/CAP_theorem>&gt;

 

 

 

Nginx

 

**Nginx** (pronounced "engine x") is a [web
server](https://en.wikipedia.org/wiki/Web_server) with a strong focus on
high [concurrency](https://en.wikipedia.org/wiki/Concurrency_(computer_science)),
performance and
low [memory](https://en.wikipedia.org/wiki/Random-access_memory) usage.
It can also act as a [reverse
proxy](https://en.wikipedia.org/wiki/Reverse_proxy) server
for [HTTP](https://en.wikipedia.org/wiki/HTTP), [HTTPS](https://en.wikipedia.org/wiki/HTTPS), [SMTP](https://en.wikipedia.org/wiki/SMTP), [POP3](https://en.wikipedia.org/wiki/POP3),
and [IMAP](https://en.wikipedia.org/wiki/IMAP) protocols, as well as
a [load balancer](https://en.wikipedia.org/wiki/Load_balancer) and
an [HTTP cache](https://en.wikipedia.org/wiki/HTTP_cache).

 

From &lt;<https://en.wikipedia.org/wiki/Nginx>&gt;

 

 

Redis Geo

matt.sh/redis-geo

Location is important. Everything exists somewhere. Knowing where things
are is more and more important in the world. Every mobile phone is a
complex location tracking device these days, but how are we using all
the data we have access to now?

Everything is real time. Imagine you have users pushing high frequency
location updates. Maybe they are on a train and updating their location
once a second. How do you show their location updates in a live
view?Thanks to the magic of Geo Commands combined with Redis PubSub, you
can get notified of every location update by subscribing to a geo-themed
Redis PubSub channel.

From &lt;<https://matt.sh/redis-geo#_how-it-works>&gt;

 

New in Cassandra 3.0: Materialized Views

 

From
&lt;<http://www.datastax.com/dev/blog/new-in-cassandra-3-0-materialized-views>&gt;

 

[Should you write your back-end as an
API?](http://programmers.stackexchange.com/questions/287819/should-you-write-your-back-end-as-an-api)

 

From
&lt;<http://programmers.stackexchange.com/questions/287819/should-you-write-your-back-end-as-an-api>&gt;

 

Gitgraph.js is a simple JavaScript library which is meant to help you
visually presenting git branching stuff like a git workflow, a tricky
git command or whatever git tree you'd have in mind.

 

From &lt;<http://gitgraphjs.com/>&gt;

 

API Gateway

 There are a variety of different technologies that can be used to
implement a scalable API Gateway. On the JVM you can use one of the
NIO-based frameworks such Netty, Vertx, Spring Reactor, or
JBoss Undertow. One popular non-JVM option is Node.js, which is a
platform built on Chrome’s JavaScript engine. Another option is to
use [NGINX Plus](http://nginx.com/solutions/get-apis/)

 

From
&lt;<http://nginx.com/blog/building-microservices-using-an-api-gateway/>&gt;

 

Pattern: Server-side service discovery and Client side discovery

 

From
&lt;<http://microservices.io/patterns/server-side-discovery.html>&gt;

<http://microservices.io/patterns/client-side-discovery.html>

 

 

>  
>
> Pattern: Service registry
>
>  
>
> Implement a service registry, which is a database of services, their
> instances and their locations. Service instances are registered with
> the service registry on startup and deregistered on shutdown. Client
> of the service and/or routers query the service registry to find the
> available instances of a service.
>
> ***Examples***
>
> Examples of service registries (or technologies that are commonly used
> as service registries) include:

-   [Eureka](https://github.com/Netflix/eureka/wiki/Eureka-at-a-glance)

-   [Apache Zookeeper](http://zookeeper.apache.org/)

-   [Consul](https://consul.io/)

-   [Etcd](https://github.com/coreos/etcd)

> Some systems such as Kubernetes, Marathon and AWS ELB have an implicit
> service registry.
>
>  
>
> From &lt;<http://microservices.io/patterns/service-registry.html>&gt;
>
>  
>
>  

MicroServices Site

 

<http://microservices.io/index.html>

 

The ELK Stack: ElasticSearch, Logstash and Kibana

So what is this ELK we’re talking about? A combination of
elasticsearch’s search and analytics capabilities, Logstash as the logs
aggregator and Kibana for the fancy dashboard visualization. We’ve been
using it for a while, feeding it from Java through our logs and Redis,
and it’s in use both by developers and for BI. Today, elasticsearch is
pretty much built-in with Logstash, and Kibana is an elasticsearch
product as well, making integration and setup go easy peasy.

 

From
&lt;<http://blog.takipi.com/15-tools-to-use-when-deploying-code-to-production/?utm_source=blog&utm_medium=post-footer&utm_content=when-jvms-crash&utm_campaign=java>&gt;

 

s2n

In order to simplify our TLS implementation and as part of our support
for [strong encryption for
everyone](https://blogs.aws.amazon.com/security/post/Tx35449P4T7DJIA/Privacy-and-Data-Security),
we are pleased to announce availability of a new Open Source
implementation of the TLS protocol: s2n.  s2n is a library that has been
designed to be small, fast, with simplicity as a priority. s2n avoids
implementing rarely used options and extensions, and today is just more
than 6,000 lines of code. As a result of this, we’ve found that it is
easier to review s2n; we have already completed three external security
evaluations and penetration tests on s2n, a practice we will be
continuing.

 

From
&lt;<http://blogs.aws.amazon.com/security/post/TxCKZM94ST1S6Y/Introducing-s2n-a-New-Open-Source-TLS-Implementation>&gt;

 

Vert.x

Vert.x is event driven and non blocking. This means your app can handle
a lot of concurrency using a small number of kernel threads. Vert.x lets
your app scale with minimal hardware.

 

From &lt;<http://vertx.io/>&gt;

 

HATEOAS stands for **Hypertext As The Engine Of Application State**. It
means that hypertext should be used to find your way through the API. An
example:

GET /account/12345 HTTP/1.1

HTTP/1.1 200 OK\
**&lt;?xml version="1.0"?&gt;**\
&lt;account&gt;\
&lt;account\_number&gt;12345&lt;/account\_number&gt;\
&lt;balance currency="usd"&gt;100.00&lt;/balance&gt;\
&lt;link rel="deposit" href="/account/12345/deposit" /&gt;\
&lt;link rel="withdraw" href="/account/12345/withdraw" /&gt;\
&lt;link rel="transfer" href="/account/12345/transfer" /&gt;\
&lt;link rel="close" href="/account/12345/close" /&gt;\
&lt;/account&gt;

Apart from the fact that we have 100 dollars (US) in our account, we can
see 4 options: deposit more money, withdraw money, transfer money to
another account, or close our account. The "link"-tags allows us to find
out the URLs that are needed for the specified actions. Now, let's
suppose we didn't have 100 usd in the bank, but we actually are in the
red:

GET /account/12345 HTTP/1.1

HTTP/1.1 200 OK\
**&lt;?xml version="1.0"?&gt;**\
&lt;account&gt;\
&lt;account\_number&gt;12345&lt;/account\_number&gt;\
&lt;balance currency="usd"&gt;-25.00&lt;/balance&gt;\
&lt;link rel="deposit" href="/account/12345/deposit" /&gt;\
&lt;/account&gt;

Now we are 25 dollars in the red. Do you see that right now we have lost
many of our options, and only depositing money is valid? As long as we
are in the red, we cannot close our account, nor transfer or withdraw
any money from the account. The hypertext is actually telling us what is
allowed and what not: HATEOAS

- See more at:
<http://restcookbook.com/Basics/hateoas/#sthash.VjMWcHCV.dpuf>

 

From &lt;<http://restcookbook.com/Basics/hateoas/>&gt;

 

 

- See more at:
<http://restcookbook.com/Basics/hateoas/#sthash.VjMWcHCV.dpuf>

 

From &lt;<http://restcookbook.com/Basics/hateoas/>&gt;

 

 

> **Association** is a relationship where all objects have their own
> lifecycle and there is no owner. Let’s take an example of Teacher and
> Student. Multiple students can associate with single teacher and
> single student can associate with multiple teachers, but there is no
> ownership between the objects and both have their own lifecycle. Both
> can create and delete independently.
>
> **Aggregation** is a specialised form of Association where all objects
> have their own lifecycle, but there is ownership and child objects can
> not belong to another parent object. Let’s take an example of
> Department and teacher. A single teacher can not belong to multiple
> departments, but if we delete the department teacher object
> will *not* be destroyed. We can think about it as a “has-a”
> relationship.
>
> **Composition** is again specialised form of Aggregation and we can
> call this as a “death” relationship. It is a strong type of
> Aggregation. Child object does not have its lifecycle and if parent
> object is deleted, all child objects will also be deleted. Let’s take
> again an example of relationship between House and Rooms. House can
> contain multiple rooms - there is no independent life of room and any
> room can not belong to two different houses. If we delete the house -
> room will automatically be deleted. Let’s take another example
> relationship between Questions and Options. Single questions can have
> multiple options and option can not belong to multiple questions. If
> we delete questions options will automatically be deleted.
>
>  
>
> From
> &lt;<http://stackoverflow.com/questions/885937/difference-between-association-aggregation-and-composition>&gt;
>
>  
>
>  
>
>  

**Code Tools: jmh**

JMH is a Java harness for building, running, and analysing
nano/micro/milli/macro benchmarks written in Java and other languages
targetting the JVM.

 

From &lt;<http://openjdk.java.net/projects/code-tools/jmh/>&gt;

 

 

[Five Minute Introduction](http://www.jdbi.org/five_minute_intro)

[JDBI](http://jdbi.org/) is a SQL convenience library for Java. It
attempts to expose relational database access in idiommatic Java,

 

From &lt;<http://www.jdbi.org/>&gt;

 

 

 

Flynn is a unified platform that fixes everything that's wrong with the
process of deploying, scaling, and managing applications and databases.
It includes everything you need from containers and service discovery to
database appliances. So you take advantage of the best new technologies
without gluing a new stack together yourself.

 

From &lt;<https://flynn.io/>&gt;

 

 

 

 

 

DevOps

Thursday, June 25, 2015

10:02

 

<http://stackoverflow.com/questions/16647069/should-i-use-vagrant-or-docker-io-for-creating-an-isolated-environment>
Good read about vagrant vs docker

 

 

Java

Wednesday, July 01, 2015

11:39

 

Static methods OverRide

Static methods can not be overridden in the exact sense of the word, but
they can hide parent static methods

In practice it means that que compiler will decide which method to
execute at compile time, and not in runtime, as it does with overridden
instance methods.

For a neat example have a
look [here](http://geekexplains.blogspot.com/2008/06/can-you-override-static-methods-in-java.html).

And [this](http://download.oracle.com/javase/tutorial/java/IandI/override.html) is
java documentation explaining the difference
between **overriding** instance methods and**hiding** class (static)
methods.

**Overriding:** Overriding in Java simply means that the particular
method would be called based on the run time type of the object and not
on the compile time type of it (which is the case with overriden static
methods)

**Hiding:** Parent class methods that are static are not part of a child
class (although they are accessible), so there is no question of
overriding it. Even if you add another static method in a subclass,
identical to the one in its parent class, this subclass static method is
unique and distinct from the static method in its parent class.

 

From
&lt;<http://stackoverflow.com/questions/2475259/can-i-override-and-overload-static-methods-in-java>&gt;

 

**Association** is a relationship where all objects have their own
lifecycle and there is no owner. Let’s take an example of Teacher and
Student. Multiple students can associate with single teacher and single
student can associate with multiple teachers, but there is no ownership
between the objects and both have their own lifecycle. Both can create
and delete independently.

**Aggregation** is a specialised form of Association where all objects
have their own lifecycle, but there is ownership and child objects can
not belong to another parent object. Let’s take an example of Department
and teacher. A single teacher can not belong to multiple departments,
but if we delete the department teacher object will *not* be destroyed.
We can think about it as a “has-a” relationship.

**Composition** is again specialised form of Aggregation and we can call
this as a “death” relationship. It is a strong type of Aggregation.
Child object does not have its lifecycle and if parent object is
deleted, all child objects will also be deleted. Let’s take again an
example of relationship between House and Rooms. House can contain
multiple rooms - there is no independent life of room and any room can
not belong to two different houses. If we delete the house - room will
automatically be deleted. Let’s take another example relationship
between Questions and Options. Single questions can have multiple
options and option can not belong to multiple questions. If we delete
questions options will automatically be deleted.

 

From
&lt;<http://stackoverflow.com/questions/885937/difference-between-association-aggregation-and-composition>&gt;

 

 

 

Spring

Friday, July 10, 2015

10:11

 

Spring Security Filter explanation

 

<http://stackoverflow.com/questions/6725234/whats-the-point-of-spring-mvcs-delegatingfilterproxy>

 

Purpose of ContextLoderListener

 

<https://schoudari.wordpress.com/2012/07/23/purpose-of-contextloaderlistener-spring-mvc/>

 

<http://stackoverflow.com/questions/11815339/role-purpose-of-contextloaderlistener-in-spring>

 

 

Context files explanation

<http://stackoverflow.com/questions/14954931/my-application-could-not-open-servletcontext-resource>

 

SAML vs Oauth vs OpenID

 

<http://resources.infosecinstitute.com/saml-oauth-openid/>

 

 

New Concepts

Wednesday, August 26, 2015

11:05

 

Bootstrap 4: <https://scotch.io/bar-talk/whats-new-in-bootstrap-4>

 

What is JSX?

 

For those unfamiliar with React, JSX is an inline markup that looks like
HTML and gets transformed to JavaScript. A JSX expression starts with an
HTML-like open tag, and ends with the corresponding closing tag. JSX
tags support the XML self close syntax so you can optionally leave the
closing tag off.

 

JSX expressions evaluate to ReactElements. Think of them as shorthand
for calling \`React.createElement()\`.

 

&lt;div&gt;\
&lt;p\
onClick={ () =&gt; setEditMode(true) }\
style = { displayStyle }\
&gt;{ email }\
&lt;/p&gt;\
&lt;input\
type="email"\
onKeyUp={ this.onKeyUp }\
style = { editStyle }\
placeholder = { email } /&gt;\
&lt;/div&gt;

 

From
&lt;<https://medium.com/media/6e369797aa6db6a236b4c7406792ea24?maxWidth=700>&gt;

 

It’s actually a declarative syntax that’s used to express the virtual
DOM. JSX gets interpreted and converted to virtual DOM, which gets
diffed against the real DOM. Rather than rewrite the whole DOM tree,
only the differences get applied. That makes React renders fast.
Additionally, JSX builds in common protections against XSS attacks.

 

 

 

 

 

Perf Monitor

Wednesday, September 16, 2015

20:16

 

-   Java Melody (<https://github.com/javamelody/javamelody/wiki>) for
    > per application monitoring

    -   This is free open-source and can be injected into your
        > individual java applications/container

-   AppDynamics is used for full environment testing (i.e. across
    > multiple app)

    -   This is about £1400 per java agent (a java agent monitors just
        > one java application/container)

    -   Unfortunately all our current ALP licenses are in use. However
        > this is a really good tool and has been invaluable over the
        > past few years.

    -   If you did need licenses let me know and I can get you a quote
        > (we pay in sterling but our AppDynamics SaaS just like our AWS
        > servers are in US)

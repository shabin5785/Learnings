1

Wednesday, September 02, 2015

10:17

ApplicationContext.

This interface is used by Spring for storing all the environmental.
information with regard to an application being managed by Spring. This
interface extends another interface, **ListableBeanFactory**, which acts
as the provider for any Spring-managed beans instance

 

We declare the bean with the ID provider and the corresponding
implementation class. When Spring sees this bean definition during
ApplicationContext initialization, it will instantiate the class and
store it with the specified ID.

 

Dependency Lookup is also a form of IoC.

At its core, IoC, and therefore DI, aims to offer a simpler mechanism
for provisioning component dependencies often referred to as an object’s
collaborators) and managing these dependencies throughout their life
cycles.

 

With Dependency Lookup–style IoC, a component must acquire a reference
to a dependency, whereas with Dependency Injection, the dependencies are
injected into the component by the IoC container. Dependency Lookup
comes in two types: Dependency Pull and Contextualized Dependency Lookup
(CDL). Dependency Injection also has two common flavors: **Constructor
and Setter Dependency Injection**.

 

To a Java developer, Dependency Pull is the most familiar type of IoC.
In Dependency Pull, dependencies are pulled from a registry as required.
Anyone who has ever written code to access an EJB (2.1 or prior
versions) has used Dependency Pull (that is, via the JNDI API to look up
an EJB component). Spring also offers Dependency Pull as a mechanism for
retrieving the components that the framework manages;

 

ApplicationContext ctx = new
ClassPathXmlApplicationContext("META-INF/spring/app-context.xml");

MessageRenderer mr = ctx.getBean("renderer", MessageRenderer.class);

 

> ![](media/image1.png){width="4.645833333333333in"
> height="2.9479166666666665in"}

 

Contextualized Dependency Lookup (CDL) is similar, in some respects, to
Dependency Pull, but in CDL, lookup is performed against the container
that is managing the resource, not from some central registry, and it is
usually performed at some set point

 

**Constructor Dependency Injection** occurs when a component’s
dependencies are provided to it in its constructor(s). The component
declares a constructor or a set of constructors, taking as arguments its
dependencies, and the IoC container passes the dependencies to the
component when instantiation occurs.

 

In **Setter Dependency Injection**, the IoC container injects a
component’s dependencies via JavaBean-style setter methods. A
component’s setters expose the dependencies the IoC container can
manage.

 

Choosing which style of IoC to use—injection or lookup—is not usually a
difficult decision. In many cases, the type of IoC you use is mandated
by the container you are using. For instance, if you are using EJB 2.1
or prior versions, you must use lookup-style IoC (via JNDI) to obtain an
EJB from the JEE container. In Spring, aside from initial bean lookups,
your components and their dependencies are always wired together using
injection-style IoC.

 

Injection vs Lookup

Using injection has zero impact on your components’ code. The Dependency
Pull code, on the other hand, must actively obtain a reference to the
registry and interact with it to obtain the dependencies, and using CDL
requires your classes to implement a specific interface and look up all
dependencies manually. When you are using injection, the most your
classes have to do is allow dependencies to be injected by using either
constructors or setters.

Using injection, you are free to use your classes completely decoupled
from the IoC container that is supplying dependent objects with their
collaborators manually, whereas with lookup, your classes are always
dependent on the classes and interfaces defined by the container.
Another drawback with lookup is that it becomes very difficult to test
your classes in isolation from the container. Using injection, testing
your components is trivial, because you can

simply provide the dependencies yourself by using the appropriate
constructor or setter. All of these reasons aside, the biggest reason to
choose injection over lookup is that it makes your life easier. You
write substantially less code when you are using injection, and the code
that you do write is simple and can, in general, be automated by a good
IDE.

 

Setter Injection vs. Constructor Injection

 

Constructor Injection is particularly useful when you absolutely must
have an instance of the dependency class before your component is used.
Many containers, Spring included, provide a mechanism for ensuring that
all dependencies are defined when you use Setter Injection, but by using
Constructor

Injection, you assert the requirement for the dependency in a
container-agnostic manner. Constructor Injection also helps achieve the
use of immutable objects. Setter Injection is useful in a variety of
cases. If the component is exposing its dependencies to the container
but is happy to provide its own defaults, Setter Injection is usually
the best way to accomplish this. Another benefit of Setter Injection is
that it allows dependencies to be declared on an interface. Setter
injection also allows you to swap dependencies for a different
implementation on the fly without creating a new instance of the parent
component. Spring’s JMX support makes this possible. Perhaps the biggest
benefit of Setter Injection is that it is the least intrusive of the
injection mechanisms.

 

> ![](media/image2.png){width="5.90625in" height="2.0833333333333335in"}

 

In many environments, Spring cannot automatically wire up all of your
application components by using Dependency Injection, and you must use
Dependency Lookup to access the initial set of components. For example,
in stand-alone Java applications, you need to bootstrap Spring’s
container in the main() method and obtain the dependencies (via the
ApplicationContext interface) for processing programmatically. However,
when you are building web applications by using Spring’s MVC support,
Spring can avoid this by gluing your entire application together
automatically.

 

The core of Spring’s Dependency Injection container is the **BeanFactory
interface**. BeanFactory is responsible for managing components,
including their dependencies as well as their life cycles. In Spring,
the term **bean** is used to refer to any component managed by the
container. If your application needs only DI support, you can interact
with the Spring DI container via the BeanFactory interface. In this
case, your application must create an instance of a class that
implements the BeanFactory interface and configures it with bean and
dependency information. After this is complete, your application can
access the beans via BeanFactory and get on with its processing. In some
cases, all of this setup is handled automatically (for example, in a web
application, Spring’s **ApplicationContext will be bootstrapped by the
web container** during application startup via a Spring-provided
ContextLoaderListener class declared in the web.xml descriptor file).

 

**PropertiesBeanDefinitionReader** reads the bean definition from
properties files, while **XmlBeanDefinitionReader** reads from XML files

 

So you can identify your beans within BeanFactory, each bean can be
assigned an ID, a name, or both. A bean can also be instantiated without
any ID or name (known as an anonymous bean) or as an inner bean within
another bean. Each bean has at least one name but can have any number of
names (additional names are separated by commas). Any names after the
first are considered aliases for the same bean.

 

DefaultListableBeanFactory factory = new DefaultListableBeanFactory();

XmlBeanDefinitionReader rdr = new XmlBeanDefinitionReader(factory);

rdr.loadBeanDefinitions(new
ClassPathResource("META-INF/spring/xml-bean-factory-config.xml"));

Oracle oracle = (Oracle) factory.getBean("oracle");

 

 

When declaring a Spring XSD location, it’s a best practice to not
include the version number. This resolution is already handled for you
by Spring as the versioned XSD file is configured through a pointer in
the spring.schemas file. This file resides in the spring-beans module
defined as a dependency in your project. This also prevents you from
having to modify all of your bean files when upgrading to a new version
of Spring.

 

In Spring, t**he ApplicationContext interface is an extension to
BeanFactory**. In addition to DI services, ApplicationContext provides
other services, such as transaction and AOP service, message source for
nternationalization (i18n), and application event handling, to name a
few. **In developing Spring-based applications, it’s recommended that
you interact with Spring via the ApplicationContext interface**. Spring
supports the bootstrapping of applicationContext by manual coding
(instantiate it manually and load the appropriate configuration) or in a
web container environment via the

ContextLoaderListener

 

 

Originally, Spring supported defining beans either through properties or
an XML file. Since the release of JDK 5 and Spring’s support of Java
annotations, Spring (starting from Spring 2.5) also supports using Java
annotations when configuring ApplicationContext. So, which one is
better, XML or annotations?

Using an XML file can externalize all configuration from Java code,
while annotations allow the developer to define and view the DI setup
from within the

code. Spring also supports a mix of the two approaches in a single
ApplicationContext

 

To use Spring’s annotation support in your application, you need to
declare the tags.

 

&lt;context:component-scan
base-package="com.apress.prospring4.ch3.annotation" /&gt;

 

The &lt;context:component-scan&gt; tag tells Spring to scan the code for
injectable beans annotated with @Component, @Controller, @Repository,
and @Service as well as supporting the @Autowired and @Inject
annotations under the package (and all its subpackages) specified. In
the &lt;context:component-scan&gt; tag, multiple packages can be defined
by using either a comma, a semicolon, or a space as the delimiter.
Moreover, the tag supports inclusion and exclusion of a components scan
for more fine-grained control

 

 

you use Spring’s @Service annotation to specify that the bean provides
services that other beans may require, passing in the bean name as the
parameter. When bootstrapping Spring’s ApplicationContext, Spring will
seek out those components and instantiate the beans with the specified
names.

 

**Using either approach doesn’t affect the way you obtain the beans from
ApplicationContext**

 

The **GenericXmlApplicationContext** class implements the
ApplicationContext interface and is able to bootstrap Spring’s
ApplicationContext from the configurations defined in XML files

 

To **configure Setter Injection** by using XML configuration, you need
to specify &lt;property&gt; tags under the &lt;bean&gt; tag for each
&lt;property&gt; into which you want to inject a dependency

The p namespace provides a simplified way for defining Setter Injection

 

Since we declared the &lt;context:component-scan&gt; tag in the XML
configuration file, during the initialization of Spring’s
ApplicationContext, Spring will discover those **@Autowired**
annotations and inject the dependency as required.

 

Instead of @Autowired, you can also use
**@Resource**(name="messageProvider") to achieve the same result.
@Resource is one of the annotations in the JSR-250 standard that defines
a common set of Java annotations for use on both JSE and JEE platforms.
Different from @Autowired, the @Resource annotation supports the name
parameter for more fine-grained DI requirements. Additionally, Spring
supports use of the @Inject annotation introduced as part of JSR-299,
“Contexts and Dependency Injection for the Java EE Platform” (CDI).
@Inject is equivalent in behavior to Spring’s @Autowired annotation.

 

In this code, instead of using a &lt;property&gt; tag, we used a
**&lt;constructor-arg&gt;** tag. Because we are not passing in another
bean this time, just a String literal, we use the value attribute
instead of ref to specify the value for the constructor argument. When
you have more than one constructor argument or your class has more than
one constructor, you need to give each &lt;constructor-arg&gt; tag an
index attribute to specify the index of the argument, starting at 0, in
the constructor signature. It is always best to use the index attribute
whenever you are dealing with constructors that have multiple arguments,
to avoid confusion between the parameters and ensure that Spring picks
the correct constructor. In addition to the p namespace, as of Spring
3.1, you can also use the **c namespace**

 

**@Value,** to define the value to be injected into the constructor.
This is the way in Spring you inject values into a bean

 

public ConfigurableMessageProvider(@Value("Configurable message") String
message) {

this.message = message;

}

 

&lt;bean id="message" class="java.lang.String" c:\_0="This is a
configurable message"/&gt;

 

Here we define a bean with an ID of message and type of
java.lang.String. Notice that we also use the c namespace for
Constructor Injection to set the string value, and \_0 indicates the
index for the constructor argument. Have the bean declared; we can take
away the @Value annotation from the target bean

 

 

In some cases, Spring finds it impossible to tell which constructor you
want it to use for Constructor Injection. This usually arises when you
have two constructors with the same number of arguments and the types
used in the arguments are represented in exactly the same way

 

&lt;constructor-arg type=”int”&gt;

&lt;value&gt;90&lt;/value&gt;

&lt;/constructor-arg&gt;

 

This is done to avoid confusions in case of conflicting constructors.

 

Spring Expression Language (SpEL)

 

SpEL enables you to evaluate an expression dynamically and then use it
in Spring’s ApplicationContext. You can use the result for injection
into Spring beans.

 

&lt;bean id="injectSimpleConfig"
class="com.apress.prospring4.ch3.xml.InjectSimpleConfig"/&gt;

&lt;bean id="injectSimpleSpel"
class="com.apress.prospring4.ch3.xml.InjectSimpleSpel"

p:name="\#{injectSimpleConfig.name}"

&lt;/bean&gt;

 

When using annotation-style value injection, we just need to substitute
the value annotations with the SpEL expressions

 

Basically, using **@Component** has the same effect as **@Service**.
Both annotations are instructing Spring that the annotated class is a
candidate for autodetection using annotation-based configuration and
classpath scanning. However, since the InjectSimpleConfig class is
storing the application configuration, rather than providing a business
service, using @Component makes more sense. Practically, @Service is a
specialization of @Component, which indicates that the annotated class
is providing a business service to other layers within the application.

 

 

To configure Spring to inject one bean into another, you first need to
configure two beans: one to be injected and one to be the target of the
injection. Once this is done, you simply configure the injection by
using the **&lt;ref&gt;** tag on the target bean

 

An important point to note is that the **type being injected does not
have to be the exact type** defined on the target; the types just need
to be compatible. Compatible means that if the declared type on the
target is an interface, the injected type must implement this interface.
If the declared type is a class, the injected type must be either the
same type or a subtype

 

Local vs Ref

 

When you use the local attribute, it means that the &lt;ref&gt; tag only
looks at the bean’s id and never at any of its aliases. Moreover, the
bean definition should exist in the same XML configuration file. To
inject a bean by any name or import one from other XML configuration
files, use the bean attribute of the &lt;ref&gt; tag instead of the
local attribute.

 

Hierarchical Context

 

Spring supports a hierarchical structure for ApplicationContext so that
one context (and hence the associating BeanFactory) is considered the
parent of

another. By allowing ApplicationContexts to be nested, Spring allows you
to split your configuration into different files—a godsend on larger
projects with lots of beans. When nesting ApplicationContexts, Spring
allows beans in what is considered the child context to reference beans
in the parent context. ApplicationContext nesting using
GenericXmlApplicationContext is very simple to get a grip on. To nest
one GenericXmlApplicationContext inside another, simply call the
setParent() method in the child ApplicationContext

 

GenericXmlApplicationContext parent = new
GenericXmlApplicationContext();

parent.load("classpath:META-INF/spring/parent.xml");

parent.refresh();

GenericXmlApplicationContext child = new GenericXmlApplicationContext();

child.load("classpath:META-INF/spring/app-context-xml.xml");

child.setParent(parent);

child.refresh();

 

Inside the configuration file for the child ApplicationContext,
referencing a bean in the parent ApplicationContext works exactly like
referencing a bean in the child ApplicationContext, unless you have a
bean in the child ApplicationContext that shares the same name. In that
case, you simply replace the bean attribute of the ref attribute with
parent.

 

First, you can use the bean attribute to reference beans in both the
child and the parent ApplicationContexts. This makes it easy to
reference the beans transparently, allowing you to move beans between
configuration files as your application grows. The second point of
interest is that you can’t use the local attribute to refer to beans in
the parent ApplicationContext. The XML parser checks to see that the
value of the local attribute exists as a valid

element in the same file, preventing it from being used to reference
beans in the parent context.

 

Drawback of p tag

the target3 bean is not using the p namespace. While the p namespace
provides handy shortcuts, it does not provide all the capabilities as
when using property tags, such as referencing a parent bean. While we
show it as an example, its best to pick either the p namespace or
property tags to define your beans, rather than mixing styles

 

Using Collections for Injection

 

choose either &lt;list&gt;, &lt;map&gt;, &lt;set&gt;, or &lt;props&gt;
to represent a List, Map, Set, or Properties instance, and then you pass
in the individual items just as you would with any other injection.
**The &lt;props&gt; tag allows for only Strings to be passed in as the
value, because the Properties class allows only for property values to
be Strings**. When using &lt;list&gt;, &lt;map&gt;, or &lt;set&gt;, you
can use any tag you want when injecting into a property, even another
collection tag. This allows you to pass in a List of Maps, a Map of
Sets, or even a List of Maps of Sets of Lists

 

&lt;property name="map"&gt;

> &lt;map&gt;
>
> &lt;entry key="someValue"&gt;
>
> &lt;value&gt;Hello World!&lt;/value&gt;
>
> &lt;/entry&gt;
>
> &lt;entry key="someBean"&gt;
>
> &lt;ref local="oracle"/&gt;
>
> &lt;/entry&gt;
>
> &lt;/map&gt;

&lt;/property&gt;

&lt;property name="props"&gt;

> &lt;props&gt;
>
> &lt;prop key="firstName"&gt;Chris&lt;/prop&gt;
>
> &lt;prop key="secondName"&gt;Schaefer&lt;/prop&gt;
>
> &lt;/props&gt;

&lt;/property&gt;

&lt;property name="set"&gt;

> &lt;set&gt;
>
> &lt;value&gt;Hello World!&lt;/value&gt;
>
> &lt;ref local="oracle"/&gt;
>
> &lt;/set&gt;

&lt;/property&gt;

&lt;property name="list"&gt;

> &lt;list&gt;)

&lt;value&gt;Hello World!&lt;/value&gt;

&lt;ref local="oracle"/&gt;

&lt;/list&gt;

&lt;/property&gt;

 

 

Using Method Injection

Besides Constructor and Setter Injection, another less frequently used
DI feature that Spring provides is Method Injection. Spring’s Method
Injection capabilities come in two loosely related forms, Lookup Method
Injection and Method Replacement. Lookup Method Injection provides
another mechanism by which a bean can obtain one of its dependencies.
Method Replacement allows you to replace the implementation of any
method on a bean arbitrarily, without having to change the original
source code. To provide these two features, Spring uses the dynamic
bytecode enhancement capabilities of CGLIB.

 

Bean Naming

Spring supports quite a complex bean-naming structure that allows you
the flexibility to handle many situations. Every bean must have at least
one name that is unique within the containing ApplicationContext. Spring
follows a simple resolution process to determine what name is used for
the bean. If you give the &lt;bean&gt; tag an id attribute, the value of
that attribute is used as the name. If no id attribute is specified,
Spring looks for a name attribute, and if one is defined, it uses the
first name defined in the name attribute. (We say the first name because
it is possible to define multiple names within the name attribute; this
is covered in more detail shortly.) If neither the id nor the name
attribute is specified, Spring uses the bean’s class name as the name,
provided, of course, that no other bean is using the same class name. In
case multiple beans without an ID or the name defined are using the same
class name, Spring will throw an exception (of type
org.springframework.beans.factory.NoSuchBeanDefinitionException) on
injection during

ApplicationContext initialization.

 

Bean Name Aliasing

Spring allows a bean to have more than one name. You can achieve this by
specifying a space-, comma-, or semicolon-separated list of names in the
name attribute of the bean’s &lt;bean&gt; tag. You can do this in place
of, or in conjunction with, using the id attribute. You can retrieve a
list of the bean aliases by calling
ApplicationContext.getAliases(String) and passing in any one of the
bean’s names or ID. The list of aliases, other than the one you
specified, will then be returned as a String array

 

&lt;bean id="name1" name="name2 name3,name4;name5"
class="java.lang.String"/&gt;

&lt;alias name="name1" alias="name6"/&gt;

 

Bean Instantiation Mode

By default, **all beans in Spring are singletons**. This means Spring
maintains a single instance of the bean, all dependent objects use the
same instance, and all calls to ApplicationContext.getBean() return the
same instance. If you start off with an object that is a singleton but
then discover it is not really suited to multithread access, you can
change it to a nonsingleton (prototype) without affecting any of your
application code.

 

The only difference between this bean declaration and any of the
declarations you have seen so far is that we add the scope attribute and
set the value to **prototype**. Spring defaults the scope to value
singleton. The prototype scope instructs Spring to instantiate a new
instance of the bean every time a bean instance is requested by the
application. The main positive you gain from Spring’s instantiation
management is that your applications can immediately

benefit from the lower memory usage associated with singletons, with
very little effort on your part.

 

Bean Scopes

 

•Singleton: The default singleton scope. Only one object will be created
per Spring IoC container.

• Prototype: A new instance will be created by Spring when requested by
the application.

• Request: For web application use. When using Spring MVC for web
applications, beans with request scope will be instantiated for every
HTTP request and then destroyed when the request is completed.

• Session: For web application use. When using Spring MVC for web
applications, beans with session scope will be instantiated for every
HTTP session and then destroyed when the session is over.

• Global session: For portlet-based web applications. The global session
scope beans can be shared among all portlets within the same Spring
MVC–powered portal application.

• Thread: A new bean instance will be created by Spring when requested
by a new thread, while for the same thread, the same bean instance will
be returned. Note that this scope is not registered by default.

• Custom: Custom bean scope that can be created by implementing the
interface org.springframework.beans.factory.config.Scope and registering
the custom scope in Spring’s configuration (for XML, use the class
org.springframework.beans.factory.config.CustomScopeConfigurer).

 

Resolving Dependencies

 

During normal operation, Spring is able to resolve dependencies by
simply looking at your configuration file or annotations in your
classes. In this way, Spring can ensure that each bean is configured in
the correct order so that each bean has its dependencies correctly
configured. Unfortunately, Spring is not aware of any dependencies that
exist between beans in your code. For example, in the constructor of
beanA, you get an instance of beanB by calling ctx.getBean("beanB"),
without asking Spring to inject the dependency for you. In this case,
Spring is unaware that beanA depends on beanB,

and, as a result, it may instantiate beanA before beanB. You can provide
Spring with additional information about your bean dependencies using
the depends-on attribute of the &lt;bean&gt; tag

 

Autowiring Your Bean

 

So far, we have had to define explicitly, via the configuration file,
how the individual beans are wired together. If you don’t like having to
wire all your components together, you can have Spring attempt to do so
automatically. By default, autowiring is disabled. To enable it, you
specify which method of autowiring you want to use by using the autowire
attribute of the bean you want to autowire.

 

Spring supports **five modes for autowiring: byName, byType,
constructor, default, and no (which is the default)**. When using byName
autowiring, Spring attempts to wire each property to a bean of the same
name. So, if the target bean has a property named foo and a foo bean is
defined in the ApplicationContext, the foo bean is assigned to the foo
property of the target. When using byType autowiring, Spring attempts to
wire each of the properties on the target bean by automatically using a
bean of the same type in ApplicationContext. So, if you have a property
of type String on the target bean, and a bean of type String in
ApplicationContext, then Spring wires the String bean to the target
bean’s String property. If you have more than one bean of the same type,
in this case String, in the same ApplicationContext, then Spring is
unable to decide which one to use for the autowiring and throws an
exception (of type
org.springframework.beans.factory.NoSuchBeanDefinitionException). The
constructor autowiring mode functions just like byType wiring, except
that it uses constructors rather than setters to perform the injection.
Spring attempts to match the greatest numbers of arguments it can in the
constructor. So, if your bean has two constructors, one that accepts a
String and one that accepts a String and an Integer, and you have both a
String and an Integer bean in your ApplicationContext, Spring uses the
two-argument constructor. In default mode, Spring will choose between
constructor and byType modes automatically. If your bean has a default
(no-arguments) constructor, Spring uses byType; otherwise, it uses
constructor.

 

Setting Bean Inheritance

 

Spring allows you to provide a &lt;bean&gt; definition that inherits its
property settings from another bean in the same ApplicationContext. You
can override the values of any properties on the child bean as required,
which allows you to have full control, but the parent bean can provide
each of your beans with a base configuration.

 

&lt;bean id="inheritParent"
class="com.apress.prospring4.ch3.xml.SimpleBean" p:name="Chris Schaefer"
p:age="32"/&gt;

&lt;bean id="inheritChild"
class="com.apress.prospring4.ch3.xml.SimpleBean" parent="inheritParent"
p:age="33"/&gt;

 

In case you don’t want a parent bean definition to become available for
lookup from ApplicationContext, you can add the attribute
abstract="true" in the &lt;bean&gt; tag when declaring the parent bean.

 

Child beans inherit both constructor arguments and property values from
the parent beans, so you can use both styles of injection with bean
inheritance. This level of flexibility makes bean inheritance a powerful
tool for building applications with more than a handful of bean
definitions. If you are declaring a lot of beans of the same value with
shared property values, avoid the temptation to use copy and paste to
share the values; instead, set up an inheritance

hierarchy in your configuration. When you are using inheritance,
remember that bean inheritance does not have to match a Java inheritance

hierarchy. It is perfectly acceptable to use bean inheritance on five
beans of the same type. Think of bean inheritance as more like a
templating feature than an inheritance feature

 

 

 

 

2

Wednesday, September 02, 2015

17:10

 

Bean Life-Cycle Management

 

In general, two life-cycle events are particularly relevant to a bean:
postinitialization and pre-destruction. In the context of Spring, the
post-initialization event is raised as soon as Spring finishes setting
all the property values on the bean and finishes any dependency checks
that you configured it to perform. The pre-destruction event

is fired just before Spring destroys the bean instance. However, for
beans with prototype scope, the pre-destruction event will not be fired
by Spring. Spring provides three mechanisms a bean can use to hook into
each of these events and perform some additional processing:
**interface-based, method-based, and annotation-based mechanisms**

 

Using the interface-based mechanism, your bean implements an interface
specific to the type of notification it wants to receive, and Spring
notifies the bean via a callback method defined in the interface. For
the method-based mechanism, Spring allows you to specify, in your
ApplicationContext configuration, the name of a method to call when the
bean is initialized and the name of a method to call when the bean is
destroyed. For the annotation mechanism, you can use JSR-250 annotations
to specify the method that Spring should call after construction or
before destruction.

 

> ![](media/image3.png){width="7.677083333333333in" height="4.25in"}

 

 

By being aware of when it is initialized, a bean can check whether all
its required dependencies are satisfied. Although Spring can check
dependencies for you, it is pretty much an all-or-nothing approach, and
it doesn’t offer any opportunities for applying additional logic. A bean
cannot perform these checks in its constructor because at this point,
Spring has not had an opportunity to provide values for the dependencies
it can satisfy. The initialization callback in Spring is called after
Spring finishes providing the dependencies that it can and performs any
dependency checks that you ask of it.

 

*Executing a Method When a Bean Is Created*

 

Specifying a callback method is simply a case of specifying the name in
the **init-method** attribute of a bean’s &lt;bean&gt; tag. The benefits
of this mechanism are negated when using a static initialization method,
because you cannot access any of the bean’s state to validate it.

 

Also note that in the &lt;beans&gt; tag,the attribute
**default-lazy-init="true"** to instruct Spring to instantiate the beans
defined in the configuration file only when the bean was requested from
the application. If we do not specify it, Spring will try to initialize
all the beans during the bootstrapping of ApplicationContext,

 

*Implementing the InitializingBean Interface*

 

The InitializingBean interface defined in Spring allows you to define
inside your bean code that you want the bean to receive notification
that Spring has finished configuring it. The InitializingBean interface
defines a single method, **afterPropertiesSet()**

 

*Using JSR-250 @PostConstruct Annotation*

 

Another method that can achieve the same purpose is to use the JSR-250
life-cycle annotation, **@PostConstruct.**

 

You can use all initialization mechanisms on the same bean instance. In
this case, Spring invokes the method annotated with @PostConstruct first
and then InitializingBean.afterPropertiesSet(), followed by your
initialization method specified in the configuration file.

 

Bean Destruction

 

When using an ApplicationContext implementation that wraps the
DefaultListableBeanFactory interface you can signal to BeanFactory that
you want to destroy all singleton instances with a call to
ConfigurableBeanFactory.destroySingletons(). To allow your beans to
receive notification that destroySingletons() has been called, you have
three options

 

To designate a method to be called when a bean is destroyed, you simply
specify the name of the method in the **destroy-method** attribute of
the bean’s &lt;bean&gt; tag. Spring calls it just before it destroys the
singleton instance of the bean (Spring will not call this method for
those beans with prototype scope).

 

Spring provides an interface, in this case **DisposableBean**, that can
be implemented by your beans as a mechanism for receiving destruction
callbacks. The isposableBean interface defines a single method,
destroy(), which is called just before the bean is destroyed

 

The third way is to use the JSR-250 life-cycle @PreDestroy annotation,
which is the inverse of the **@PostConstruct** annotation.

 

As with the case of bean creation, you can use all mechanisms on the
same bean instance for bean destruction. In this case, Spring invokes
the method annotated with @PreDestroy first and then
DisposableBean.destroy(), followed by your destroy method configured in
your XML definition.

 

Using a Shutdown Hook

 

The only drawback of the destruction callbacks in Spring is that they
are not fired automatically; you need to remember to call
AbstractApplicationContext.destroy() before your application is closed.
When your application runs as a servlet, you can simply call destroy()
in the servlet’s destroy() method. However, in a stand-alone
application, things are not quite so simple, especially if you have
multiple exit points out of your application. Fortunately, there is a
solution. Java allows you to create a shutdown hook, a thread that is
executed just before the application shuts down. This is the perfect way
to invoke the destroy() method of your AbstractApplicationContext. The
easiest way to take advantage of this mechanism is to use the
AbstractApplicationContext’s registerShutdownHook() method

 

 

Making Beans Spring Aware

 

One of the biggest selling points of Dependency Injection over
Dependency Lookup as a mechanism for achieving Inversion of Control is
that your beans do not need to be aware of the implementation of the
container that is managing them. To a bean that uses constructor or
setter injection, the Spring container is the same as the container
provided by Google Guice or PicoContainer. However, in certain
circumstances, you may need a bean that is using Dependency Injection to
obtain its dependencies so it can interact with the container for some
other reason. That said, this feature is really intended for internal
Spring use

 

*BeanNameAware Interface*

 

The **BeanNameAware** interface, which can be implemented by a bean that
wants to obtain its own name, has a single method: setBeanName(String).
Spring calls the **setBeanName()** method after it has finished
configuring your bean but before any life-cycle callbacks
(initialization or destroy) are called. In most cases, the

implementation of the setBeanName() interface is just a single line that
stores the value passed in by the container in a field for use later

 

*ApplicationContextAware Interface*

 

Using the ApplicationContextAware interface, it is possible for your
beans to get a reference to the ApplicationContext that configured them.
The main reason this interface was created was to allow a bean to access
Spring’s ApplicationContext in your application—for example, to acquire
other Spring beans programmatically,

using getBean(). You should, however, avoid this practice and use
Dependency Injection to provide your beans with their collaborators

 

The ApplicationContextAware interface defines a single method,
setApplicationContext(ApplicationContext), which Spring calls to pass
your bean a reference to its ApplicationContext.

 

FactoryBeans

 

One of the problems that you will face when using Spring is how to
create and then inject dependencies that cannot be created simply by
using the new operator. To overcome this problem, Spring provides the
FactoryBean interface that acts as an adaptor for objects that cannot be
created and managed using the standard Spring semantics. Typically, you
use FactoryBeans to create beans that you cannot create by using the new
operator, such as those you access through static factory methods,
although this is not always the case. Simply put, a FactoryBean is a
bean that acts as a factory for other beans. FactoryBeans are configured
within your ApplicationContext like any normal bean, but when Spring
uses the FactoryBean interface to satisfy a dependency or lookup
request, it does not return FactoryBean; instead, **it invokes the
FactoryBean.getObject()** method and returns the result of that
invocation

 

In Java, the MessageDigest class provides functionality for creating a
digest of any arbitrary data. MessageDigest itself is abstract, and you
obtain concrete implementations by calling MessageDigest.getInstance()
and passing in the name of the digest algorithm you want to use. For
instance, if we want to use the MD5 algorithm to create a digest, we use
the following code to create the MessageDigest instance:

MessageDigest md5 = MessageDigest.getInstance("MD5");

If we want to use Spring to manage the creation of the MessageDigest
object, the best we can do without a FactoryBean is have a property,
algorithmName, on our bean and then use an initialization callback to
call MessageDigest.getInstance(). Using a FactoryBean, we can
encapsulate this logic inside a bean. Then any beans

that require a MessageDigest instance can simply declare a property,
messageDigest, and use the FactoryBean to obtain the instance.

 

public class MessageDigestFactoryBean implements

FactoryBean&lt;MessageDigest&gt;, InitializingBean {

private String algorithmName = "MD5";

private MessageDigest messageDigest = null;

@Override

public MessageDigest getObject() throws Exception {

> return messageDigest;

}

@Override

public Class&lt;MessageDigest&gt; getObjectType() {

> return MessageDigest.class;

}

@Override

> public boolean isSingleton() {

return true;

}

@Override

public void afterPropertiesSet() throws Exception {

> messageDigest = MessageDigest.getInstance(algorithmName);

}

}

 

The FactoryBean interface declares three methods: getObject(),
getObjectType(), and isSingleton(). Spring calls the getObject() method
to retrieve the object created by the FactoryBean. This is the actual
object that is passed to other beans that use the FactoryBean as a
collaborator

 

The getObjectType() method allows you to tell Spring what type of object
your FactoryBean will return. This can be null if the return type is
unknown in advance, but if you specify a type, Spring can use it for
autowiring purposes

 

Given that Spring automatically satisfies any references to a
FactoryBean by the objects produced by that FactoryBean, you may be
wondering whether **you can actually access the FactoryBean directly**.
The answer is yes. Accessing FactoryBean is simple: you prefix the bean
name with an ampersand in the call to getBean(),

 

MessageDigestFactoryBean factoryBean = (MessageDigestFactoryBean)
ctx.getBean("&shaDigest");

 

 

factory-bean and factory-method Attributes

 

Sometimes you need to instantiate JavaBeans that were provided by a
non-Spring-powered third-party application. You don’t know how to
instantiate that class, but you know that the third-party application
provides a class that can be used to get an instance of the JavaBean
that your Spring application needs. In this case, Spring bean’s
factory-bean and factory-method attributes in the &lt;bean&gt; tag can
be used.

 

&lt;bean id="shaDigest"

> factory-bean="shaDigestFactory"
>
> factory-method="createInstance"&gt;

&lt;/bean&gt;

 

JavaBeans PropertyEditors

 

A PropertyEditor is an interface that converts a property’s value to and
from its native type representation into a String. As of version 4,
Spring comes with 13 built-in PropertyEditor implementations that are
preregistered with BeanFactory

 

*Creating a Custom PropertyEditor*

 

The editor is very simple. It extends JDK’s **PropertyEditorSupport**
class and implements the **setAsText()** method. To use the editor in
our application, we need to register the editor in Spring’s
ApplicationContext

 

&lt;bean name="customEditorConfigurer"
class="org.springframework.beans.factory.config.CustomEditorConfigurer"&gt;

&lt;property name="customEditors"&gt;

> &lt;map&gt;
>
> &lt;entry key="com.apress.prospring4.ch4.Name"
>
> value="com.apress.prospring4.ch4.NamePropertyEditor"/&gt;
>
> &lt;/map&gt;

&lt;/property&gt;

&lt;/bean&gt;

 

First, custom PropertyEditors get injected into the
CustomEditorConfigurer class by using the Map-typed customEditors
property. Second, each entry in the

Map represents a single PropertyEditor, with the key of the entry being
the name of the class for which the PropertyEditor is used. As you can
see, the key for the NamePropertyEditor is
com.apress.prospring4.ch4.Name, which signifies that this is the class
for which the editor should be used.

 

More Spring ApplicationContext Configuration

 

The main function of ApplicationContext is to provide a much richer
framework on which to build your applications. The biggest benefit of
using ApplicationContext is that it allows you to configure and manage
Spring and Spring-managed resources in a completely declarative way.
This means that wherever possible, Spring provides

support classes to load ApplicationContext into your application
automatically, thus removing the need for you to write any code to
access ApplicationContext

 

ApplicationContext supports the following features:

• Internationalization

• Event publication

• Resource management and access

• Additional life-cycle interfaces

• Improved automatic configuration of infrastructure components

 

Internationalization with the MessageSource

 

Using the **MessageSource** interface, your application can access
String resources, called messages, stored in a variety of languages. For
each language you want to support in your application, you maintain a
list of messages that are keyed to correspond to messages in other
languages. Although you don’t need to use ApplicationContext to use
MessageSource, the ApplicationContext interface extends MessageSource
and provides special support for loading messages and for making them
available in your environment

 

Spring provides three MessageSource implementations:
**ResourceBundleMessageSource, ReloadableResourceBundleMessageSource,
and StaticMessageSource**. The

StaticMessageSource implementation should not be used in a production
application because you can’t configure it externally, and this is
generally one of the main requirements when you are adding i18n
capabilities to your application. ResourceBundleMessageSource loads
messages by using a Java ResourceBundle.

ReloadableResourceBundleMessageSource is essentially the same, except it
supports scheduled reloading of the underlying source files. All three
MessageSource implementations also implement another interface called
**HierarchicalMessageSource**, which allows for many MessageSource
instances to be nested

 

To take advantage of ApplicationContext’s support for MessageSource, you
must define a bean in your configuration of type MessageSource and with
the name messageSource. ApplicationContext takes this MessageSource and
nests it within itself, allowing you to access the messages by using
ApplicationContext

 

&lt;bean id="messageSource"
class="org.springframework.context.support.ResourceBundleMessageSource"
p:basenames-ref="basenames"/&gt;

&lt;util:list id="basenames"&gt;

> &lt;value&gt;buttons&lt;/value&gt;
>
> &lt;value&gt;labels&lt;/value&gt;

&lt;/util:list&gt;

 

When looking for a message for a particular Locale, the ResourceBundle
looks for a file that is named as a combination of the base name and the
locale name. For above

the content of the properties files for English (labels\_en.properties)
and Czech (labels\_cs\_CZ.properties)

 

System.out.println(ctx.getMessage("msg", null, english));

System.out.println(ctx.getMessage("msg", null, czech));

 

 

**The main reason to use ApplicationContext rather than a manually
defined MessageSource** bean is that Spring does, where possible, expose
ApplicationContext, as a MessageSource, to the view tier. This means
that when you are using Spring’s JSP tag library, the
&lt;spring:message&gt; tag automatically reads messages from
ApplicationContext, and when you are using JSTL, the &lt;fmt:message&gt;
tag does the same. All of these benefits mean that it is better to use
the MessageSource support in ApplicationContext when you are building a
web application, rather than manage an instance of MessageSource
separately.

 

 

Application Events

 

Another feature of ApplicationContext not present in BeanFactory is the
ability to publish and receive events by using ApplicationContext as a
broker.

An event is class-derived from ApplicationEvent, which itself derives
from java.util.EventObject. Any bean can listen for events by
implementing the ApplicationListener&lt;T&gt; interface;
ApplicationContext automatically registers any bean that implements this
interface as a listener when it is configured. Events are published
using the ApplicationEventPublisher.publishEvent() method, so the
publishing class must have knowledge of ApplicationContext (which
extends the ApplicationEventPublisher interface). In a web application,
this is simple because many of your classes are derived from Spring
Framework classes that allow access to ApplicationContext through a
protected method. In a stand-alone application, you can have your
publishing bean implement ApplicationContextAware to enable it to
publish events

 

**Considerations for Event Usage**

In many cases in an application, certain components need to be notified
of certain events. Often you do this by writing code to notify each
component explicitly or by using a messaging technology such as JMS. The
drawback of writing code to notify each component in turn is that you
are coupling those components to the publisher, in many cases
unnecessarily. Consider a situation whereby you cache product details in
your application to avoid trips to the database. Another component
allows product details to be modified and persisted to the database. To
avoid making the cache invalid, the update component explicitly notifies
the cache that the user details have changed. In this example, the
update component is coupled to a component that, really, has nothing to
do with its business responsibility. A better solution would be to have
the update component publish an event every time a product’s details are
modified and then have interested components, such as the cache, listen
for that event. This has the benefit of keeping the components
decoupled, which makes it simple to remove the cache if needed, or to
add another listener that is interested in knowing when a product’s
details change. Using JMS in this case would be overkill, because the
process of invalidating the product’s entry in the cache is quick and is
not business critical. The use of the Spring event infrastructure adds
very little overhead to your application.

 

 

Accessing Resources

 

At the core of Spring’s resource support is the
org.springframework.core.io.Resource interface. The Resource interface
defines ten self-explanatory methods: **contentLength(), exists(),
getDescription(), getFile(), getFileName(), getURI(), getURL(),
isOpen(), isReadable(), and lastModified()**. In addition to these ten
methods, there is one that is not quite so self-explanatory:
**createRelative()**. The createRelative() method creates a new Resource
instance by using a path that is relative to the instance on which it is
invoked. Internally, Spring uses another interface, ResourceLoader, and
the default implementation, DefaultResourceLoader, to locate and create
Resource instances

 

Configuration Using Java Classes

 

Besides XML and property file configuration, you can use Java classes to
configure Spring’s ApplicationContext. Spring JavaConfig used to be a
separate project, but starting with Spring 3.0, its major features for
configuration using Java classes was merged into the core Spring
Framework.

 

• The @PropertySource annotation is used to load properties files into
the Spring ApplicationContext, which accepts the location as the
argument (more than one location can be provided). For XML,
&lt;context:property-placeholder&gt; serves the same purpose.

 

• @ImportResource can also be used to import configuration from XML
files, which means you can use XML and Java configuration classes in a
mix-and-match way. Besides @ImportResource, the @Import annotation can
import other configuration classes, which means you can also have
multiple Java configuration classes for various configurations

 

• @ComponentScan defines the packages that Spring should scan for
annotations for bean definitions. It’s the same as the
&lt;context:component-scan&gt; tag in the XML configuration.

 

Profiles

 

Another interesting feature that Spring provides is the concept of
configuration profiles. Basically, a profile instructs Spring to
configure only the ApplicationContext that was defined when the
specified profile was active

 

In the previous two configurations, notice the usage of
profile="kindergarten" and profile="highschool", respectively, within
the &lt;beans&gt; tag. It actually tells Spring that those beans in the
file should be instantiated only when the specified profile is active.

 

The ctx.load() method will load both kindergarten-config.xml and
highschool-config.xml, since we pass the method the wildcard as the
prefix. In this example, only the beans in the file
kindergarten-config.xml will be instantiated by the Spring base on the
profile attribute, which is activated by passing the JVM argument

-Dspring.profiles.active="kindergarten

 

The profiles feature in Spring creates another way for developers to
manage the application’s running configuration, which used to be done in
build tools (for example, Maven’s profile support). Spring’s profile
feature lets us as application developers define the profiles by
ourselves and activate them either programmatically or by passing in the
JVM argument. By using Spring’s profile support, you can now use the
same application archive and deploy to all environments, by passing in
the correct profiles as an argument during JVM startup

 

But this approach also has its drawbacks. For example, some may argue
that putting all the configuration for different environments into
application configuration files or Java classes and bundling them
together will be error prone if not handled carefully (for example, the
administrator may forget to set the correct JVM argument in the

application server environment). Packing files for all profiles together
will also make the package a bit larger than usual.

 

The Environment interface

 

It is an abstraction layer that serves to encapsulate the environment of
the running Spring application. Besides the profile, other key pieces of
information encapsulated by the Environment interface are properties.
Properties are used to store the application’s underlying environment
configuration, such as the location of the application folder, database
connection information, and so on. Under the abstraction, all system
properties, environment variables, and application properties are served
by the Environment interface, which Spring populates when bootstrapping
ApplicationContext

 

Configuration Using JSR-330 Annotations

 

JEE 6 provides support for JSR-330 (“Dependency Injection for Java”),
which is a collection of annotations for expressing an application’s DI
configuration within a JEE container or other compatible IoC framework.
Spring also supports and recognizes those annotations, so although you
may not be running your application in a JEE 6 container, you can still
use JSR-330 annotations within Spring. Using JSR-330 annotations can
help you ease the migration to the JEE 6 container or other compatible
IoC container (for example, Google Guice) away from Spring.

 

 

 

3

Friday, September 04, 2015

11:27

 

The term crosscutting concerns refers to logic in an application that
cannot be decomposed from the rest of the application and may result in
code duplication and tight coupling. By using AOP for modularizing
individual pieces of logic, known as concerns, you can apply these to
many parts of an application without duplicating the code or

creating hard dependencies. Logging and security are typical examples of
crosscutting concerns that are present in many applications.

 

It is important to understand that **AOP complements object-oriented
programming (OOP)**, rather than competing with it. OOP is very good at
solving a wide variety of problems that we, as programmers, encounter.
However, if you look at the logging example again, it is obvious to see
where OOP is lacking when it comes to implementing crosscutting logic on
a large scale. Using AOP on its own to develop an entire application is
practically impossible, given that AOP functions on top of OOP.
Likewise, although it is certainly possible to develop entire
applications by using OOP, you can work smarter by employing AOP to
solve certain problems that involve crosscutting logic.

 

• **Joinpoints**: A joinpoint is a well-defined point during the
execution of your application. Typical examples of joinpoints include a
call to a method, the method invocation itself, class initialization,
and object instantiation. Joinpoints are a core concept of AOP and
define the points in your application at which you can insert additional
logic using AOP.

• **Advice**: The code that is executed at a particular joinpoint is the
advice, defined by a method in your class. There are many types of
advice, such as before, which executes before the joinpoint, and after,
which executes after it.

• **Pointcuts**: A pointcut is a collection of joinpoints that you use
to define when advice should be executed. By creating pointcuts, you
gain fine-grained control over how you apply advice to the components in
your application. As mentioned previously, a typical joinpoint is a
method invocation, or the collection of all method invocations in a
particular class. Often you can compose pointcuts in complex
relationships to further constrain when advice is executed.

• **Aspects**: An aspect is the combination of advice and pointcuts
encapsulated in a class. This combination results in a definition of the
logic that should be included in the application and where it should
execute.

• **Weaving**: This is the process of inserting aspects into the
application code at the appropriate point. For compile-time AOP
solutions, this weaving is generally done at build time. Likewise, for
runtime AOP solutions, the weaving process is executed dynamically at
runtime. AspectJ supports another weaving mechanism called load-time
weaving (LTW), in which it intercepts the underlying JVM class loader
and provides weaving to the bytecode when it is being loaded by the
class loader.

• **Target**: An object whose execution flow is modified by an AOP
process is referred to as the target object. Often you see the target
object referred to as the advised object.

• **Introduction**: This is the process by which you can modify the
structure of an object by introducing additional methods or fields to
it. You can use introduction AOP to make any

object implement a specific interface without needing the object’s class
to implement that interface explicitly.

 

Pointcut vs Joinpoint

 

To understand the difference between a join point and pointcut, think of
pointcuts as specifying the weaving rules and join points as situations
satisfying those rules.

In below example,

@Pointcut("execution(\* \* getName()")

Pointcut defines rules saying, advice should be applied on getName()
method present in any class in any package and joinpoints will be a list
of all getName() method present in classes so that advice can be applied
on these methods.

 

Types of AOP

 

In **static AOP**, the weaving process forms another step in the build
process for an application. In Java terms, you achieve the weaving
process in a static AOP implementation by modifying the actual bytecode
of your application, changing and extending the application code as
necessary. This is a well-performing way of achieving the weaving
process because the end result is just Java bytecode, and you do not
perform any special tricks at runtime to determine when advice should be
executed. The drawback of this mechanism is that any modifications you
make to the aspects, even if you simply want to add another joinpoint,
require you to recompile the entire application. AspectJ’s compile-time
weaving is an excellent example of a static AOP implementation.

 

**Dynamic AOP** implementations, such as Spring AOP, differ from static
AOP implementations in that the weaving process is performed dynamically
at runtime. How this is achieved is implementation-dependent, but as you
will see, Spring’s approach is to create proxies for all advised
objects, allowing for advice to be invoked as required. The

drawback of dynamic AOP is that, typically, it does not perform as well
as static AOP, but the performance is steadily increasing. The major
benefit of dynamic AOP implementations is the ease with which you can
modify the entire aspect set of an application without needing to
recompile the main application code.

 

Example

 

public class MessageWriter {

> public void writeMessage() {
>
> System.out.print("World");
>
> }

}

 

With our message-printing method implemented, let’s advise—which in AOP
terms means add advice to—this method so that writeMessage() prints
“Hello World!” instead.

To do this, we need to execute code prior to the existing body executing
(to write “Hello”), and we need to execute code after that method body
executes (to write “!”). In AOP terms, what we need is around advice,
which executes around a joinpoint. In this case, the joinpoint is the
invocation of the writeMessage() method

 

public class MessageDecorator implements MethodInterceptor {

> @Override
>
> public Object invoke(MethodInvocation invocation) throws Throwable {
>
> System.out.print("Hello ");
>
> Object retVal = invocation.proceed();
>
> System.out.println("!");
>
> return retVal;
>
> }

}

 

The **MethodInterceptor** interface is a standard AOP Alliance interface
for implementing around advice for method invocation joinpoints. The
**MethodInvocation** object represents the method invocation that is
being advised, and using this object, we control when the method
invocation is allowed to proceed. Because this is around advice, we are
capable of performing actions before the method is invoked as well as
after it is invoked but before it returns.

 

The final step in this sample is to **weave the MessageDecorator
advice** (more specifically, the invoke() method) into the code. To do
this, we create an instance of **MessageWriter**, the target, and then
create a proxy of this instance, instructing the proxy factory to weave
in the MessageDecorator advice

 

 

MessageWriter target = new MessageWriter();

ProxyFactory pf = new ProxyFactory();

pf.addAdvice(new MessageDecorator());

pf.setTarget(target);

MessageWriter proxy = (MessageWriter) pf.getProxy();

target.writeMessage();

System.out.println("");

proxy.writeMessage();

 

The important part here is that we use the ProxyFactory class to create
the proxy of the target object, weaving in the advice at the same time.
We pass the MessageDecorator advice to the ProxyFactory with a call to
addAdvice() and specify the target for weaving with a call to
setTarget(). Once the target is set and some advice is added to the
ProxyFactory, we generate the proxy with a call to getProxy(). Finally,
we call writeMessage() on both the original target object and the proxy
object.

 

World

Hello World!

 

As you can see, calling writeMessage() on the untouched target object
results in a standard method invocation, and no extra content is written
to console output. However, the invocation of the proxy causes the code
in MessageDecorator to execute, creating the desired “Hello World!”
output. From this example, you can see that the advised class had no
dependencies on Spring or the AOP Alliance interfaces; the beauty of
Spring AOP, and indeed AOP in general, is that you can advise almost any
class, even if that class was created without AOP in mind. **The only
restriction, in Spring AOP at least, is that you can’t advise final
classes**, because they cannot be overridden and therefore cannot be
proxied

 

Spring AOP Architecture

 

The core architecture of Spring AOP is based around proxies. When you
want to create an advised instance of a class, you must use
**ProxyFactory** to create a proxy instance of that class, first
providing ProxyFactory with all the aspects that you want to be woven
into the proxy. Using ProxyFactory is a purely programmatic approach to
creating AOP

proxies. For the most part, you don’t need to use this in your
application; instead, you can rely on the declarative AOP configuration
mechanisms provided by Spring (the ProxyFactoryBean class, the aop
namespace, and @AspectJstyle annotations) to take advantage of
declarative proxy creation.

 

At runtime, Spring analyzes the crosscutting concerns defined for the
beans in ApplicationContext and generates proxy beans (which wrap the
underlying target bean) dynamically. Instead of calling the target bean
directly, callers are injected with the proxied bean. The proxy bean
then analyzes the running condition (that is, joinpoint, pointcut, or
advice) and weaves in the appropriate advice accordingly

 

Internally, Spring has two proxy implementations: **JDK dynamic proxies
and CGLIB proxies.** By default, when the target object to be advised
implements an interface, Spring will use a JDK dynamic proxy to create
proxy instances of the target. However, when the advised target object
doesn’t implement an interface (for example, it’s a concrete

class), CGLIB will be used for proxy instance creation. One major reason
is that JDK dynamic proxy supports only the proxying of interfaces.

 

Joinpoints in Spring

 

One of the more noticeable simplifications in Spring AOP is that it
**supports only one joinpoint type: method invocation.** The Method
Invocation joinpoint is by far the most useful joinpoint available, and
using it, you can achieve many of the tasks that make AOP useful in
day-to-day programming

 

Aspects in Spring

 

In Spring AOP, an aspect is represented by an instance of a class that
implements the Advisor interface. Spring provides convenience Advisor
implementations that you can reuse in your applications, thus removing
the need for you to create custom Advisor implementations. There are two
subinterfaces of Advisor: **PointcutAdvisor and IntroductionAdvisor**.
The PointcutAdvisor interface is implemented by all Advisor
implementations that use pointcuts to control the advice applied to
joinpoints. In Spring, introductions are treated as special kinds of
advice, and by using the IntroductionAdvisor interface, you can control
those classes to which an introduction applies.

 

ProxyFactory Class

 

The ProxyFactory class controls the weaving and proxy creation process
in Spring AOP. Before you can create a proxy, you must specify the
advised or target object. You can do this, as you saw earlier, by using
the setTarget() method. Internally, ProxyFactory delegates the proxy
creation process to an instance of DefaultAopProxyFactory, which in turn
delegates to either Cglib2AopProxy or JdkDynamicAopProxy, depending on
the settings of your application

 

The ProxyFactory class provides the **addAdvice()** method that you saw
in Listing 5-3 for cases where you want advice to apply to the
invocation of all methods in a class, not just a selection. Internally,
addAdvice() wraps the advice you pass it in an instance of
**DefaultPointcutAdvisor**, which is the standard implementation of
PointcutAdvisor, and configures it with a pointcut that includes all
methods by default. When you want more control over the Advisor that is
created, or when you want to add an introduction to the proxy, create
the Advisor yourself and use the addAdvisor() method of the ProxyFactory

 

You can use the same ProxyFactory instance to create many proxies, each
with different aspects. To help with this, **ProxyFactory has
removeAdvice() and removeAdvisor()** methods, which allow you to remove
any advice or Advisors from the ProxyFactory that you previously passed
to it. To check whether a ProxyFactory has particular advice attached to
it, call **adviceIncluded()**, passing in the advice object for which
you want to check

 

Advice Types in Spring

 

Before

**org.springframework.aop.MethodBeforeAdvice :** Using before advice,
you can perform custom processing before a joinpoint executes. Because a
joinpoint in Spring

is always a method invocation, this essentially allows you to perform
preprocessing before the method executes. Before advice has full access
to the target of the method invocation as well as the arguments passed
to the method, but it has no control over the execution of the method
itself. In case the before advice throws an exception, further execution
of the interceptor chain (as well as the target method) will be aborted,
and the exception will propagate back up the interceptor chain.

 

**SimpleBeforeAdvice** class. The MethodBeforeAdvice interface, which is
implemented by SimpleBeforeAdvice, defines a single method, before(),
which the AOP framework calls before the method at the joinpoint is
invoked. The before() method is passed three arguments: the method that
is to be invoked, the arguments that will be passed to that method, and
the Object that is the target of the invocation.

@Override

public void before(Method method, Object\[\] args, Object target)throws
Throwable {

> System.out.println("Before method: " + method.getName());

}

 

 

After-returning

**org.springframework.aop.AfterReturningAdvice** : After-returning
advice is executed after the method invocation at the joinpoint has
finished executing and has

returned a value. The after-returning advice has access to the target of
the method invocation, the arguments passed to the method, and the
return value as well. Because the method has already executed when the
after-returning advice is invoked, it has no control over the method
invocation at all. In case the target method throws an exception, the
afterreturning advice will not be run, and the exception will be
propagated up to the call stack as usual.

 

**you cannot modify the return value in the after-returning advice.**
When using after-returning advice, you are limited to adding processing.
Although after-returning advice cannot modify the return value of a
method invocation, it can throw an exception that can be sent up the
stack instead of the return value

 

the AfterReturningAdvice interface declares a single method,
afterReturning(), which is passed the return value of method invocation,
a reference to the method that was invoked, the arguments that were
passed to the method, and the target of the invocation

 

@Override

public void afterReturning(Object returnValue, Method method,Object\[\]
args, Object target) throws Throwable {

> System.out.println("");
>
> System.out.println("After method: " + method.getName());

}

 

 

 

After (finally)

**org.springframework.aop.AfterAdvice:** After-returning advice is
executed only when the advised method completes normally. However, the
after (finally)

advice will be executed no matter the result of the advised method. The
advice is executed even when the advised method fails and an exception
is thrown.

 

Around

**org.aopalliance.intercept.MethodInterceptor:** In Spring, around
advice is modeled using the AOP Alliance standard of a method
interceptor. Your advice is allowed to

execute before and after the method invocation, and you can control the
point at which the method invocation is allowed to proceed. You can
choose to bypass the method altogether if you want, providing your own
implementation of the logic.

 

Around advice functions like a combination of before and after advice,
with one big difference—**you can modify the return value**. Not only
that, but you can prevent the method from executing. This means that by
using around advice, you can essentially replace the entire
implementation of a method with new code. Around advice in Spring is
modeled as an interceptor using the MethodInterceptor interface.

 

invoke() method of the MethodInterceptor class does not provide the same
set of arguments as MethodBeforeAdvice and AfterReturningAdvice. The
method is not passed the target of the invocation, the method that was
invoked, nor the arguments used. However, you can access this data by
using the MethodInvocation object that is passed to invoke().

 

 

@Override

public Object invoke(MethodInvocation invocation) throws Throwable {

}

 

 

Throws

**org.springframework.aop.ThrowsAdvice**: Throws advice is executed
after a method invocation returns, but only if that invocation threw an
exception. It is possible

for throws advice to catch only specific exceptions, and if you choose
to do so, you can access the method that threw the exception, the
arguments passed into the invocation, and the target of the invocation.

 

Throws advice is similar to after-returning advice in that it executes
after the joinpoint, which is always a method invocation, but throws
advice executes only if the method throws an exception. Throws advice is
also similar to afterreturning advice in that it has little control over
program execution. If you are using throws advice, you can’t choose to

ignore the exception that was raised and return a value for the method
instead. The only modification you can make to the program flow is to
change the type of exception that is thrown.

 

Unlike the interfaces you have seen so far, **ThrowsAdvice does not
define any methods**; instead, it is simply a marker interface used by
Spring. The reason for this is that Spring allows typed throws advice,
which allows you to define exactly which Exception types your throws
advice should catch. Spring achieves this by detecting methods with
certain signatures using reflection. Spring looks for two distinct
method signatures.

 

@Override

public void afterThrowing(Exception ex) throws Throwable {

}

 

@Override

public void afterThrowing(Method method, Object\[\] args, Object
target,IllegalArgumentException ex) throws Throwable {

}

 

The first thing Spring looks for in throws advice is one or more public
methods called afterThrowing(). The return type of the methods is
unimportant, although we find it best to stick with void because this
method can’t return any meaningful value. The first afterThrowing()
method in the SimpleThrowsAdvice class has a single argument of type
Exception. You can specify any type of Exception as the argument, and
this method is ideal when you are not concerned about the method that
threw the exception or the arguments that were passed to it

 

In the second afterThrowing() method, we declared four arguments to
catch the Method that threw the exception, the arguments that were
passed to the method, and the target of the method invocation. The order
of the arguments in this method is important, and you must specify all
four

 

Introduction

**org.springframework.aop.IntroductionInterceptor**: Spring models
introductions as special types of interceptors. Using an introduction
interceptor, you can specify the implementation for methods that are
being introduced by the advice.

 

Advisors and Pointcuts in Spring

 

**you may want to limit the methods to which the advice applies.** you
could simply perform the checking in the advice itself that the method
being advised is the correct one, but this approach has several
drawbacks. First, hard-coding the list of acceptable methods into the
advice reduces the advice’s reusability. By using pointcuts, you can
configure the methods to which an advice applies, without needing to put
this code inside the advice; this clearly increases the reuse value of
the advice. Other drawbacks with hard-coding the list of methods into
the advice are performance related. To inspect the method being advised
in the advice, you need to perform the check each time any method on the
target is invoked. This clearly reduces the performance of your
application. When you use pointcuts, the check is performed once for
each method, and the results are cached for later use. The other
performance-related drawback of not using pointcuts to restrict the
list-advised methods is that Spring can make optimizations for
nonadvised methods when creating a proxy, which results in faster
invocations on nonadvised methods

 

Pointcut Interface

public interface Pointcut {

> ClassFilter getClassFilter ();
>
> MethodMatcher getMethodMatcher();

}

 

When determining whether a Pointcut applies to a particular method,
Spring first checks to see whether the Pointcut applies to the method’s
class by using the ClassFilter instance returned by
Pointcut.getClassFilter().

 

public interface ClassFilter {

> boolean matches(Class&lt;?&gt; clazz);

}

 

the ClassFilter interface defines a single method, matches(), that is
passed an instance of Class that represents the class to be checked

 

public interface MethodMatcher {

> boolean matches(Method m, Class&lt;?&gt; targetClass);
>
> boolean isRuntime();
>
> boolean matches(Method m, Class&lt;?&gt; targetClass, Object\[\]
> args);

}

 

Spring supports **two types of MethodMatcher, static and dynamic**,
which are determined by the return value of isRuntime(). Before using
MethodMatcher, Spring calls isRuntime() to determine whether
MethodMatcher is static, indicated by a return value of false, or
dynamic, indicated by a return value of true.

 

For a **static pointcut, Spring calls the matches(Method,
Class&lt;T&gt;)** method of the MethodMatcher once for every method on
the target, caching the return value for subsequent invocations of those
methods

 

With **dynamic pointcuts**, Spring still performs a static check by
using matches(Method, Class&lt;T&gt;) the first time a method is invoked
to determine the overall applicability of a method. However, in addition
to this and provided that the static check returned true, Spring
performs a further check for each invocation of a method by using the
matches(Method, Class&lt;T&gt;, Object\[\]) method. In this way, a
dynamic MethodMatcher can determine whether a pointcut should apply
based on a particular invocation of a method, not just on the method
itself

 

Clearly, **static pointcuts perform much better than dynamic pointcuts**
because they avoid the need for an additional check per invocation.
Dynamic pointcuts provide a greater level of flexibility for deciding
whether to apply advice.

 

Spring Pointcut Implementations

 

**org.springframework.aop.support.annotation.AnnotationMatchingPointcut
:**Pointcut that looks for specific Java annotation on a class or
method. This class requires JDK 5 or higher.

**org.springframework.aop.aspectj.AspectJExpressionPointcut:** Pointcut
that uses AspectJ weaver to evaluate a pointcut expression in AspectJ
syntax.

**org.springframework.aop.support.ComposablePointcut:**The
ComposablePointcut class is used to compose two or more pointcuts
together with operations such as union() and

intersection().

**org.springframework.aop.support.ControlFlowPointcut:**The
ControlFlowPointcut is a special case pointcut that matches all methods
within the control flow of another method—that is, any method that is
invoked either directly or indirectly as the result of another method
being invoked.

**org.springframework.aop.support.DynamicMethodMatcherPointcut:**The
DynamicMethodMatcherPointcut is intended as a base class for building
dynamic pointcuts.

**org.springframework.aop.support.JdkRegexpMethodPointcut:** The
JdkRexepMethodPointcut allows you to define pointcuts using JDK 1.4
regular expression support. This class requires JDK 1.4 or newer.

**org.springframework.aop.support.NameMatchMethodPointcut:** Using the
NameMatchMethodPointcut, you can create a pointcut that performs simple
matching against a list of method names.

**org.springframework.aop.support.StaticMethodMatcherPointcut:** The
StaticMethodMatcherPointcut class is intended as a base for building
static pointcuts.

 

 

Using StaticMethodMatcherPointcut

 

public class SimpleStaticPointcut extends StaticMethodMatcherPointcut {

@Override

public boolean matches(Method method, Class&lt;?&gt; cls) {

> return ("foo".equals(method.getName()));

}

@Override

public ClassFilter getClassFilter() {

> return new ClassFilter() {
>
> public boolean matches(Class&lt;?&gt; cls) {
>
> return (cls == BeanOne.class);
>
> }
>
> };

}

}

 

Using DyanmicMethodMatcherPointcut

 

Creating a dynamic pointcut is not much different from creating a static
one

 

Although we are required to implement only the dynamic check, we
implement the static check as well. The reason for this is that we know
the bar() method will never be advised. By indicating this by using the
static check, Spring never has to perform a dynamic check for this
method. This is because when the static check method is implemented,
Spring will first check against it, and if the checking result is a not
a match, Spring will stop doing any further dynamic checking. Moreover,
the result of the static check will be cached for better performance.
But if we neglect the static check, Spring performs a dynamic check each
time the bar() method is invoked. As a recommended practice, perform the
class checking in the getClassFilter() method, method checking in the
matches(Method, Class&lt;?&gt;) method, and argument checking in the
matches(Method, Class&lt;?&gt;, Object\[\]) method. This will make your
pointcut much easier to understand and maintain, and performance will be
better too.

 

 

Using Simple Name Matching

 

Often when creating a pointcut, you want to match based on just the name
of the method, ignoring method signature and return type. In this case,
you can avoid needing to create a subclass of
StaticMethodMatcherPointcut and use the NameMatchMethodPointcut (which
is a subclass of StaticMethodMatcherPointcut) to match against a list of
method names instead. When you are using NameMatchMethodPointcut, no
consideration is given to the signature of the method, so if you have
methods foo() and foo(int), they are both matched for the name foo.

 

There is no need to create a class for the pointcut; you can simply
create an instance of NameMatchMethodPointcut, and you are on your way

 

Pointcuts with Regular Expressions

 

what if you want to match all methods whose names starts with get? In
this case, you can use the regular expression pointcut
JdkRegexpMethodPointcut to match a method name based on a regular
expression

 

we do not need to create a class for the pointcut; instead, we just
create an instance of JdkRegexpMethodPointcut and specify the pattern to
match, and we are finished. The interesting thing to note is the
pattern. When matching method names, Spring matches the fully qualified
name of the method, so for foo1(), Spring is matching against
com.apress.prospring4.ch5.RegexpBean.foo1, which is why there’s the
leading .\* in the pattern. This is a powerful concept because it allows
you to match all methods within a given package, without needing to know
exactly which classes are in that package and what the names of the
methods are

 

Annotation Matching Pointcuts

 

If your application is annotation-based, you may want to use your own
specified annotations for defining pointcuts, that is, apply the advice
logic to all methods or types with specific annotations. Spring provides
the class AnnotationMatchingPointcut for defining pointcuts using
annotations

 

an instance of AnnotationMatchingPointcut is acquired by calling its
static method forMethodAnnotation() and passing in the annotation type.
This indicates that we want to apply the advice to all the methods
annotated with the given annotation. It’s also possible to specify
annotations applied at the type level by calling the
forClassAnnotation() method.

 

 

Understanding Proxies

 

Friday, September 18, 2015

15:13

 

[JAX-RS](http://en.wikipedia.org/wiki/JAX-RS): Java API for RESTful Web
Services is a Java programming language API

 

**A resource class** is a Java class annotated with JAX-RS annotations
to represent a Web resource. Two types of resource classes are
available: **root resource classes and subresource classes**. A root
resource class is annotated with at least a @Path annotation, while
subresource classes typically have no root @Path values.

 

The **@Produces** annotation is used to specify the format of the
response. When not available on the resource method, it's inherited from
a class, and if it's not available on the class then it's inherited from
a corresponding message body writer, if any. Default value is \*/\*, but
it's recommended that some definite value is specified. The same applies
to **@Consumes**, except that it's the message body *readers* that are
checked as the last resort.

 

The **@Path** annotation is applied to resource classes or methods. The
value of @Path annotation is a relative URI path and follows the URI
Template format and may include arbitrary regular expressions. When not
available on the resource method, it's inherited from a class

 

Either **javax.ws.rs.core.Response** or custom type can be returned.
javax.ws.rs.core.Response can be used to set the HTTP response code,
headers and entity. JAX-RS MessageBodyWriters (see below) are in charge
of serializing the response entities, those which are returned directly
or as part of javax.ws.rs.core.Response.

 

**Exception Handling**

One can either throw an unchecked WebApplicationException or return
Response with a proper error code set.

Yet another option is to register an ExceptionMapper provider. Ex :

 

**public** BookExceptionMapper **implements**
ExceptionMapper&lt;BookException&gt; {

    **public** Response toResponse(BookException ex) {

        // convert to Response

    }

}

 

This allows for throwing a checked or runtime exception from an
application code and map it to an HTTP response in a registered
provider.

When no mappers are found for custom exceptions, they are propagated to
the underlying container as required by the specification where they
will typically be wrapped in ServlerException, eventually resulting in
HTTP 500 status being returned by default. Thus one option for
intercepting the exceptions is to register a custom servlet filter which
will catch ServletExceptions and handle the causes

 

 

**Parameters**

PathParam annotation is used to map a given Path template variable to a
method parameter.

Parameters can be of type String or of any type that have constructors
accepting a String parameter or stat ic valueOf(String s) methods. 

Additionally CXF JAXRS checks for static fromString(String s) method, so
types with no valueOf(String) factory methods can also be dealt with

 

It's also possible to inject all types of parameters into fields or
through dedicated setters like below

 

@Path("/customer/{id}")

**public** **class** CustomerService {

 

    @PathParam("id")

    **private** Long id;

     

    **private** String name;

 

    @PathParam("name")

    **public** setName(String name) {

        **this**.name = name;

    }

 

    @PUT

    @Path("{name}")

    **public** Response updateCustomer() {

        // use id and name

    }

}

 

**Selection of Path**

When multiple resource classes match a given URI request, the following
algorithm is used :

1\. Prefer the resource class which has more literal characters in its
@Path annotation. Eg: Both classes match /bar/1/baz requests but Test2
will be selected as it has 9 Path literal characters compared to 5 in
Test1

 

2\. Prefer the resource class which has more capturing groups in its
@Path annotation. Eg: Both classes match /bar/1/2 requests and both have
the same number of literal characters but Test2 will be selected as it
has 2 Path capturing groups (id and id1) as opposed to 1 in Test1.

 

3\. Prefer the resource class which has more capturing groups with
arbitrary regular expressions in its @Path annotation.

Once the resource class has been selected, the next step is to choose a
resource method. If multiple methods can be matched then the same rules
which are used for selecting resource classes are applied. Additionally,
one more rule is used.

 

4\. Prefer a resource method to a subresource locator method

 

**Sub Resource Method**

 

A method of a resource class that is annotated with @Path becomes a
sub-resource locator when no annotation with an HttpMethod designator
like @GET is present. Sub-resource locators are used to further resolve
the object that will handle the request. They can delegate to other
sub-resource locators, including themselves.

 

 

**Message Body Providers**

 

JAX-RS relies on MessageBodyReader and MessageBodyWriter implementations
to serialize and de-serialize Java types. JAX-RS requires that certain
types has to be supported out of the box. 

By default, CXF supports String, byte\[\], InputStream, Reader, File,
JAXP Source, JAX-RS StreamingOutput, JAXB-annotated types with
application/xml, text/xml and application/json formats as well as
JAXBElement

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

WADL

Friday, September 18, 2015

15:37

 

WADL is a resource-centric description language which has been designed
to facilitate the modeling, description and testing of RESTful Web
applications.

 

A top level WADL document element is called "application". Usually it
may contain a "grammars" section and "resources" element with one or
more top-level "resource" elements, with each one representing a
specific root resource

 

**WADL-first Development**

 

CXF 2.4.1 introduces a wadl2java code generator and cxf-wadl2java-plugin
Maven plugin which can be used to generate server and client JAX-RS code
and speed up the transition between modeling and implementation stages.

 

Running wadltojava

 

&lt;**groupId**&gt;org.apache.cxf&lt;/**groupId**&gt;

&lt;**artifactId**&gt;cxf-wadl2java-plugin&lt;/**artifactId**&gt;

&lt;**version**&gt;2.4.1&lt;/**version**&gt;

 

**WADL Auto Generation at Runtime**

 

&lt;**dependency**&gt;

  &lt;**groupId**&gt;org.apache.cxf&lt;/**groupId**&gt;

  &lt;**artifactId**&gt;cxf-rt-rs-service-description&lt;/**artifactId**&gt;

  &lt;**version**&gt;3.0.0-milestone1&lt;/**version**&gt;

&lt;/**dependency**&gt;

 

CXF JAX-RS supports the auto-generation of WADL for JAX-RS endpoints. 

CXF 3.0.0 and 2.7.11 introduce java2wadl plugin for generating WADL at
the build time:

&lt;**groupId**&gt;org.apache.cxf&lt;/**groupId**&gt;

&lt;**artifactId**&gt;cxf-java2wadl-plugin&lt;/**artifactId**&gt;

&lt;**version**&gt;3.0.0&lt;/**version**&gt;

 

**Service listings**

 

 

Links to WADL instances for RESTful endpoints are available from {base
endpointaddress}/services, in addition to SOAP endpoints if any.

 

 

 

 

 

 

 

 

 

 

 

 

 

 

Spring

Friday, September 18, 2015

15:41

&lt;**beans** xmlns="<http://www.springframework.org/schema/beans>"

      xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>"

      xmlns:jaxrs="<http://cxf.apache.org/jaxrs>"

      xsi:schemaLocation="

         <http://www.springframework.org/schema/beans>
<http://www.springframework.org/schema/beans/spring-beans-2.0.xsd>

         <http://cxf.apache.org/jaxrs>
<http://cxf.apache.org/schemas/jaxrs.xsd>"&gt;

 

     &lt;**import** resource="classpath:META-INF/cxf/cxf.xml" /&gt;

     &lt;**import**
resource="classpath:META-INF/cxf/osgi/cxf-extension-osgi.xml" /&gt;

 

     &lt;**jaxrs:server** id="customerService" address="/customers"&gt;

        &lt;**jaxrs:serviceBeans**&gt;

           &lt;**ref** bean="serviceBean"/&gt;

        &lt;/**jaxrs:serviceBeans**&gt;

     &lt;/**jaxrs:server**&gt;

       

     &lt;**bean** id="serviceBean" class="service.CustomerService"/&gt;

&lt;/**beans**&gt;

 

 

 

 

 

&lt;?**xml** version="1.0" encoding="ISO-8859-1"?&gt;

 

&lt;!DOCTYPE web-app

    PUBLIC "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"

    "<http://java.sun.com/dtd/web-app_2_3.dtd>"&gt;

&lt;**web-app**&gt;

    &lt;**context-param**&gt;

        &lt;**param-name**&gt;contextConfigLocation&lt;/**param-name**&gt;

        &lt;**param-value**&gt;WEB-INF/beans.xml&lt;/**param-value**&gt;

    &lt;/**context-param**&gt;

 

    &lt;**listener**&gt;

        &lt;**listener-class**&gt;

            org.springframework.web.context.ContextLoaderListener

        &lt;/**listener-class**&gt;

    &lt;/**listener**&gt;

 

    &lt;**servlet**&gt;

        &lt;**servlet-name**&gt;CXFServlet&lt;/**servlet-name**&gt;

        &lt;**display-name**&gt;CXF Servlet&lt;/**display-name**&gt;

        &lt;**servlet-class**&gt;

            org.apache.cxf.transport.servlet.CXFServlet

        &lt;/**servlet-class**&gt;

        &lt;**load-on-startup**&gt;1&lt;/**load-on-startup**&gt;

    &lt;/**servlet**&gt;

 

    &lt;**servlet-mapping**&gt;

        &lt;**servlet-name**&gt;CXFServlet&lt;/**servlet-name**&gt;

        &lt;**url-pattern**&gt;/\*&lt;/**url-pattern**&gt;

    &lt;/**servlet-mapping**&gt;

&lt;/**web-app**&gt;

 

 

 

 

Config

Friday, September 18, 2015

15:43

 

**Debugging**

 

One may want to use a browser to test how a given HTTP resource reacts
to different HTTP Accept or Accept-Language header values and request
methods. For example, if a resource class supports a "/resource" URI
then one can test the resource class using one of the following queries
:

&gt; GET /resource.xml 

&gt; GET /resource.en

The runtime will replace '.xml' or '.en' with an appropriate header
value. For it to know the type or language value associated with a given
URI suffix, some configuration needs to be done. Here's an example of
how it can be done with Spring:

&lt;**jaxrs:server** id="customerService" address="/"&gt;

  &lt;**jaxrs:serviceBeans**&gt;

    &lt;**bean** class="org.apache.cxf.jaxrs.systests.CustomerService"
/&gt;

  &lt;/**jaxrs:serviceBeans**&gt;

  &lt;**jaxrs:extensionMappings**&gt;

    &lt;**entry** key="json" value="application/json"/&gt;

    &lt;**entry** key="xml" value="application/xml"/&gt;

  &lt;/**jaxrs:extensionMappings**&gt;

  &lt;**jaxrs:languageMappings**&gt;

     &lt;**entry** key="en" value="en-gb"/&gt; 

  &lt;/**jaxrs:languageMappings**&gt;

&lt;/**jaxrs:server**&gt;

 

**Logging**

Many of the existing CXF features can be applied either
to jaxrs:server or jaxrs:client. For example, to enable logging of
requests and responses, simply do:

&lt;**beans** xmlns:cxf="<http://cxf.apache.org/core>"

   xsi:schemaLocation="<http://cxf.apache.org/core>

      <http://cxf.apache.org/schemas/core.xsd>"&gt;

&lt;**jaxrs:server**&gt;

&lt;**jaxrs:features**&gt;

     &lt;**cxf:logging**/&gt;

&lt;/**jaxrs:features**&gt;

&lt;**jaxrs:server**&gt;

&lt;/**beans**&gt;

 

 

 

 

 

Jaxb

Friday, September 18, 2015

15:47

 

The request and response can be marshalled and unmarshalled to/from Java
object using JAXB.

There's a number of ways to tell to the JAXB provider how objects can be
serialized. The simplest way is to mark a given type with
@XmlRootElement annotation.

For example:

@XmlRootElement(name = "Customer")

**public** **class** Customer {

    **private** String name;

    **private** **long** id;

 

    **public** Customer() {

    }

 

    **public** **void** setName(String n) {

        name = n;

    }

 

    **public** String getName() {

        **return** name;

    }

 

    **public** **void** setId(**long** i) {

        id = i;

    }

 

    **public** **long** getId() {

        **return** id;

    }

}

 

 

In the example below, the Customer object returned by getCustomer is
marshaled using JAXB data binding:

@Path("/customerservice/")

**public** **class** CustomerService {

    @GET

    @Path("/customers/{customerId}/")

    **public** Customer getCustomer(@PathParam("customerId") String id)
{

        ....

    }

}

 

 

**JSON support**

 

Following code returns a Customer object that is marshaled to JSON
format:

@Path("/customerservice/")

**public** **class** CustomerService {

    @Produces("application/json")

    @GET

    @Path("/customers/{customerId}/")

    **public** Customer getCustomer(@PathParam("customerId") String id)
{

        ....

    }

 

 

**Jackson**

 

If you prefer working with Jackson JSON providers then register either
JacksonJsonProvider:

&lt;**jaxrs:providers**&gt;

   &lt;**bean**
class="org.codehaus.jackson.jaxrs.JacksonJsonProvider"/&gt;

&lt;/**jaxrs:providers**&gt;

or JacksonJaxbJsonProvider (when working with JAXB beans):

&lt;**jaxrs:providers**&gt;

   &lt;**bean**
class="org.codehaus.jackson.jaxrs.JacksonJaxbJsonProvider"/&gt;

&lt;/**jaxrs:providers**&gt;

and add this Maven dependency:

&lt;**dependency**&gt;

  &lt;**groupId**&gt;org.codehaus.jackson&lt;/**groupId**&gt;

  &lt;**artifactId**&gt;jackson-jaxrs&lt;/**artifactId**&gt;

  &lt;**version**&gt;1.9.0&lt;/**version**&gt;

&lt;/**dependency**&gt;

 

 

 

 

 

 

 

**Filters**

Friday, September 18, 2015

15:52

 

Often it's necessary to pre- or post-process some requests according to
a number of requirements.

For example, a request like

GET /resource?\_type=xml is supported by a CXF specific RequestHandler
filter which modifies the CXF input Message 

by updating one of its headers.

In some cases users can use the existing filter technologies such as
Servler filters or Spring AOP proxies. In other cases, it can be handy

to write a CXF filter which will introspect the resource class, input or
output message, the operation which was invoked and modify the request
or response accordingly.

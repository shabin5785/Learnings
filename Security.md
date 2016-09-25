Oauth + Saml

Friday, July 10, 2015

11:28

How to integrate Spring-oAuth2 with Spring-SAML

[**Ohad
Redlich**](http://www.codeproject.com/script/Membership/View.aspx?mid=1287966), 5
Jun 2013 [CPOL](http://www.codeproject.com/info/cpol10.aspx)

![](media/image1.png){width="0.16666666666666666in"
height="0.16666666666666666in"}

 22.9K

![](media/image2.png){width="0.16666666666666666in"
height="0.16666666666666666in"}

 8

Please [sign
in](http://www.codeproject.com/script/Membership/LogOn.aspx) to vote

This document describes how to integrate the Spring-Security-oAuth2
project with Spring-Security-SAML.

Introduction 

This document describes how to integrate the Spring-Security-oAuth2
project with Spring-Security-SAML.

I assume the reader is familiar with both oAuth and its components, and
SAML and its components.

Motivation

Suppose you want your system to support oAuth2.  I would recommend using
the Spring-Security-oAuth project. When you use Spring, you enjoy the
many benefits of this open-source package: it is widely used, there is
responsive support (in the forum), it is open source, and much more.
This package allows the developer to write an oAuth-client, an oAuth
resource server, or an oAuth authorization server.

Let us discuss SAML.  If you want to implement your own SAML SP (Service
Provider), I recommend using Spring-Security-SAML, for the same reasons
I recommended Spring-security-oAuth, above.

Now, consider an application that authenticates its users with oAuth,
meaning the application is an "oAuth resource server", and its clients
implement the oAuth protocol, meaning they are "oAuth clients".  I was
asked to enable this application to connect SAML IdPs (identity
providers) and authenticate users in front of them. This means the
application must support not only oAuth, but SAML as well. Note,
however, that if the application supports SAML, changes would have to be
made in all clients, not only in the application itself. Currently the
clients are "oAuth clients", (i.e., they fulfill the oAuth protocol). If
the application supports SAML as well, the clients will also have to
support it on their side. In SAML, the redirects are implemented
differently, and the requests are different. So, the question is, how
can we make this application support SAML without changing all clients?

The solution is to create an application ("the bridge") that will be a
bridge between oAuth and SAML. When a non-authorized client tries to
access the protected resource, it is redirected to the authorization
server (this is how oAuth works). But here is the trick: from the
client’s point of view– and from the application itself – this bridge
functions as a valid "oAuth authorization server". Therefore, there is
no need to change anything, not in the client code and not in the
application code. On the other hand, instead of opening a popup dialog
with username and password, this server functions as an SP and redirects
the user to authenticate in front of a pre-configured IdP. 

Get to Business

How oAuth works

Let us start with a brief description of how oAuth works. OAuth supports
several flows (called "Authorization Grants"); in this document I will
discuss the grant called "authorization code". The other grants can be
implemented similarly.

From the [spec](http://tools.ietf.org/html/rfc6749#section-1.3.1):

In the "authorization code" flow, the authorization code is obtained by
using an authorization server    as an intermediary between the client
and resource owner.  Instead of requesting authorization directly from
the resource owner, the client directs the resource owner to an
authorization server (via its user-agent = the browser), which in turn
directs the resource owner back to the client with the authorization
code.

Before directing the resource owner back to the client with the
authorization code, the authorization server authenticates the resource
owner and obtains authorization.  Because the resource owner only
authenticates with the authorization server, the resource   owner's
credentials are never shared with the client.

The authorization code provides a few important security benefits such
as the ability to authenticate the client, and the transmission of the
access token directly to the client without passing it through the
resource owner's user-agent, potentially exposing it to others,
including the resource owner. 

![](media/image3.jpg){width="6.0in" height="4.510416666666667in"}

How SAML works 

![](media/image4.jpg){width="6.354166666666667in"
height="4.177083333333333in"}

When the user wants to get to a protected resource (=service provider,
or SP) using a web browser, he navigates to that webpage. The SP will
not ask for a username and password to log in, but instead redirect the
browser to the IDP for authentication.

Embedded within this redirect message (as the SAMLRequest parameter) is
a SAML authentication request message. As SAML is XML-based the complete
authentication request message is compressed (to save space in the URL)
and encoded (because many characters are not allowed in URLs).

When the IDP receives this message and decides to grant the SP’s
request, it will authenticate the user by asking him to enter his
credentials (unless he already did – for example when having logged in
at another service earlier – in which case single sign-on is triggered
by simply skipping authentication). After successful authentication, the
user’s browser is sent back to the SP at the so called
AssertionConsumerService URL. As before, a SAML protocol message is
piggybacking  along – this time carrying a SAML authentication response
message.

Spring configurations

As mentioned earlier, amongst Spring’s benefits are its flexibility and
configurability. One can develop oAuth or SAML projects with minimal
POJO classes; most of the work is done via the beans configuration. It
is up to the developer to decide whether the basic implementation of
Spring suits him, or whether he should configure the application
differently, or even implement his own classes.

The Spring configurations (XML beans file) for the oAuth authorization
server looks something like this (I’ve pasted only the relevant beans):

Hide   Shrink 

![](media/image5.png){width="0.16666666666666666in"
height="0.16666666666666666in"}

   Copy Code

&lt;!-- *Protect the /oauth/token url to allow only registered clients*
--&gt;\
&lt;security:http pattern="/oauth/token"\
authentication-manager-ref="clientAuthenticationManager"&gt;\
&lt;security:intercept-url pattern="/oauth/token"\
access="ROLE\_CLIENT" requires-channel="https"/&gt;\
&lt;security:anonymous enabled="false" /&gt;\
&lt;security:http-basic /&gt;\
\
&lt;security:custom-filter\
ref="clientCredentialsTokenEndpointFilter"\
before="BASIC\_AUTH\_FILTER" /&gt;\
&lt;/security:http&gt;\
\
\
&lt;security:http auto-config="true"\
authentication-manager-ref="usersAuthManager"&gt;\
&lt;security:intercept-url pattern="/oauth/\*\*" access="ROLE\_USER"
/&gt;\
&lt;security:intercept-url pattern="/\*\*"
access="IS\_AUTHENTICATED\_FULLY"/&gt;\
&lt;security:anonymous enabled="false"/&gt;\
&lt;/security:http&gt;

&lt;security:authentication-manager alias="usersAuthManager"&gt;\
&lt;security:authentication-provider
user-service-ref="userDetailsService"/&gt;\
&lt;/security:authentication-manager&gt;\
\
&lt;security:user-service id="userDetailsService"&gt;\
&lt;security:user name="demo1@company.com"\
password="pass" authorities="ROLE\_USER" /&gt;\
&lt;security:user name="demo2@company.com"\
password="demo" authorities="ROLE\_USER" /&gt;\
&lt;/security:user-service&gt;

&lt;bean id="clientCredentialsTokenEndpointFilter"\
class="org.springframework.security.oauth2.provider.\
client.ClientCredentialsTokenEndpointFilter"&gt;\
&lt;property name="authenticationManager"
ref="clientAuthenticationManager" /&gt;\
&lt;/bean&gt;

&lt;!-- *OAuth2 Configuration* --&gt;\
&lt;oauth:authorization-server\
client-details-service-ref="clientDetails"\
token-services-ref="watchdoxAuthorizationServerTokenServices"\
user-approval-handler-ref="automaticUserApprovalHandler"&gt;\
&lt;oauth:authorization-code /&gt;\
&lt;oauth:implicit /&gt;\
&lt;oauth:refresh-token /&gt;\
&lt;oauth:client-credentials /&gt;\
&lt;oauth:password /&gt;\
&lt;/oauth:authorization-server&gt;\
\
&lt;security:authentication-manager
id="clientAuthenticationManager"&gt;\
&lt;security:authentication-provider
user-service-ref="clientDetailsUserService" /&gt;\
&lt;/security:authentication-manager&gt;\
\
&lt;bean id="clientDetailsUserService"\
class="org.springframework.security.oauth2...ClientDetailsUserDetailsService"&gt;\
&lt;constructor-arg ref="clientDetails" /&gt;\
&lt;/bean&gt;\
\
&lt;bean id="clientDetails"\
class="org.springframework.security.oauth2...JdbcClientDetailsService"&gt;\
&lt;constructor-arg ref="dataSource" /&gt;\
&lt;/bean&gt;

&lt;bean id="dataSource" ...&gt;\
… DataSource configurations here\
&lt;/bean&gt;

The [Spring configurations for SAML
SP](https://github.com/SpringSource/spring-security-saml/blob/master/saml2-sample/src/main/resources/security/securityContext.xml) can
be found in
the [Spring-Security-SAML-sample](https://github.com/SpringSource/spring-security-saml) project,
so I will not include it here.

Now, we have to understand how to integrate these two projects.

Integrating Spring’s oAuth and SAML

As mentioned earlier, our application is an oAuth authorization server.
We would like to configure this application so it will also be a SAML
SP. By doing this, every time a user is redirected to our application in
order to authenticate, we will redirect him again to the SAML IdP.
Technically, redirecting the user to the IdP means creating a SAML
request. So, our application must have the capability to process SAML
responses that come from that IdP.

Importing the saml-securityContext.xml

From the beans.xml file of our application, we have to add all the SAML
beans that are declared in the *saml-securityContext.xml*:

Hide   Copy Code

&lt;import resource=*"classpath:saml-securityContext.xml"*/&gt;

SAML Entry point 

The first thing to note in SAML properties is that in the main http
block there is a declaration of the entry-point:  

Hide   Copy Code

entry-point-ref=*"samlEntryPoint"*

Generally, it means that whenever a relevant http call tries to access
this app, this is the entry-point that handles the request. In the SAML
case, samlEntryPoint (class SAMLEntryPoint) checks if the IdP is known;
if not, it starts a discovery process, otherwise it initializes the SSO
process – this generates the SAML request to the IdP.

Obviously, we need this functionality. So we will declare our web
application as a "protected resource", so that every time the user tries
to authenticate, the SAML process will occur. We achieve this by
changing  the http block that handles the  /oAuth/authorize call, and
setting its endpoint filter to point to "samlEntryPoint".

Hide   Copy Code

&lt;security:http entry-point-ref=*"samlEntryPoint"*&gt;

User’s Authentication Manager

As you can see in the code above, the same http block that we discussed
also points to an Authentication Manager:

Hide   Copy Code

...authentication-manager-ref=*"usersAuthManager"*&gt;

This Authentication Manager is the one that is responsible for the
user’s authentication. Within it, there is a declaration of the
provider, which holds the users and passwords. Of course, in real world
implementations, this provider directs to a JDBC, where all users are
stored with their encrypted passwords. The good news here is, we do not
have to handle any users and passwords, since we delegate this to the
IdP. So, we change the declaration of our server to point to the
authentication manager of the SAML SP: this manager has a provider
(SAMLAuthenticationProvider or some other class that extends it). This
class implements theauthenticate() method, that attempts to perform
authentication of an Authentication object. 

MetadataGeneratorFilter 

This is a filter that automatically generates default SP metadata. To
include it in our filter chain, it has to be declared as the first
element in the chain of the http block we saw above:

Hide   Copy Code

&lt;security:custom-filter before=*"FIRST"*
ref=*"metadataGeneratorFilter"*/&gt;

SAML Filter Chain 

Working with Spring-SAML requires several filters to be added to the
chain, such as logout filter, metadata display filter and a few more.
Spring-SAML creates a dedicated chain for this, that should be run right
after theBASIC\_AUTH\_FILTER. So, in the http block (yes, the same one…)
we add the following:

Hide   Copy Code

&lt;security:custom-filter after=*"BASIC\_AUTH\_FILTER"*
ref=*"samlFilter"*/&gt;

To Sum Up  

We end up with these changes only; all other beans remain unchanged:

Hide   Copy Code

&lt;import resource="classpath:saml-securityContext.xml"/&gt;\
&lt;security:http authentication-manager-ref="authenticationManager"\
entry-point-ref="samlEntryPoint"&gt;\
&lt;security:intercept-url pattern="/oauth/\*\*" access="ROLE\_USER"
/&gt;\
&lt;security:intercept-url pattern="/\*\*"
access="IS\_AUTHENTICATED\_FULLY"/&gt;\
\
&lt;security:anonymous enabled="false"/&gt;\
\
&lt;security:custom-filter before="FIRST"
ref="metadataGeneratorFilter"/&gt;\
&lt;security:custom-filter after="BASIC\_AUTH\_FILTER"
ref="samlFilter"/&gt;\
&lt;/security:http&gt;

The Token

Some of you may be asking – hey, what about the token?

Ah!

Until now, everything works great; Spring SAML makes sure we have a
valid Authentication object in theSecurityContextHolder (actually, it is
of type ExpiringUsernameAuthenticationToken); thanks to this, we are
able to get the authorization code and then the access token. The user
is happy, and we are all happy. But what happens when we want to get
some information from the SAML token (e.g. the user’s name or email) and
create an oAuth token that contains them? In this case (not a rare one,
actually) we need to  become a bit more familiar with
how SAMLAuthenticationProvider works.

SAMLAuthenticationProvider is autowired to the authentication manager
thanks to the *SAML-securityContext.xml* (as [discussed
above](file:///C:\Users\Ohad\Google%20Drive\WD%20documents\oauth2%20saml%20integration.docx#_User’s_Authentication_Manager)).
The authentication manager calls
theSAMLAuthenticationProvider.authenticate() method and passes it the
Authentication object, which is of type SAMLAuthenticationToken. This
method validates the token, parses it and makes all necessary checks to
make sure it corresponds to the SAMLRequest. Then – and this is the
interesting part– it tries to load the user’s details from the SAML
credentials (parsed earlier from the response). How does this happen? It
checks if there is a SAMLUserDetailsService object available; if there
is none, it returns null (as it did in our case till now) and this is
fine, but it does not use the details from the SAML token. If, however,
there *is* aSAMLUserDetailsService object, it calls
its loadUserBySaml() method.

Now, we have to ensure that there is a SAMLUserDetailsService object
attached. We do this by implementing one by ourselves, and annotating it
as "Component" so it will be autowired to theSAMLAuthenticationProvider.

Hide   Copy Code

*/\*\*\
\* this class is autowired to the SamlProvider, so it tries to get the
user's details from the token using this\
\* class, o/w it returns null.\
\* @author Ohad\
\*\
\*/*\
@Component\
public class SAMLUserDetailsServiceImpl implements
SAMLUserDetailsService\
{\
@Override\
public Object loadUserBySAML(SAMLCredential credential)\
throws UsernameNotFoundException\
{\
List&lt;GrantedAuthority&gt; authorities = new
ArrayList&lt;GrantedAuthority&gt;();\
String email = credential.getNameID().getValue();\
GrantedAuthority authority = new SimpleGrantedAuthority("ROLE\_USER");\
authorities.add(authority);\
\
UserDetails userDetails = new User(\
email, "password", true, true, true, true, authorities);\
\
return userDetails;\
}\
}

The provider then takes the UserDetails object and sets it to the
Authentication object that it creates. Now we have access to these
details so we can call the SecurityContextHolder.getAuthentication() and
get them. When we do this? Spring’s TokenEndpoint.getAccessToken() calls
implicitly to the  tokenServices bean, to create the access token.
Spring’s default token-services is DefaultTokenServices, which does not
use the ‘name’ field of the given Authentication object. (Actually, it
uses a random UUID). To overcome this, we create our own token-service
that will do this work. Note that its bean name has to be attached
properly in the XML file:

Hide   Copy Code

&lt;!-- *OAuth2 Configuration* --&gt;\
&lt;oauth:authorization-server\
        token-services-ref="myAuthorizationServerTokenServices"\
...

Below is an example for such token service:

Hide   Copy Code

@Component("myAuthorizationServerTokenServices")\
public class OAuth2TokenServices implements
AuthorizationServerTokenServices, InitializingBean\
{\
        @Override\
        public OAuth2AccessToken createAccessToken(OAuth2Authentication
authentication) throws AuthenticationException\
        {\
                        String email = authentication.getName();\
                        String generatedToken = generate the Token with
the 'email'\
                        DefaultOAuth2AccessToken result = new
DefaultOAuth2AccessToken( generatedToken );\
                        result.setExpiration( expiration );\
                        result.setTokenType("Bearer");\
                        ...\
                        return result;\
        }\
}

Summary  

We have seen how to integrate two different Spring projects, each
handling a different authentication mechanism, and by integrating them
have achieved a bridge that, from the clients’ side, remains an oAuth
authentication server, but allows the application to connect and
authenticate in front of SAML IdPs.

Many thanks to **David Goldhar** for his help with this document! 

References

 

From
&lt;<http://www.codeproject.com/Articles/598581/How-to-integrate-Spring-oAuth-with-Spring-SAML>&gt;

 

 

 

 

&lt;&lt;oauth and saml config.txt&gt;&gt;

 

 

 

Waffle

Friday, July 10, 2015

13:49

 

[**Single Sign-On: Spring-Security Negotiate Filter (Kerberos + NTLM)
w/Waffle**](http://code.dblock.org/2010/07/09/single-sign-on-spring-security-negotiate-filter-kerberos-ntlm-wwaffle.html)

![](media/image6.jpg){width="3.6979166666666665in" height="0.71875in"}

In this post I’ll explain how to configure the Waffle Spring-Security
Negotiate filter to do single-sign-on on Windows and touch on how much
more elegant the spring-based filter configuration is versus, for
example, a generic servlet filter.

**Download**

Download [Waffle](https://github.com/dblock/waffle). The zip
contains *Waffle.chm* with the latest version of this tutorial.

**Configure Your Application**

*Configure Spring-Security*

We’ll assume
that [Spring-Security](http://static.springsource.org/spring-security/site/) is
configured via web.xml with a filter chain and a
Spring*ContextLoaderListener*. The Waffle beans configuration will be
added to *waffle-filter.xml*.

&lt;filter&gt;\
&lt;filter-name&gt;springSecurityFilterChain&lt;/filter-name&gt;\
&lt;filter-class&gt;org.springframework.web.filter.DelegatingFilterProxy&lt;/filter-class&gt;\
&lt;/filter&gt;\
&lt;filter-mapping&gt;\
&lt;filter-name&gt;springSecurityFilterChain&lt;/filter-name&gt;\
&lt;url-pattern&gt;/\*&lt;/url-pattern&gt;\
&lt;/filter-mapping&gt;\
&lt;context-param&gt;\
&lt;param-name&gt;contextConfigLocation&lt;/param-name&gt;\
&lt;param-value&gt;/WEB-INF/waffle-filter.xml&lt;/param-value&gt;\
&lt;/context-param&gt;\
&lt;listener&gt;\
&lt;listener-class&gt;org.springframework.web.context.ContextLoaderListener&lt;/listener-class&gt;\
&lt;/listener&gt;

*Package Files*

You need waffle-jna.jar, jna.jar, platform.jar and
commons-logging-1.1.1.jar from the Waffle distribution as well as Spring
and Spring-security JARs. Those should be placed in your application’s
classpath (eg. packaged in WAR). If you’re using Tomcat, for demo
purposes you can put these files in Tomcat’s *lib*.

*Windows Authentication Provider*

Declare a Windows Authentication provider. This is the link between
Waffle and the operating system.

&lt;bean id="waffleWindowsAuthProvider"
class="waffle.windows.auth.impl.WindowsAuthProviderImpl" /&gt;

*Waffle Security Filter Providers*

Declare a collection of Waffle security filter providers that implement
various authentication protocols.

&lt;bean id="negotiateSecurityFilterProvider"
class="waffle.servlet.spi.NegotiateSecurityFilterProvider"&gt;\
&lt;constructor-arg ref="waffleWindowsAuthProvider" /&gt;\
&lt;/bean&gt;

&lt;bean id="basicSecurityFilterProvider"
class="waffle.servlet.spi.BasicSecurityFilterProvider"&gt;\
&lt;constructor-arg ref="waffleWindowsAuthProvider" /&gt;\
&lt;/bean&gt;

&lt;bean id="waffleSecurityFilterProviderCollection"
class="waffle.servlet.spi.SecurityFilterProviderCollection"&gt;\
&lt;constructor-arg&gt;\
&lt;list&gt;\
&lt;ref bean="negotiateSecurityFilterProvider" /&gt;\
&lt;ref bean="basicSecurityFilterProvider" /&gt;\
&lt;/list&gt;\
&lt;/constructor-arg&gt;\
&lt;/bean&gt;

If you’re not very familiar with Spring, you will start loving it right
here. We’re adding two providers to a collection in a configuration
file. This means that we don’t need to have another configuration
mechanism than this one to add or remove one. We don’t need to do this
in code either. Each class instance (bean) is also configurable
individually – we can, for example, configure the name of the realm for
Basic authentication.

&lt;bean id="basicSecurityFilterProvider"
class="waffle.servlet.spi.BasicSecurityFilterProvider"&gt;\
&lt;constructor-arg ref="waffleWindowsAuthProvider" /&gt;\
&lt;property name="Realm" value="DemoRealm" /&gt;\
&lt;/bean&gt;

It’s more verbose, but it’s much more flexible.

*Add a Waffle Security Filter*

Add the Waffle security filter and entry point to
the *sec:http* configuration section. The filter will be placed before
the Basic authentication filter that ships with Spring-Security. The
filter uses the collection of authentication filter providers defined
above to perform authentication.

&lt;sec:http entry-point-ref="negotiateSecurityFilterEntryPoint"&gt;\
&lt;sec:intercept-url pattern="/\*\*" access="IS\_AUTHENTICATED\_FULLY"
/&gt;\
&lt;sec:custom-filter ref="waffleNegotiateSecurityFilter"
position="BASIC\_AUTH\_FILTER" /&gt;\
&lt;/sec:http&gt;

&lt;bean id="negotiateSecurityFilterEntryPoint"
class="waffle.spring.NegotiateSecurityFilterEntryPoint"&gt;\
&lt;property name="Provider"
ref="waffleSecurityFilterProviderCollection" /&gt;\
&lt;/bean&gt;

*Spring-Security Authentication Manager*

Define a required default Spring-Security authentication manager. We’re
not going to use it in this setup because the filter takes care of
authentication and the user doesn’t have a way to supply, for example, a
username and password.

&lt;sec:authentication-manager alias="authenticationProvider" /&gt;

Note that Waffle does include a Spring-based authentication manager for
form-based authentication or non-web-based scenarios.

*The Filter Itself*

Finally, define the Spring-Security Waffle filter that uses the
collection of security filter providers to perform authentication.

&lt;bean id="waffleNegotiateSecurityFilter"
class="waffle.spring.NegotiateSecurityFilter"&gt;\
&lt;property name="Provider"
ref="waffleSecurityFilterProviderCollection" /&gt;\
&lt;/bean&gt;

**Demo Application**

A demo application with the complete configuration file can be found in
the Waffle distribution in
the *Samples\\waffle-spring-filter* directory. Copy the entire directory
into Tomcat’s webapps directory and navigate to
<http://localhost:8080/waffle-spring-filter>. You should be
automatically logged-in under your current Windows account.

**Links**

-   [Spring-Security](http://static.springsource.org/spring-security/site/)

-   [Waffle](https://github.com/dblock/waffle)

 

From
&lt;<http://code.dblock.org/2010/07/09/single-sign-on-spring-security-negotiate-filter-kerberos-ntlm-wwaffle.html>&gt;

 

 

 

Java security

Tuesday, February 02, 2016

15:11

Input into a system should be checked so that it will not cause
excessive resource consumption disproportionate to that used to request
the service. Common affected resources are CPU cycles, memory, disk
space, and file descriptors. Don’t keep files open. Use the new try with
resource option. The try-with-resource syntax introduced in Java SE 7
automatically handles the release of many resource types

 

 

Image size attacks?

 

Billion laughs attack" whereby XML entity expansion causes an XML
document to grow dramatically during parsing. Set the
XMLConstants.FEATURE\_SECURE\_PROCESSING  feature to enforce reasonable
limits.

 

Have proper hashcode implementation to avoid O(n) to become O(n)2

Heavy Regular expressions may exhibit catastrophic backtracking

Detailed logging of unusual behavior may result in excessive output to
log files.

 

Some objects, such as open files, locks and manually allocated memory,
behave as resources which require every acquire operation to be paired
with a definite release. It is easy to overlook the vast possibilities
for executions paths when exceptions are thrown. Resources should always
be released promptly no matter what.

 

Purge sensitive information from exceptions such as filename and home
directory paths etc…

Internal exceptions should be caught and sanitized before propagating
them to upstream callers. The type of an exception may reveal sensitive
information, even if the message has been removed. For
instance, FileNotFoundException reveals whether or not a given file
exists.

 

Exceptions may also include sensitive information about the
configuration and internals of the system. Do not pass exception
information to end users unless one knows exactly what it contains. For
example, do not include exception stack traces inside HTML comments.

 

Some information, such as Social Security numbers (SSNs) and passwords,
is highly sensitive. This information should not be kept for longer than
necessary nor where it may be seen, even by administrators. For
instance, it should not be sent to log files and its presence should not
be detectable through searches. Some transient data may be kept in
mutable data structures, such as char arrays, and cleared immediately
after use. Clearing data structures has reduced effectiveness on typical
Java runtime systems as objects are moved in memory transparently to the
programmer.

 

To narrow the window when highly sensitive information may appear in
core dumps, debugging, and confidentiality attacks, it may be
appropriate to zero memory containing the data immediately after use
rather than waiting for the garbage collection mechanism.However, doing
so does have negative consequences. Code quality will be compromised
with extra complications and mutable data structures. Libraries may make
copies, leaving the data in memory anyway. The operation of the virtual
machine and operating system may leave copies of the data in memory or
even on disk.

 

Attacks using maliciously crafted inputs to cause incorrect formatting
of outputs are
well-documented [\[7\]](http://www.oracle.com/technetwork/java/seccodeguide-139067.html#ref-7).
Such attacks generally involve exploiting special characters in an input
string, incorrect escaping, or partial removal of special characters.
Parsing and canonicalization should be done before validation.

 

It is well known that dynamically created SQL statements including
untrusted input are subject to command injection. This often takes the
form of supplying an input containing a quote character (') followed by
SQL. Avoid dynamic SQL.

For parameterised SQL statements using Java Database Connectivity
(JDBC),
usejava.sql.PreparedStatement or java.sql.CallableStatement instead
ofjava.sql.Statement

 

 

Untrusted data should be properly sanitized before being included in
HTML or XML output. Failure to properly sanitize the data can lead to
many different security problems, such as Cross-Site Scripting (XSS) and
XML Injection vulnerabilities. It is important to be particularly
careful when using Java Server Pages (JSP).

 

 

A Java package comprises a grouping of related Java classes and
interfaces. Declare any class or interface public if it is specified as
part of a published API, otherwise, declare it package-private.
Similarly, declare class members and constructors (nested classes,
methods, or fields) public or protected as appropriate, if they are also
part of the API. Otherwise, declare them private or package-private to
avoid exposing the implementation. Note that members of interfaces are
implicitly public.

 

Containers may hide implementation code by adding to
the package.access security property. This property prevents untrusted
classes from other class loaders linking and using reflection on the
specified package hierarchy. Care must be taken to ensure that packages
cannot be accessed by untrusted contexts before this property has been
set.This example code demonstrates how to append to
the package.access security property. Note that it is not thread-safe.
This code should generally only appear once in a system.

 

Design classes and methods for inheritance or declare them
final [\[6\]](http://www.oracle.com/technetwork/java/seccodeguide-139067.html#ref-6).
Left non-final, a class or method can be maliciously overridden by an
attacker. A class that does not permit subclassing is easier to
implement and verify that it is secure. Prefer composition to
inheritance.

 

 

Subclasses do not have the ability to maintain absolute control over
their own behavior. A superclass can affect subclass behavior by
changing the implementation of an inherited method that is not
overridden. If a subclass overrides all inherited methods, a superclass
can still affect subclass behavior by introducing new methods. Such
changes to a superclass can unintentionally break assumptions made in a
subclass and lead to subtle security vulnerabilities.

The Hashtable class was enhanced in JDK 1.2 to include a new method,
entrySet, which supports the removal of entries from the Hashtable. The
Provider class was not updated to override this new method. This
oversight allowed an attacker to bypass the SecurityManager check
enforced in Provider.remove, and to delete Provider mappings by simply
invoking the Hashtable.entrySet method.The primary flaw is that the data
belonging to Provider (its mappings) is stored in the Hashtable class,
whereas the checks that guard the data are enforced in the Provider
class. This separation of data from its corresponding SecurityManager
checks only exists because Provider extends from Hashtable. Because a
Provider is not inherently a Hashtable, it should not extend from
Hashtable. Instead, the Provider class should encapsulate a Hashtable
instance allowing the data and the checks that guard that data to reside
in the same class. The original decision to subclass Hashtable likely
resulted from an attempt to achieve code reuse, but it unfortunately led
to an awkward relationship between a superclass and its subclasses, and
eventually to a security vulnerability.

 

Input from untrusted sources must be validated before use. Maliciously
crafted inputs may cause problems, whether coming through method
arguments or external streams. Examples include overflow of integer
values and directory traversal attacks by including "../" sequences in
filenames

 

 

Making classes immutable prevents the issues associated with mutable
objects (described in subsequent guidelines) from arising in client
code. Immutable classes should not be subclassable. Further, hiding
constructors allows more flexibility in instance creation and caching.
This means making the constructor private or default access
("package-private"), or being in a package controlled by the
package.access security property. Immutable classes themselves should
declare fields final and protect against any mutable inputs and outputs

 

 

If a method returns a reference to an internal mutable object, then
client code may modify the internal state of the instance. Unless the
intention is to share state, copy mutable objects and return the copy.

 

 

Mutable objects may be changed after and even during the execution of a
method or constructor call. Types that can be subclassed may behave
incorrectly, inconsistently, and/or maliciously. If a method is not
specified to operate directly on a mutable input parameter, create a
copy of that input and perform the method logic on the copy.

 

 

When designing a mutable value class, provide a means to create safe
copies of its instances. This allows instances of that class to be
safely passed to or returned from methods in other classes (see
Guideline 6-2 and Guideline 6-3). This functionality may be provided by
a static creation method, a copy constructor, or by implementing a
public copy method (for final classes).If a class is final and does not
provide an accessible method for acquiring a copy of it, callers could
resort to performing a manual copy. This involves retrieving state from
an instance of that class and then creating a new instance with the
retrieved state. Mutable state retrieved during this process must
likewise be copied if necessary. Performing such a manual copy can be
fragile. If the class evolves to include additional state, then manual
copies may not include that state. The java.lang.Cloneable mechanism is
problematic and should not be used. Implementing classes must explicitly
copy all mutable fields which is highly error-prone. Copied fields may
not be final. The clone object may become available before field copying
has completed, possibly at some intermediate stage. In non-final classes
Object.clone will make a new instance of the potentially malicious
subclass. Implementing Cloneable is an implementation detail, but
appears in the public interface of the class.

 

Overridable methods may not behave as expected.For instance, when
expecting identity equality behavior, Object.equals may be overridden to
return true for different objects. In particular when used as a key in a
Map, an object may be able to pass itself off as a different object that
it should not have access to

 

Callers can trivially access and modify public non-final static fields.
Neither accesses nor modifications can be guarded against, and newly set
values cannot be validated. Fields with subclassable types may be set to
objects with malicious implementations. Always declare public static
fields as final

 

Only immutable values should be stored in public static fields. Many
types are mutable and are easily overlooked, in particular arrays and
collections. Mutable objects that are stored in a field whose type does
not have any mutator methods can be cast back to the runtime type. Enum
values should never be mutable

 

Private statics are easily exposed through public interfaces, if
sometimes only in a limited way (see Guidelines 6-2 and 6-6). Mutable
statics may also change behaviour between unrelated code. To ensure safe
code, private statics should be treated as if they are public. Adding
boilerplate to expose statics as singletons does not fix these issues.

 

Classes that expose Collections either through public variables or get
methods have the potential for side effects, where calling classes can
modify contents of the Collection. Developers should consider exposing
read-only copies of Collections relating to security authentication or
internal state.While a Collection object reference can be made immutable
through the final keyword described in Guideline 6-9, the actual
contents of the collection must be made immutable separately through the
Collections.unmodifiable... APIs.

 

Construction of classes can be more carefully controlled if constructors
are not exposed. Define static factory methods instead of public
constructors. Support extensibility through delegation rather than
inheritance. Implicit constructors through serialization and clone
should also be avoided.

 

Where an existing API exposes a security-sensitive constructor, limit
the ability to create instances. A security-sensitive class enables
callers to modify or circumventSecurityManager access controls. Any
instance of ClassLoader, for example, has the power to define classes
with arbitrary security permissions.To restrict untrusted code from
instantiating a class, enforce a SecurityManager check at all points
where that class can be instantiated. In particular, enforce a check at
the beginning of each public and protected constructor. In classes that
declare public static factory methods in place of constructors, enforce
checks at the beginning of each factory method. Also enforce checks at
points where an instance of a class can be created without the use of a
constructor. Specifically, enforce a check inside
the readObject orreadObjectNoData method of a serializable class, and
inside the clone method of a cloneable class.

 

When a constructor in a non-final class throws an exception, attackers
can attempt to gain access to partially initialized instances of that
class. Ensure that a non-final class remains totally unusable until its
constructor completes successfully. From JDK 6 on, construction of a
subclassable class can be prevented by throwing an exception before the
Object constructor completes.

 

Constructors that call overridable methods give attackers a reference to
this (the object being constructed) before the object has been fully
initialized. Likewise, clone, readObject, or readObjectNoData methods
that call overridable methods may do the same. The readObject methods
will usually call java.io.ObjectInputStream.defaultReadObject, which is
an overridable method.

 

A non-final class may be subclassed by a class that also implements
java.lang.Cloneable. The result is that the base class can be
unexpectedly cloned, although only for instances created by an
adversary. The clone will be a shallow copy. The twins will share
referenced objects but have different fields and separate intrinsic
locks

 

Making a class serializable effectively creates a public interface to
all fields of that class. Serialization also effectively adds a hidden
public constructor to a class, which needs to be considered when trying
to restrict object construction.

 

 

Once an object has been serialized the Java language's access controls
can no longer be enforced and attackers can access private fields in an
object by analyzing its serialized byte stream. Therefore, do not
serialize sensitive data in a serializable class.

Approaches for handling sensitive fields in serializable classes are:

Declare sensitive fields transient

Define the serialPersistentFields array field appropriately

Implement writeObject and use ObjectOutputStream.putField selectively

Implement writeReplace to replace the instance with a serial proxy

Implement the Externalizable interface

 

Deserialization creates a new instance of a class without invoking any
constructor on that class. Therefore, deserialization should be designed
to behave like normal construction.

 

Prevent an attacker from using serialization or deserialization to
bypass theSecurityManager checks enforced in a class. Specifically, if a
serializable class enforces a SecurityManager check in its constructors,
then enforce that same check in areadObject or readObjectNoData method
implementation. Otherwise an instance of the class can be created
without any check via deserialization.

 

 

Callback methods are generally invoked from the system with full
permissions. It seems reasonable to expect that malicious code needs to
be on the stack in order to perform an operation, but that is not the
case. Malicious code may set up objects that bridge the callback to a
security checked operation. For instance, a file chooser dialog box that
can manipulate the filesystem from user actions, may have events posted
from malicious code. Alternatively, malicious code can disguise a file
chooser as something benign while redirecting user events.

 

---------------------------------------------------------------------------------------------------------

 

 

Put simply, don't have public fields or methods in a class unless
required. Every method, field, or class that is not private is a
potential avenue of attack. Provide accessors to them so you can limit
their accessibility.

 

Non-Final classes let an attacker extend a class in a malicious manner.
An application may have a USER object which by design would never be
extended, so implementing this class as Final would prevent malicious
code extending the user class. Non-final classes should be such for a
good reason. Extensibility of classes should be enabled if it is
required not simply for the sake of being extensible.

 

Package scope is really used so there are no naming conflicts for an
application, especially when reusing classes from another framework.
Packages are by default open, not sealed, which means a rogue class can
be added to your package. If such a rogue class was added to a package,
the scope of protected fields would not yield any security. By default,
all fields and methods not declared public or private are protected, and
can only be accessed within the same package; don’t rely on this for
security.

 

Simply put, when translated into bytecode, inner classes are "rebuilt"
as external classes in the same package. This means any class in the
package can access this inner class. The owner/enclosing/father classes’
private fields are morphed into protected fields as they are accessible
by the now external inner class.

 

Don't hard code any passwords, user IDs, etc in your code. Silly and bad
design. Can be decompiled. Place them in a protected directory in the
deployment tree.

 

Override the clone method to make classes unclonable unless required.
Cloning allows an attacker to instantiate a class without running any of
the class constructors.

 

Serialization can be used to save objects when the JVM is "switched
off". Serialization flattens the object and saves it as a stream of
bytes. Serialization can allow an attacker to view the inner state of an
object and even see the status of the private attributes. writeObject()
is the method which kicks-off the serialization procedure. By overriding
this method to throw an exception and making it final, the object cannot
be serialized. When Serialization of objects occurs, transient data gets
dropped, so "tagging" sensitive information as transient protects
against serialization attacks. Deserialization can be used to construct
an object from a stream of bytes, which may mimic a legitimate class.
This could be used by an attacker to instantiate an object’s state. As
with object serialization, deserialization can be prevented by
overriding its corresponding method call readObject().

 

 

 

 

 

 

 

 

Injection Attack

Wednesday, February 03, 2016

10:34

 

> **Injection flaws** occur when an application sends untrusted data to
> an interpreter. Injection flaws are very prevalent, particularly in
> legacy code. They are often found in SQL, LDAP, Xpath, or NoSQL
> queries; OS commands; XML parsers, SMTP Headers, program arguments,
> etc. Injection flaws are easy to discover when examining code, but
> frequently hard to discover via testing. Scanners and fuzzers can help
> attackers find injection flaws.
>
>  
>
> Primary Defenses:

-   **Option \#1: Use of Prepared Statements (Parameterized Queries)**

-   **Option \#2: Use of Stored Procedures**

-   **Option \#3: Escaping all User Supplied Input**

> Additional Defenses:

-   **Also Enforce: Least Privilege**

-   **Also Perform: White List Input Validation**

>  
>
> The use of prepared statements with variable binding (aka
> parameterized queries) is how all developers should first be taught
> how to write database queries. They are simple to write, and easier to
> understand than dynamic queries. Parameterized queries force the
> developer to first define all the SQL code, and then pass in each
> parameter to the query later. This coding style allows the database to
> distinguish between code and data, regardless of what user input is
> supplied.
>
> Prepared statements ensure that an attacker is not able to change the
> intent of a query, even if SQL commands are inserted by an attacker.
> In the safe example below, if an attacker were to enter the userID of
> tom' or '1'='1, the parameterized query would not be vulnerable and
> would instead look for a username which literally matched the entire
> string tom' or '1'='1.
>
>  
>
> Stored procedures have the same effect as the use of prepared
> statements when implemented safely\* which is the norm for most stored
> procedure languages. They require the developer to just build SQL
> statements with parameters which are automatically parameterized
> unless the developer does something largely out of the norm. The
> difference between prepared statements and stored procedures is that
> the SQL code for a stored procedure is defined and stored in the
> database itself, and then called from the application. Both of these
> techniques have the same effectiveness in preventing SQL injection so
> your organization should choose which approach makes the most sense
> for you.
>
>  
>
> This second technique is to escape user input before putting it in a
> query. However, this methodology is frail compared to using
> parameterized queries and we cannot guarantee it will prevent all SQL
> Injection in all situations. This technique should only be used, with
> caution, to retrofit legacy code in a cost effective way. Applications
> built from scratch, or applications requiring low risk tolerance
> should be built or re-written using parameterized queries.
>
> This technique works like this. Each DBMS supports one or more
> character escaping schemes specific to certain kinds of queries. If
> you then escape all user supplied input using the proper escaping
> scheme for the database you are using, the DBMS will not confuse that
> input with SQL code written by the developer, thus avoiding any
> possible SQL injection vulnerabilities.
>
>  
>
> To minimize the potential damage of a successful SQL injection attack,
> you should minimize the privileges assigned to every database account
> in your environment. Do not assign DBA or admin type access rights to
> your application accounts. We understand that this is easy, and
> everything just ‘works’ when you do it this way, but it is very
> dangerous. Start from the ground up to determine what access rights
> your application accounts require, rather than trying to figure out
> what access rights you need to take away. Make sure that accounts that
> only need read access are only granted read access to the tables they
> need access to. If an account only needs access to portions of a
> table, consider creating a view that limits access to that portion of
> the data and assigning the account access to the view instead, rather
> than the underlying table. Rarely, if ever, grant create or delete
> access to database accounts.
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

 

 

Authentication and Session

Wednesday, February 03, 2016

10:47

 

> Developers frequently build custom authentication and session
> management schemes, but building these correctly is hard. As a result,
> these custom schemes frequently have flaws in areas such as logout,
> password management, timeouts, remember me, secret question, account
> update, etc. Finding such flaws can sometimes be difficult, as each
> implementation is unique
>
>  

1.  User authentication credentials aren’t protected when stored using
    > hashing or encryption.

2.  Credentials can be guessed or overwritten through weak account
    > management functions (e.g., account creation, change password,
    > recover password, weak session IDs).

3.  Session IDs are exposed in the URL (e.g., URL rewriting).

4.  Session IDs are vulnerable to [session
    > fixation](https://www.owasp.org/index.php/Session_fixation) attacks.

5.  Session IDs don’t timeout, or user sessions or authentication
    > tokens, particularly single sign-on (SSO) tokens, aren’t properly
    > invalidated during logout.

6.  Session IDs aren’t rotated after successful login.

7.  Passwords, session IDs, and other credentials are sent over
    > unencrypted connections

>  
>
>  
>
>

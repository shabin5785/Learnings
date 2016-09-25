Microservices

Monday, February 08, 2016

12:20

 

> <https://github.com/auth0/mfa-and-microservices-blog-samples/tree/master/microservices>
>
>  
>
> Everybody is talking about microservices. Industry veterans may
> remember monolithic or SOA-based solutions being *the way* of doing
> things. Times have changed. New tools have allowed developers to focus
> on specific problems without adding excessive complexity to deployment
> or other administrative tasks that are usually associated with
> isolated services. It has become increasingly easy to choose to work
> with the right tool for the right problem.
>
> In this **post series**, we will explore the world of microservices,
> how it can help solve real world problems, and why the industry is
> increasingly picking it as the standard way of doing things. In this
> series, we will attempt to tackle common problems related to this
> approach, and provide convenient and simple examples. By the end of
> the series, we should have a skeleton implementation of a full
> microservice-based architecture. Today, we will focus on what
> microservices are and how they compare to the alternatives. We will
> also list the problems we plan to discuss in the following posts.
>
> **Update:** in [part
> 2](https://auth0.com/blog/2015/09/13/an-introduction-to-microservices-part-2-API-gateway/) we
> talk about the *API gateway*.
>
>  
>
> **What is a microservice?**
>
> A microservice is an **isolated**, **loosely-coupled** unit of
> development that works on a **single concern**. This is similar to the
> old "Unix" way of doing things: do one thing, and do it well. Matters
> such as how to "combine" whatever is provided by the service are left
> to higher layers or to policy. This usually means that microservices
> tend to avoid interdependencies: if one microservice has a hard
> requirement for other microservices, then you should ask yourself if
> it makes sense to make them all part of the same unit.
>
> ![](media/image1.png){width="6.0in" height="1.625in"}
>
> What makes microservices particularly attractive to development teams
> is their **independence**. Teams can work on a problem or group of
> problems on their own. This creates several attractive qualities
> favored by many developers:

-   **Freedom to pick the right tool**: Is that new library or
    > development platform something you always wanted to use? You can
    > (if it's the right tool for the job).

-   **Quick iteration**: Was the first version suboptimal? No problem,
    > version 2 can be out the door in no time. Because microservices
    > tend to be small, changes can be implemented relatively quickly.

-   **Rewrites are a possibility**: In contrast with monolithic
    > solutions, since microservices are small, rewrites are
    > a possibility. Was the technology stack the wrong pick? No
    > problem, switch to the right alternative.

-   **Code quality and readability**: Isolated development units tend to
    > be of higher quality and new developers can get up to speed with
    > the existing code fairly easily.

> **Production-quality microservices**
>
> Now that we know what microservices are, here is a list of things we
> need to keep in mind when designing our microservice-based
> architecture. Don't worry if this seems too abstract; we will deal
> with all these concerns in a systematic way throughout this series of
> posts.

-   **Cross-cutting concerns** must be implemented in a way such that
    > microservices need not deal with details regarding problems
    > outside their specific scope. For instance, authentication can be
    > implemented as part of any API gateway or proxy.

-   **Data sharing** is hard. Microservices tend to favor per-service or
    > per-group databases that can be updated directly. When doing data
    > modeling for your application, notice whether this way of doing
    > things fits your application. For sharing data between databases,
    > it may be necessary to implement an internal process that handles
    > internal updates and transactions between databases. It is
    > possible to share a single database between many microservices;
    > just keep in mind that this may limit your options when and if you
    > need to scale in the future.

-   **Availability**: Microservices, by virtue of being isolated and
    > independent, need to be monitored to detect failures as early
    > as possible. In a big software stack, one service that goes down
    > may go unnoticed for some time. Account for this when picking your
    > software stack for managing services.

-   **Evolution**: Microservices tend to evolve fast. When dedicated
    > teams deal with specific concerns, new and better solutions are
    > found quickly. Therefore, it is necessary to account for
    > versioning of services. Old versions are usually available as long
    > as there are clients who need to consume data from them. Newer
    > versions are exposed in an application-specific way. For instance,
    > with an HTTP/REST API, the version of the microservice may be part
    > of a custom header, or be embedded in the returned data. Account
    > for this.

-   **Automated deployment**: The whole reason that microservices are so
    > convenient nowadays is that it is so easy to deploy a new service
    > from a completely clean environment. See Heroku, Amazon Web
    > Services,[Webtask.io](https://webtask.io/) or other
    > PaaS providers. If you are going for your own in-house approach,
    > keep in mind that the complexity of deploying new services or
    > versions of preexisting services is critical to the success of
    > your solution. If deployment is not handled in a convenient,
    > automated way, you risk eventually reaching a level of complexity
    > that outweighs the benefits originally brought about by
    > the approach.

-   **Interdependencies**: Keep them to a minimum. There are different
    > ways of dealing with dependencies between services. We will
    > explore them further later in this blog post series. For now, just
    > keep in mind that dependencies are one of the biggest problems
    > with this approach, so seek ways to keep them to a minimum.

-   **Transport and data format**: Microservices are fit for any
    > transport and data format; however, they are usually exposed
    > publicly through a RESTful API over HTTP. Any data format fit for
    > your information works. HTTP + JSON is very popular these days,
    > but there is nothing stopping you from using protocol-buffers over
    > AMQP, for instance.

> **Doing things right**
>
> All of these concerns can be dealt with in a systematic way. We will
> explore techniques and patterns in this post series to deal with them.
> Here is what we will be talking about in future posts:

-   **API proxying**

-   **Logging**

-   **Service discovery and registration**

-   **Service dependencies**

-   **Data sharing and synchronization**

-   **Graceful failure**

-   **Automated deployment and instantiation**

> **Keeping it real: a sample microservice**
>
> Now, this should be easy. If microservices take so much baggage off
> the development team's mind, writing one should be a piece of cake,
> right? Yes, in a way. While we could write a simple RESTful HTTP
> service and call that a microservice, in this post we will do it by
> taking into account some of the things we have listed above (don't
> worry: in the following posts, we will expand this example to include
> solutions for ALL the concerns listed above).
>
> For our example, we will pick the backend code from Sandrino Di
> Mattia's
> excellent [post](https://auth0.com/blog/2015/08/25/logging-and-debugging-in-react-with-flux-replaying-your-users-actions/) about
> using Flux for debugging. In Sandrino's post, a simple express.js app
> makes the backend for a React.js app. We will take that backend and
> adapt it. You can see the original backend
> code [here](https://github.com/auth0/react-flux-debug-actions-sample/blob/master/server.js).
>
> The backend in Sandrino's example handles many different concerns:
> login,
> authentication, [CORS](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing),
> update operations over tickets, and queries. For our microservice we
> will focus on one task: querying tickets. Check it out:
>
> var express = require('express');\
> var morgan = require('morgan');\
> var http = require('http');\
> var mongo = require('mongodb').MongoClient;\
> var winston = require('winston');
>
> // Logging\
> winston.emitErrs = true;\
> var logger = new winston.Logger({\
> transports: \[\
> new winston.transports.Console({\
> timestamp: true,\
> level: 'debug',\
> handleExceptions: true,\
> json: false,\
> colorize: true\
> })\
> \],\
> exitOnError: false\
> });
>
> logger.stream = {\
> write: function(message, encoding){\
> logger.debug(message.replace(/\\n\$/, ''));\
> }\
> };
>
> // Express and middlewares\
> var app = express();\
> app.use(\
> //Log requests\
> morgan(':method :url :status :response-time ms -
> :res\[content-length\]', {\
> stream: logger.stream\
> })\
> );
>
> var db;\
> if(process.env.MONGO\_URL) {\
> mongo.connect(process.env.MONGO\_URL, null, function(err, db\_) {\
> if(err) {\
> logger.error(err);\
> } else {\
> db = db\_;\
> }\
> });\
> }
>
> app.use(function(req, res, next) {\
> if(!db) {\
> //Database not connected\
> mongo.connect(process.env.MONGO\_URL, null, function(err, db\_) {\
> if(err) {\
> logger.error(err);\
> res.sendStatus(500);\
> } else {\
> db = db\_;\
> next();\
> }\
> });\
> } else {\
> next();\
> }\
> });
>
> // Actual query\
> app.get('/tickets', function(req, res, next) {\
> var collection = db.collection('tickets');\
> collection.find().toArray(function(err, result) {\
> if(err) {\
> logger.error(err);\
> res.sendStatus(500);\
> return;\
> }\
> res.json(result);\
> });\
> });
>
> // Standalone server setup\
> var port = process.env.PORT || 3001;\
> http.createServer(app).listen(port, function (err) {\
> if (err) {\
> logger.error(err);\
> } else {\
> logger.info('Listening on [http://localhost:'](http://localhost:') +
> port);\
> }\
> });

-   **One thing and one thing only**: Our microservice's single concern
    > is querying for the full list of tickets. Nothing more.
    > Authentication, CORS and other concerns are to be handled by upper
    > layers in our architecture.

-   **Logging**: We have kept logging using the 'winston' library. For
    > now we will just log to the console, but in later versions we will
    > push logs in a predefined format to a centralized location
    > for analysis.

-   **No dependencies**: Our microservice has no dependencies on
    > other microservices.

-   **Easily scaled**: With no dependencies, a separate process, and
    > operating on a single concern our microservice can easily
    > be scaled.

-   **Small and readable**: Our microservice is small and readable. New
    > developers can modify or rewrite it in no time.

-   **Data sharing**: For now our microservice reads data from its
    > own database. We will explore in future posts what happens when
    > other microservices need to update or create tickets.

-   **Registration and failure**: Our microservice stands on its own. In
    > future posts we will explore how to manage service discovery and
    > what you can do in case microservices fail.

> Get
> the [code](https://github.com/sebadoom/auth0/tree/master/microservices/microservice-1).
>
> **Aside: Interested in microservices? You will love webtasks!**
>
> Microservices are an important part of our stack at Auth0, and we have
> come up with a great way of making it even easier to use them. Check
> out[webtask.io](https://webtask.io/).

-   **Lightweight** and **simple** development workflow.

-   Streamlined **deployment**.

-   Powerful **security model** convenient for both HTML5 and
    > mobile apps.

-   **Web-friendly** programming model suitable for both HTML and
    > data APIs.

> We have converted the example above to a webtask, see how easy it is:
>
> npm install wt-cli -g
>
> \# This will send an activation link to your email. One time only.\
> wt init your.name@email.com
>
> \# This will return a new endpoint for your webtask\
> wt create
> <https://raw.githubusercontent.com/sebadoom/auth0/master/microservices/microservice-1-webtask/server.js>
>
> \# Use the endpoint here (we have setup a sample DB for this example)\
> curl
> [https://webtask.it.auth0.com/api/run/wt-sebastian\_peyrott-auth0\_com-0/0214e081084da52e5dd32915232242d8/tickets\\?webtask\_no\_cache\\=1\\&MONGO\_URL\\=mongodb://test:test@ds035553.mongolab.com:35553/microservices](https://webtask.it.auth0.com/api/run/wt-sebastian_peyrott-auth0_com-0/0214e081084da52e5dd32915232242d8/tickets/?webtask_no_cache\=1\&MONGO_URL\=mongodb://test:test@ds035553.mongolab.com:35553/microservices)
> -v
>
> See
> the [code](https://github.com/sebadoom/auth0/blob/master/microservices/microservice-1-webtask/server.js).
> Compare it with our previous version and see how little we changed.
>
> **What is an API gateway and why use it?**
>
> In all service-based architectures there are several concerns that are
> shared among all (or most) services. A microservice-based architecture
> is not an exception. As we said in the first post, microservices are
> developed almost in isolation. Cross-cutting concerns are dealt with
> by upper layers in the software stack. The API gateway is one of those
> layers. Here is a list of common concerns handled by API gateways:

-   Authentication

-   Transport security

-   Load-balancing

-   Request dispatching (including fault tolerance and
    > service discovery)

-   Dependency resolution

-   Transport transformations

> **Authentication**
>
> Most gateways perform some sort of authentication for **each
> request** (or series of requests). According to **rules** that are
> specific to each service, the gateway either routes the request to the
> requested microservice(s) or returns an error code (or less
> information). Most gateways add authentication information to the
> request when passing it to the microservice behind them. This allows
> microservices to implement **user specific logic** whenever required.
>
> **Security**
>
> Many gateways function as a single entry point for a public API. In
> such cases, the **gateways handle transport security** and then
> dispatch the requests either by using a different secure channel or by
> removing security constraints that are not necessary inside the
> internal network. For instance, for a RESTful HTTP API, a gateway may
> perform **"SSL termination"**: a secure SSL connection is established
> between the clients and the gateway, and proxied requests are then
> sent over non-SSL connections to internal services.
>
> **Load-balancing**
>
> Under high-load scenarios, gateways can **distribute requests among
> microservice-instances** according to custom logic. Each service may
> have specific scaling limitations. Gateways are designed to balance
> the load by taking these limitations into account. For instance, some
> services may scale by having multiple instances running under
> different internal endpoints. Gateways can dispatch requests to these
> endpoints (or even request the dynamic instantiation of more
> endpoints) to handle load.
>
> **Request-dispatching**
>
> Even under normal-load scenarios, gateways can provide custom logic
> for dispatching requests. In big architectures, **internal endpoints
> are added and removed** as teams work or new microservice instances
> are spawned (due to topology changes, for instance). Gateways may work
> in tandem with service registration/discovery processes or databases
> that describe how to dispatch each request. This provides
> exceptional **flexibility** to development teams.
> Additionally, **faulty services** can be routed to backup or generic
> services that allow the request to complete rather than fail
> completely.
>
> **Dependency resolution**
>
> As microservices deal with very specific concerns, some
> microservice-based architectures tend to become "chatty": to perform
> useful work, many requests need to be sent to many different services.
> For convenience and performance reasons, gateways may
> provide **facades** ("virtual" endpoints) that internally are **routed
> to many different microservices**.
>
> **Transport transformations**
>
> As we learnt in the first post of this series, microservices are
> usually developed in isolation and development teams have great
> flexibility in choosing the development platform. This may result in
> microservices that return data and use transports that are **not
> convenient for clients** on the other side of the gateway. The gateway
> must perform the necessary**transformations** so that clients can
> still communicate with the microservices behind it.
>
> **An API gateway example**
>
> Our example is a simple node.js gateway. It handles HTTP requests and
> forwards them to the appropriate internal endpoints (performing the
> necessary transformations in transit). It handles the following
> concerns:
>
> **Authentication**
>
> Authentication using **JWT**. A single endpoint handles initial
> authentication: /login. User details are stored in a Mongo database
> and access to endpoints is restricted by roles.
>
> /\*\
> \* Simple login: returns a JWT if login data is valid.\
> \*/\
> function doLogin(req, res) {\
> getData(req).then(function(data) {\
> try {\
> var loginData = JSON.parse(data);\
> User.findOne({ username: loginData.username }, function(err, user) {\
> if(err) {\
> logger.error(err);\
> send401(res);\
> return;\
> }
>
> if(user.password === loginData.password) {\
> var token = jwt.sign({\
> jti: uuid.v4(),\
> roles: user.roles\
> }, secretKey, {\
> subject: user.username,\
> issuer: issuerStr\
> });
>
> res.writeHeader(200, {\
> 'Content-Length': token.length,\
> 'Content-Type': "text/plain"\
> });\
> res.write(token);\
> res.end();\
> } else {\
> send401(res);\
> }\
> }, 'users');\
> } catch(err) {\
> logger.error(err);\
> send401(res);\
> }\
> }, function(err) {\
> logger.error(err);\
> send401(res);\
> });\
> }
>
> /\*\
> \* Authentication validation using JWT. Strategy: find existing user.\
> \*/\
> function validateAuth(data, callback) {\
> if(!data) {\
> callback(null);\
> return;\
> }
>
> data = data.split(" ");\
> if(data\[0\] !== "Bearer" || !data\[1\]) {\
> callback(null);\
> return;\
> }
>
> var token = data\[1\];\
> try {\
> var payload = jwt.verify(token, secretKey);\
> //Your custom validation logic goes here.\
> if(!payload.jti || revokedTokens\[payload.jti\]) {\
> logger.debug('Revoked token, access denied: ' + payload.jti);\
> callback(null);\
> } else {\
> callback({jwt: payload});\
> }\
> } catch(err) {\
> logger.error(err);\
> callback(null);\
> }\
> }
>
> *Disclaimer: the code shown in this post is not production ready. It
> is used just to show concepts. Don't copy paste it blindly :)*
>
> **Transport security**
>
> Transport security is handled through **TLS**: all public requests are
> received first by a reverse nginx proxy setup with sample
> certificates.
>
> **Load balancing**
>
> Load-balancing is handled by **nginx**. See the
> sample [config](https://github.com/sebadoom/auth0/blob/master/microservices/gateway/nginx.conf).
>
> **Dynamic dispatching, data aggregation and failures**
>
> Requests are **dynamically dispatched** according to a configuration
> stored in a database. Two types of requests are supported: HTTP and
> AMQP.
>
> Requests also support the **aggregation strategy** for splitting
> requests among several microservices: a single public endpoint may
> aggregate data from many different internal endpoints (microservices).
> All returned data is in JSON format. See this excellent [post by
> Netflix](http://techblog.netflix.com/2013/01/optimizing-netflix-api.html) on
> how this strategy helped them achieve better performance. Also check
> our [post on
> Falcor](https://auth0.com/blog/2015/08/28/getting-started-with-falcor/)which
> allows for easy data fetching from many sources.
>
> ![](media/image2.png){width="6.0in" height="5.322916666666667in"}
>
> **Failed internal requests** are handled by logging the error and
> returning less information than requested.
>
> /\*\
> \* Parses the request and dispatches multiple concurrent requests to
> each\
> \* internal endpoint. Results are aggregated and returned.\
> \*/\
> function serviceDispatch(req, res) {\
> var parsedUrl = url.parse(req.url);
>
> Service.findOne({ url: parsedUrl.pathname }, function(err, service) {\
> if(err) {\
> logger.error(err);\
> send500(res);\
> return;\
> }
>
> var authorized = roleCheck(req.context.authPayload.jwt, service);\
> if(!authorized) {\
> send401(res);\
> return;\
> }
>
> // Fanout all requests to all related endpoints.\
> // Results are aggregated (more complex strategies are possible).\
> var promises = \[\];\
> service.endpoints.forEach(function(endpoint) {\
> logger.debug(sprintf('Dispatching request from public endpoint ' +\
> '%s to internal endpoint %s (%s)',\
> req.url, endpoint.url, endpoint.type));
>
> switch(endpoint.type) {\
> case 'http-get':\
> case 'http-post':\
> promises.push(httpPromise(req, endpoint.url,\
> endpoint.type === 'http-get'));\
> break;\
> case 'amqp':\
> promises.push(amqpPromise(req, endpoint.url));\
> break;\
> default:\
> logger.error('Unknown endpoint type: ' + endpoint.type);\
> }\
> });
>
> //Aggregation strategy for multiple endpoints.\
> Q.allSettled(promises).then(function(results) {\
> var responseData = {};
>
> results.forEach(function(result) {\
> if(result.state === 'fulfilled') {\
> responseData = \_.extend(responseData, result.value);\
> } else {\
> logger.error(result.reason.message);\
> }\
> });
>
> res.setHeader('Content-Type', 'application/json');\
> res.end(JSON.stringify(responseData));\
> });\
> }, 'services');\
> }
>
> **Role checks**
>
> var User = userDb.model('User', new mongoose.Schema ({\
> username: String,\
> password: String,\
> roles: \[ String \]\
> }));
>
> var Service = servicesDb.model('Service', new mongoose.Schema ({\
> name: String,\
> url: String,\
> endpoints: \[ new mongoose.Schema({\
> type: String,\
> url: String\
> }) \],\
> authorizedRoles: \[ String \]\
> }));
>
> function roleCheck(jwt\_, service) {\
> var intersection = \_.intersection(jwt\_.roles,
> service.authorizedRoles);\
> return intersection.length === service.authorizedRoles.length;\
> }
>
> **Transport and data transformations**
>
> **Transport transformations** are performed to convert between HTTP
> and AMQP requests.
>
> **Logging**
>
> **Logging** is centralized: all logs are published to the console and
> to an internal message-bus. Other services listening on the
> message-bus can take action according to these logs.
>
> Get the
> full [code](https://github.com/sebadoom/auth0/tree/master/microservices/gateway).
>
> **Aside: How webtask and Auth0 implement these patterns?**
>
> We told you about [webtasks](https://webtask.io/) in our first post in
> the series. As webtasks *are*microservices they too run behind a
> gateway. The webtasks gateway handles authentication,
> dynamic-dispatching and centralized logging so that you don't have
> too.

-   For authentication, [Auth0](https://auth0.com/) is the issuer of
    > tokens and webtask will verify those tokens. There is a trust
    > relationship between them so that tokens can be verified.

-   For real time logging webtask implemented a stateless
    > resilient [ZeroMQ
    > architecture](http://tomasz.janczuk.org/2015/09/from-kafka-to-zeromq-for-log-aggregation.html) which
    > works across the cluster.

-   For dynamic-dispatching, there is a custom-built Node.js proxy which
    > uses [CoreOS etcd](https://github.com/coreos/etcd) as a pub-sub
    > mechanism to route webtasks accordingly.

> ![](media/image3.png){width="6.0in" height="2.0208333333333335in"}
>
>  
>
> **The service registry**
>
> The service registry is a database populated with information on how
> to dispatch requests to microservice instances. Interactions between
> the registry and other components can be divided into two groups, each
> with two subgroups:

-   Interactions between microservices and the registry (registration)

    1.  Self-registration

    2.  Third-party registration

<!-- -->

-   Interactions between clients and the registry (discovery)

    1.  Client-side discovery

    2.  Server-side discovery

> **Registration**
>
> Most microservice-based architectures are in constant evolution.
> Services go up and down as development teams split, improve, deprecate
> and do their work. Whenever a service endpoint changes, the **registry
> needs to know about the change**. This is what *registration* is all
> about: who publishes or updates the information on how to reach each
> service.
>
> **Self-registration** forces microservices to interact with the
> registry by themselves. **When a service goes up, it notifies the
> registry**. The same thing happens when the service goes down.
> Whatever additional data is required by the registry must be provided
> by the **service itself**. If you have been following this series, you
> know that microservices are all about dealing with a *single concern*,
> so self-registration might seem like an anti-pattern. However, for
> simple architectures, self-registration might be the right choice.
>
> ![](media/image4.png){width="6.0in" height="3.1145833333333335in"}
>
> **Third-party registration** is normally used in the industry. In this
> case, there is a **process or service that manages all other
> services**. This process polls or checks in some way which
> microservice instances are running and it automatically **updates the
> service registry**. Additional data might be provided in the form of
> per-service config files (or policy), which the registration process
> uses to update the database. Third-party registration is commonplace
> in architectures that use tools such as [Apache
> ZooKeeper](http://zookeeper.apache.org/) or [Netflix
> Eureka](https://github.com/Netflix/eureka) and other service managers.
>
> ![](media/image5.png){width="6.0in" height="2.2604166666666665in"}
>
> Third-party registration also provides other benefits. For instance,
> what happens when a service goes down? A third-party registration
> service might be configured to provide safe fallbacks for services
> that fail. Other policies might be implemented for other cases. For
> instance, the service registry process might be notified of a
> high-load condition and automatically add a new endpoint by requesting
> the instantiation of a new microservice-process or VM. As you can
> imagine, these possibilities are critical for big architectures.
>
> **Discovery**
>
> As you can imagine, discovery is the counterpart to registration from
> the point of view of clients. When a client wants to access a service,
> it must find out **where the service is located** (and other relevant
> information to perform the request).
>
> **Client-side discovery** forces clients to **query a discovery
> service** before performing the actual requests. As happens
> with *self-registration*, this requires clients to deal with
> additional concerns other than their main objective. The discovery
> service may or may not be located behind the API gateway. If it is not
> located behind the gateway, balancing, authentication and other
> cross-cutting concerns may need to be re-implemented for the discovery
> service. Additionally, each client needs to know the fixed endpoint
> (or endpoints) to contact the discovery service. These are all
> disadvantages. The one big advantage is not having to code the
> necessary logic in the gateway system. Study this carefully when
> picking your discovery method.
>
> ![](media/image6.png){width="6.0in" height="3.9583333333333335in"}
>
> **Server-side discovery** makes the **API gateway handle the
> discovery** of the right endpoint (or endpoints) for a request. This
> is normally used in bigger architectures. As all requests are directly
> sent to the gateway, all the benefits discussed in relation to it
> apply (see [part
> 2](https://auth0.com/blog/2015/09/13/an-introduction-to-microservices-part-2-API-gateway/)).
> The gateway may also implement discovery caching, so that many
> requests may have lower latencies. The logic behind cache invalidation
> is specific to an implementation.
>
> ![](media/image7.png){width="6.0in" height="2.7916666666666665in"}
>
> **Example: A registry service**
>
> In [part
> 2](https://auth0.com/blog/2015/09/13/an-introduction-to-microservices-part-2-API-gateway/) we
> worked on a simple API gateway implementation. In that example we
> implemented dynamic dispatching of requests through queries to a
> service database. In other words, we implemented **server-side
> discovery**. For this example, we will extend our microservice
> architecture by working on the **registration** aspect. We will do so
> in two ways:

-   By providing a simple registration library that any development team
    > can integrate into their microservice to
    > perform **self-registration**.

-   By providing a sample [systemd
    > unit](http://www.freedesktop.org/software/systemd/man/systemd.unit.html) that
    > registers a service during startup or shutdown (**third-party
    > registration** using systemd as a service manager).

> *Why systemd? It has become the de-facto service manager in most Linux
> installations. There are other alternatives for managing your services
> but all require installation and configuration. For simplicity, we
> picked the one that comes preinstalled in most distros, and that is
> systemd.*
>
> **A registration library**
>
> Our microservice example from previous posts was developed
> for *node.js*, so our library will be for it as well. Here is the main
> logic of our library:
>
> module.exports.register = function(service, callback) {\
> if(!validateService(service)) {\
> callback(new Error("Invalid service"));\
> }
>
> findExisting(service.name, function(err, found) {\
> if(found) {\
> callback(new Error("Existing service"));\
> return;\
> }
>
> var dbService = new Service({\
> name: service.name,\
> url: service.url,\
> endpoints: service.endpoints,\
> authorizedRoles: service.authorizedRoles\
> });
>
> dbService.save(function(err) {\
> callback(err);\
> });\
> });\
> }
>
> module.exports.unregister = function(name, callback) {\
> findExisting(name, function(err, found) {\
> if(!found) {\
> callback(new Error("Service not found"));\
> return;\
> }
>
> found.remove(function(err) {\
> callback(err);\
> });\
> });\
> }
>
> Microservices that perform self-registration need to call these
> functions during startup or shutdown (including abnormal shutdowns).
> We have integrated this library into our existing microservice example
> in the following way (set the SELF\_REGISTRY variable to any value to
> enable this function). Startup code:
>
> // Standalone server setup\
> var port = process.env.PORT || 3001;\
> http.createServer(app).listen(port, function (err) {\
> if (err) {\
> logger.error(err);\
> } else {\
> logger.info('Listening on [http://localhost:'](http://localhost:') +
> port);
>
> if(process.env.SELF\_REGISTRY) {\
> registry.register({\
> name: serviceName,\
> url: '/tickets',\
> endpoints: \[ {\
> type: 'http',\
> url: '<http://127.0.0.1:>' + port + '/tickets'\
> } \],\
> authorizedRoles: \['tickets-query'\]\
> }, function(err) {\
> if(err) {\
> logger.error(err);\
> process.exit();\
> }\
> });\
> }\
> }\
> });
>
> And shutdown code:
>
> function exitHandler() {\
> if(process.env.SELF\_REGISTRY) {\
> registry.unregister(serviceName, function(err) {\
> if(err) {\
> logger.error(err);\
> }\
> process.exit();\
> });\
> } else {\
> process.exit();\
> }\
> }
>
> process.on('exit', exitHandler);\
> process.on('SIGINT', exitHandler);\
> process.on('SIGTERM', exitHandler);\
> process.on('uncaughtException', exitHandler);
>
> **Third-party registration using systemd**
>
> Our gateway example reads service information from a Mongo database.
> Mongo provides a command-line interface that we can use to register
> services during startup or shutdown. Here is a sample systemd unit
> (remember to disable the SELF\_REGISTRY environment variable if you
> are using the sample microservice from this post):
>
> \[Unit\]\
> Description=Sample tickets query microservice
>
> \#Uncomment the following line when not running systemd in user mode\
> \#After=network.target
>
> \[Service\]\
> \#Uncomment the following line to run the service as a specific user\
> \#User=seba
>
> Environment="MONGO\_URL=mongodb://127.0.0.1:27018/test"
>
> ExecStart=/usr/bin/node
> /home/seba/Projects/Ingadv/Auth0/blog-code/microservices/server.js\
> ExecStartPost=/usr/bin/mongo --eval 'db.services.insert({"name":
> "Tickets Query Service", "url": "/tickets", "endpoints": \[{"type":
> "http", "url": "<http://127.0.0.1:3001/tickets>"}\],
> "authorizedRoles": \["tickets-query"\] });' 127.0.0.1:27017/test\
> ExecStopPost=/usr/bin/mongo --eval 'db.services.remove({"name":
> "Tickets Query Service"});' 127.0.0.1:27017/test
>
> \[Install\]\
> WantedBy=default.target
>
> Registration is handled by
> the *ExecStartPost* and *ExecStopPost* directives by calling the
> command-line Mongo client (included in all standard MongoDB
> installations).
>
> Get the [code](https://github.com/auth0/blog-microservices-part3).
>
> **Aside: use Auth0 for your microservices**
>
> Auth0 and microservices go hand-in-hand thanks to the magic
> of [JWT](http://jwt.io/). Check it out:
>
> var express = require('express');\
> var app = express();\
> var jwt = require('express-jwt');
>
> var jwtCheck = jwt({\
> secret: new Buffer('your-auth0-client-secret', 'base64'),\
> audience: 'your-auth0-client-id'\
> });
>
> app.use('/api/path-you-want-to-protect', jwtCheck);
>
> // (...)
>
> Your *client id* and *client secret* are available through the Auth0
> dashboard. Create a new account and [start
> hacking](https://auth0.com/docs)!
>
> **The problem of dependencies**
>
> As we have discussed in [previous
> posts](https://auth0.com/blog/2015/09/04/an-introduction-to-microservices-part-1/),
> one of the biggest enemies of distributed architectures are
> dependencies. In a microservice-based architecture, services are
> modeled as isolated units that manage a reduced set of problems.
> However, fully functional systems rely on the **cooperation and
> integration** of its parts, and microservice architectures are not an
> exception.
>
> In a traditional monolithic application, dependencies usually appear
> as method calls. It is usually a matter of *importing* the right parts
> of the project to access their functionality. In esence, doing so
> creates a **dependency**between the different parts of the
> application. With microservices, each microservice is meant to operate
> on its own. However, sometimes one may find that to provide certain
> functionality, **access to some other part** of the system is
> necessary. In concrete, some part of the system needs access to data
> managed by other part of the system.
>
> This is what is commonly known as **data sharing**: two separate parts
> of a system *share* the same data. If you are familiar with
> multithreaded programming you have a taste of **how hard data sharing
> can get**. However, in contrast to multithreaded applications, data
> sharing in a distributed architecture has its own sets of problems:

-   Can we share a single database? Does this scale as we add services?

-   Can we handle big volumes of data?

-   Can we provide consistency guarantees while reducing data-access
    > contention using simple locks?

-   What happens when a service developed by a team requires a change of
    > schema in a database shared by other services?

> ![](media/image8.png){width="6.0in" height="2.875in"}
>
> We will now study how some of these questions are answered in
> practice.
>
> **Separating concerns**
>
> Before going back to our problem of shared data and calls between
> services we need to take a step back and ask ourselves the obvious
> question: if we have these problems, could it be that we made **a
> mistake while modeling our data** or APIs? Certainly. This is why we
> need to talk about what we mean by **separate concerns** in greater
> detail. This can be described with the help of two concepts:

-   **Loose coupling**: which means microservices should be able to be
    > modified *without* requiring changes in other microservices.

-   **Problem locality**: which means related problems should be grouped
    > together (in other words, if a change requires an update in
    > another part of the system, those parts should be close to
    > each other).

> In concrete, loose coupling means microservices should provide clear
> interfaces that **model the data and access patterns** related to the
> data sitting behind them, and they should stick to those interfaces
> (when changes are necessary, versioning, which we will discuss later,
> comes into play). Problem locality means concerns and microservices
> should be**grouped** according to their **problem domain**. If an
> important change is required in a microservice related to billing, it
> is much more likely other microservices in the same problem domain
> (billing) will require changes, rather than microservices related to,
> say, product information. In a sense, developing microservices means
> drawing **clear boundaries** between different problem domains, then
> splitting those problem domains into independent units of work that
> can be easily managed. It makes much more sense to share data inside a
> domain boundary if required than share data between unrelated domains.
>
> ![](media/image9.png){width="6.0in" height="2.5in"}
>
> **The case for merging services into one**
>
> One important question you should ask yourself when working with
> separate microservices inside a problem domain is: are these services
> talking too much with eachother? If so, consider the impact of making
> them a **single service**. Microservices should be small, but **no
> smaller than necessary** to be convenient. Bam! Data sharing and
> dependency problems are gone. Of course, the opposite applies: if you
> find your services getting bigger and bigger to reduce chattiness,
> then perhaps you should rethink how your data is modeled, or how your
> problem domains are split. Trying to **keep balance** is the key.
>
> ![](media/image10.png){width="6.0in" height="3.6875in"}
>
> By the way, remember improving your solutions through **iteration** is
> part of the benefits of the microservices approach. Do your best
> effort to get things right from the beginning, but know you can make
> changes if things don't work out.
>
> **Data sharing**
>
> Now that we understand that data sharing may not be the only answer,
> we will focus on what to do when it is. We will split shared data in
> two groups:**static data** and **mutable data**.
>
> **Static data**
>
> Static data is data that is usually read but **rarely (if ever)
> modified**. Sometimes it is necessary to study access patterns after
> the system goes live before finding out what data can be
> considered *static*. The nice thing about static data is that even if
> it is shared, no locks or consistency algorithms are necessary. All
> services can **read the data concurrently** and not care about any
> other readers. However you can choose different approaches to store
> this data according to your needs:

-   Keep it in a database: this may or may not be a good approach
    > according to the database you have picked. Two things to keep in
    > mind: 1) Is it sensible to have each service query this database
    > through the wire each time this data is required? 2) Can
    > transactional updates to the data be performed whenever this data
    > needs to be updated (even if it is once in a while)?

-   Embed it in the code or share it as a file: if the data is small
    > enough, it may make sense to embed it in the code or distribute it
    > as part of a file to be deployed with each service. Things to keep
    > in mind: 1) How easy is it to atomically restart all services
    > sharing this data? 2) Is it small enough to not cause performance
    > issues when loading each service?

-   Make it into a service: similar to the database approach with the
    > added benefit of being able to make arbitrarily complex decisions
    > about how the data is sent over the wire and who can access it.

> **Mutable data**
>
> As we have mentioned before, the biggest problem with shared data
> is**what to do when it changes**. Suppose our microservice
> architecture is the heart of an online game distribution service. One
> of our microservices handles the game list of a customer. Other
> microservice handles the purchase of a game. When a customer purchases
> a game, that game is added to the list of games he or she owns. Our
> purchase microservice needs to tell our game-list microservice of the
> games that are added to a customer's list. How can we approach this
> problem? What follows is a list of common approaches to the problem.
> We will describe each and their advantages and disadvantages (note
> this is not an exhaustive list).

-   Shared database

-   Another microservice

-   Event/subscription model

-   Data pump model

> **SHARED DATABASE**
>
> ![](media/image11.png){width="6.0in" height="3.0625in"}
>
> We have noted some of the problems with the shared database approach
> before, so we will now focus on what we can do to avoid them. When
> dealing with shared data across databases (or tables within a
> database) there are essentially two
> approaches: **transactions** and **eventual consistency**.
>
> Transactions are mechanisms that allow database clients to make sure a
> series of **changes either happen or not**. In other words,
> transactions allow us to guarantee consistency. In the world
> of *distributed systems*, there are**distributed transactions**. There
> are different ways of implementing distributed transactions, but in
> general, there is a **transaction manager**that must be notified when
> a client wants to start a transaction. Only if the transaction manager
> (that usually communicates this intention to other clients) allows us
> to move forward the transaction can be performed. The downside to this
> approach is that **scaling is usually harder**. Transactions are
> useful in the context of **small or quick changes**.
>
> Eventual consistency deals with the problem of distributed data
> by**allowing inconsistencies for a time**. In other words, systems
> that rely on eventual consistency assume the data will be in an
> incosistent state at some point and handle the situation by postponing
> the operation, using the data as-is, or ignoring certain pieces of
> data. Eventual consistency systems are easier to reason about but not
> all data models or operations fit its semantics. Eventual consistency
> is useful in the context of **big volumes of data**.
>
> When facing the problem of a shared database, **try very hard to keep
> the data in a single place** (i.e. not to split it). If there is no
> other option but to split the data, study the options above in detail
> before committing to any.
>
> **ANOTHER MICROSERVICE**
>
> ![](media/image12.png){width="6.0in" height="7.53125in"}
>
> In this approach rather than allowing microservices to access the
> database directly, a new microservice is developed.
> This **microservice manages all access to the shared data** by the two
> services. By having a common entry point it is easier to reason about
> changes in various places. For small volumes of data, this can be a
> good option as long as the new microservice is the only one managing
> the data. Consider if this is something you can do and whether the
> microservice can scale to your future requirements.
>
> **EVENT/SUBSCRIPTION MODEL**
>
> ![](media/image13.png){width="6.0in" height="5.302083333333333in"}
>
> In this approach, rather than relying on each service fetching the
> data, services that make changes to data or that generate data **allow
> other services to subscribe to events**. When these events take place,
> subscribed services receive the notification and make use of the
> information contained in the event. This means that at no point any
> microservice is reading data that can be modified by other
> microservices. The simplicity of this approach makes it a powerful
> solution to many use cases, however there are downsides: a good set of
> events must be integrated into the generating microservice and lost
> events are a possibility. You should also consider the case of big
> volumes of data: the data gets sent to as many subscribers as
> registered.
>
> **DATA PUMP MODEL**
>
> ![](media/image14.png){width="6.0in" height="2.1979166666666665in"}
>
> This is related to the eventual consistency case and the additional
> microservice case: a microservice handles changes in one part of the
> system (either by reading from a database, handling events or polling
> a service) and updates another part of the system with those changes
> atomically. In esence, data is **pumped** from one part of the system
> to the other. A thing to keep in mind: consider the implications of
> duplicating data across microservices. Remember that duplicated data
> means changes in one copy of the data create inconsistencies unless
> updates are performed to each copy. This is useful for cases where big
> volumes of data need to be analyzed by slow processes (consider the
> case of data analytics, you need recent copies of the data, but not
> necessarily the latests changes). For long running pumps, remember
> that consistency requirements are still important. One way to do this
> is to read the data from a read-only copy of the database (such as a
> backup).
>
> **Versioning and failures**
>
> An important part of managing dependencies has to do with what happens
> when a **service is updated** to fit new requirements or solve a
> design issue. Other microservices may depend on the **semantics of the
> old version** or worse: **depend on the way data is modeled** in the
> database. As microservices are developed in isolation, this means **a
> team usually cannot wait** for another team to make the necessary
> changes to a dependent service before going live. The way to solve
> this is through**versioning**. All microservices should make it clear
> what version of a different microservice they require and what version
> they are. A good way of versioning is through **semantic versioning**,
> that is, keeping versions as a set of numbers that make it clear when
> a breaking change happens (for instance, one number can mean that the
> API has been modified).
>
> ![](media/image15.png){width="6.0in" height="4.25in"}
>
> The problem of dependency and changes (versions) rises an interesting
> question: **what if things break when a dependency is modified** (in
> spite of our efforts to use versioning)? Failure. We have discussed
> this briefly in previous posts in this series and now is good time to
> remember it: **graceful failure** is *key* in a distributed
> architecture. **Things will fail**. Services should do whatever is
> possible to run even when dependencies fail. It is perfectly
> acceptable to have a fallback service, a local cache or even to return
> less data than requested. Crashes should be avoided, and all
> dependencies should be treated as things prone to failure.
>
> ![](media/image16.png){width="6.0in" height="3.6770833333333335in"}
>
> **Example: events and shared data between microservices with random
> failures**
>
> For our example we will create a small group of versioned
> microservices with fallback capabilities. As this example models the
> behavior of dependant microservices inside a corporate network, we
> will not make use of the public API gateway we developed for previous
> posts. However, the logic behind dynamic dispatching of services will
> be reused in this case to provide fallback capabilities. In other
> words, we have refactored the logic behind the dynamic dispatching of
> services from the API gateway into a library. We now use this library
> to provide dynamic dispatching and fallback capabilities inside our
> network.
>
> ![](media/image17.png){width="6.0in" height="4.083333333333333in"}
>
> There are 2 services: a tickets service and a "reply feed" service.
> The tickets service allows adding, querying and subscribing to
> updates. The reply feed subscribes to the tickets service to receive
> new replies without querying the tickets service. Additionally the
> tickets service is split in two versions: 1.0.0 and 1.0.1. Version
> 1.0.1 is identical to 1.0.0 but causes random failures when querying
> tickets. When a failure is detected the system automatically falls
> back to the next compatible version available.
>
> //Recursive, consider this in production. This won't be a problem\
> //once node.js and V8 support tail-call optimizations.\
> function callNext(i) {\
> if(i === services.length) {\
> callback(new Error("No service available"));\
> return;\
> }
>
> logger.debug('Calling ' + services\[i\].name + ' version: ' +\
> services\[i\].versionMajor + '.' +\
> services\[i\].versionMinor + '.' +\
> services\[i\].versionPatch);
>
> dispatch.serviceDispatch(services\[i\], data,\
> function(err, response) {\
> if(err) {\
> logger.info("Failed call to: " + services\[i\]);\
> logger.error(err);
>
> callNext(i + 1);\
> } else {\
> logger.info("Succeeded call to: " + services\[i\]);
>
> callback(null, response);\
> }\
> }\
> );\
> }
>
> callNext(0);
>
> Data sharing is presented in the form of the shared database between
> the different versions of the tickets service. Consistency is achieved
> through transactional guarantees provided by Mongo. Mongo guarantees
> that all modifications performed to a single document either happen or
> they don't. No client sees intermediate results.
>
> On the other hand, data sharing between the replies service and the
> tickets service is achieved through the event/subscription model. As
> the reply feed only needs to store the latest 10 replies (this is a
> design requirement) a simple event for each new message can work as a
> solution, without requiring shared access to the tickets database.
>
> **REPLIESFEED.JS**
>
> function subscribe() {\
> var data = JSON.stringify({\
> url: eventUrl\
> });
>
> registry.call('Ticket Subscribe', 1, 0, 1, data, function(err,
> response) {\
> if(err) {\
> logger.error(err);\
> }\
> });\
> }
>
> app.post('/replyEvent', function(req, res) {\
> //TODO: validate req.body data
>
> logger.debug(req.body);
>
> latestReplies.push(req.body);\
> if(latestReplies.length &gt; 10) {\
> latestReplies.splice(0, latestReplies.length - 10);\
> }
>
> res.sendStatus(200);\
> });
>
> **TICKETS.JS AND TICKETS-RANDOM-FAIL.JS**
>
> function notifySubscribers(data) {\
> var collection = db.collection('tickets');\
> var oid = new ObjectID(data.ticketId);\
> collection.findOne({ '\_id': oid }, { title: 1 }, function(err,
> ticket) {\
> if(err) {\
> logger.error(err);\
> return;\
> }
>
> data.title = ticket.title;\
> var jsonData = JSON.stringify(data);
>
> logger.debug(data);
>
> for(var subscriber in commentSubscribers) {\
> if(commentSubscribers.hasOwnProperty(subscriber)) {\
> console.log('EVENT: sending new reply to subscriber: ' +\
> subscriber);\
> dest = url.parse(subscriber);
>
> var req = http.request({\
> hostname: dest.hostname,\
> port: dest.port,\
> path: dest.path,\
> method: 'POST',\
> headers: {\
> 'Content-Type': 'application/json',\
> 'Content-Length': jsonData.length\
> }\
> });
>
> req.on('error', function(err) {\
> logger.error(err);\
> });
>
> req.write(jsonData);\
> req.end();\
> }\
> }\
> });\
> }
>
> The example is completed by a simple process that accesses these
> services and logs everything to console. The logs show when a service
> falls back to a different version and when an event is sent. Get
> the [full code](https://github.com/auth0/blog-microservices-part4). To
> run it deploy an empty Mongo database to the db directory and insert
> the tickets from tickets.json into the tickets collection. Then
> run test.js and watch the logs.
>
> *Please note all of the code in this example is just that: an example.
> Do not consider this production ready. Run your own tests :)*
>
> **Aside: webtasks are microservices**
>
> As we have shown in previous posts, webtasks *are* microservices. Our
> architecture relies heavily on webtasks and it is easy to turn one of
> the above microservices into a webtask. Check it out and [create your
> own webtasks](https://webtask.io/). Try to turn one of the examples
> into a webtask and then push it with wt. Remember webtasks do not
> support require commands to files in the same directory, so you will
> need to embed the code in a single .jsfile. Database connections must
> be performed against a publicly accessible server.
>
> wt create repliesFeedAsWebtask.js\
> \# Wait a bit and then run\
> wt logs
>
> **Conclusion**
>
> Dependencies are **hard**, moreso in a distributed architecture. Data
> sharing and interservice calls **should be kept to a minimum** if
> possible. If you cannot avoid them, consider the implications of
> turning **multiple services into one**. If that is not the right
> choice, study what kind of data you are sharing (static or mutable)
> and what are the proper ways of sharing it according to your **current
> and future use cases** (volume of data, scaling considerations,
> algorithmic and implementation complexity, consistency requirements,
> etc.). Remember that you can and you should make modifications to your
> architecture as you find better ways of doing things.**Microservices
> favor iteration**, use it to your advantage and avoid integration
> patterns that prevent future modifications.
>
>  
>
> From
> &lt;<https://auth0.com/blog/2015/11/07/introduction-to-microservices-part-4-dependencies/>&gt;
>
>  
>
>  
>
> **Microservice architectures: lessons learnt from the early adopters**
>
> March 19th, 2015 | By Guido de Caso
>
> Two platitudes reign supreme in tech: “Change is the only constant”
> and “Hindsight is 20/20.” As our industry has evolved over the last
> few decades, things have moved from imperative to object oriented and
> into functional programming; from waterfall to agile processes; from
> centralized to distributed versioning control mechanisms; and from
> desktop GUIs to web and into mobile apps. Even the way we develop,
> push, build, test, deploy and monitor our precious code continues to
> evolve with a strong focus on cloud-based solutions and continuous
> delivery. As these new technologies have emerged, what’s interesting
> is how obvious they seem by the time they reach wide adoption — but
> only in retrospect. Until that point, there’s often uncertainty,
> speculation, and debate.
>
> This uncertainty is what separates the early and late adopters — well,
> and those who adopt the *wrong* technologies (sorry, Betamaxers).
> Early adopters of new technologies will exploit their cutting-edge
> benefits much sooner — but at the cost of a lot of resources spent in
> perfecting them. On the other hand, late adopters can swiftly avoid
> the pitfalls thanks to those who have already paved the way for them —
> though they risk falling behind the competition in the meantime.
>
> If you are a Google-sized player, you can easily absorb the costs of
> being an early adopter and enjoy its benefits. For smaller companies,
> these costs may be prohibitive or the risks involved simply too high
> to cope with.
>
> So, if you’re a smaller company, how can you gain the benefits of
> being an early adopter while avoiding most of the risks? Well, at
> Medallia, we decided we needed to be a smart early adopter. What does
> being a smart early adopter mean? It means almost looking ahead into
> the future (gathering data) to figure out which tech solution will be
> obvious in the years ahead. And this is highlighted by our ongoing
> adoption of **microservice architectures.**
>
> What are microservice architectures? They’re the successor of
> service-oriented architectures (SOAs), which have been slowly gaining
> traction over the last few years. Many of us may think of big
> enterprisey push from software giants such as IBM’s WebSphere, myriads
> of XML and WS-\* protocols when we hear about SOAs. However,
> Microservice architectures are a more recent generation of SOAs with
> grassroots origins. These architectures embrace principles like
> clearly defined APIs, unified service discovery and continuous
> deployment mechanisms. None of these principles are particularly new,
> but microservice architectures combine them in such a natural and
> symbiotic way that these ideas recently gained new relevance.
>
> The Medallia Engineering Team saw a big opportunity in this emerging
> technology, but in order to be agile early adopters with less risk, we
> spoke with engineering leaders inside of some of the world’s biggest
> and most successful companies to better understand microservice
> architectures, and here’s what we found:
>
> **Synchronous Inter-service Communication**
>
> One aspect that we covered during our conversations was synchronous
> inter-service communication. We discussed about HTTP/JSON versus
> binary-based solutions (such as Thrift or Protocol Buffers). While
> pretty much everyone is using HTTP for public APIs, there is a big
> diversity in terms of how internal communication is handled. Using
> Thrift/Protobuf internally has the advantage of rock-solid schema
> enforcing and backwards/forwards compatibility as well as better out
> of the box performance compared to HTTP. On the other hand, using HTTP
> both internally and externally has the advantage of uniformity with
> the implied benefits in developer agility.
>
> Regardless of the choice of technology, many must-have components need
> to be manually added on top of either HTTP or binary protocols.
> Libraries such as hystrix or finagle emerged to deal with client
> robustness, Servo and Zipkin for monitoring, and the list goes
> on.** **
>
> **External API **
>
> In an app-driven world, many of the microservices need to be somewhat
> available to the outside world. The simplest approach is to allow each
> external request (e.g., coming from an external-facing API) to go
> through directly to the service that it’s trying to reach. This
> implies that the logic for securing requests (e.g., authenticating the
> user or app key) must be replicated on every service.** **
>
> Most of the companies we engaged in conversation with agreed that this
> is probably not the best way to go about it, and they found it much
> more effective to establish a clear demarcation layer. External
> requests get properly authenticated and routed to the appropriate
> service. Once secured, the external request is converted into an
> internal request that gets treated pretty much as if it had been
> originated from another internal service. This demarcation layer acts
> as a reverse proxy and allows us to have the logic for securing
> external requests in a single place.
>
> **Composition Layer **
>
> A different problem is raised by the variety of request formats.
> External requests are most likely to be HTTP/JSON, which is the
> ubiquitous technology at that level. Internal requests, however, may
> be using a different technology such as Thrift. Will the demarcation
> layer be responsible for translating the HTTP/JSON request into a
> Thrift equivalent? Or will services need to understand both Thrift for
> internal requests and HTTP/JSON for external ones?
>
> While pondering these alternatives we realised that it is unlikely
> that external apps will consume services in the same way that internal
> services do. While the uniform external/internal API seemed to be the
> most elegant way to go, treating internal and external requests the
> same way is hardly ever the right choice. Internal requests may handle
> a lot of ids or data that is not ready to be consumed by an external
> party. For example, let’s say that we have an Account service and a
> Roles service. An account has a role, stored as an internal integer ID
> for such role. So account ‘yolanda’ may have role ’33’. When exposing
> this internally in an API it is perfectly fine to return ‘username:
> yolanda, role: 33′. However, if we were to expose this externally we
> may decide instead to replace role ’33’ for its role name by querying
> the Role service in order to yield ‘username: yolanda, role: manager’
> to an external app.
>
> Performing these service compositions on our side, as opposed to
> leaving it up to the client apps, has quite interesting advantages:

-   **Efficiency**. External request roundtrips are quite expensive so
    > if an app has to fetch ‘username: yolanda, role:33′ only to go and
    > make a second query to fetch the name of role ’33’ that’s twice as
    > many requests than performing the composition in our side, where
    > network calls are orders of magnitude faster than a
    > public network.

-   **Consistency**. If we leave the composition up to each app then we
    > are bound to have code duplication: each of the apps needs to
    > perform the composition themselves. Even slight variations in how
    > these apps handle the composition can yield inconsistencies in the
    > user experience. For example, while most apps will request the
    > name of role ’33’, maybe a few of them will instead ask for its
    > short-name so the result would be ‘mgr’ instead of ‘manager’.

-   **Security**. In many cases we don’t want to expose a full object
    > with all its complexity or internal fields to the outside world.
    > If we have the same API for internal and external requests there
    > is no way we can filter out the fields that we show on each case.
    > On the other hand, by performing compositions on our side we can
    > craft the objects that we return in such a way that their
    > visibility is limited to what we decide to show to the
    > external apps. For example, the Account service may also expose
    > the e-mail internally but we may strip that out at the composition
    > layer in order to protect our customers’ PII.

-   **Plurality**. The composition layer is the natural place to
    > translate a HTTP/JSON request into several requests performed
    > internally via Thrift (or other transports). This layer should be
    > absolutely stateless and there is a wide range of choices for
    > programming languages that can be used here, node.js being a
    > salient example.

> **Security**
>
> When it comes to how to secure inter-service communication it seems to
> be an area where lots remains to be improved. During our exploration
> phase we discovered that while most companies secure external requests
> via API keys and mechanisms such as OAuth2, internal communication
> security is very thin and only applied where strictly required for
> compliance. In our case, we envision having third-party services
> running in our infrastructure so we must think about security for
> internal requests from the get go. However, traditional mechanisms
> such as HTTPS with client and server side authentication via
> certificates have an awful overhead.
>
> **Service Discovery**
>
> Service discovery is an area where we found various technologies such
> as Eureka or ZooKeeper competing for adoptance. However, while there
> are differences as to how each of these technologies is to be used and
> maintained, the general concept of service discovery is pretty similar
> in either case. Clients need to contact services and a naming
> mechanism is used, optionally with either versioning or other elements
> such as tenant as parameters. A service can be running in many
> instances so load balancing comes into play. The most flexible
> approach that we found so far is to have the service discovery
> mechanism return a ‘service contacting policy’ that indicates the
> different URLs where the service can be found, their health status,
> their relative load-balancing weights and other elements such as
> overrides for steering specific user requests to specific instances
> (particularly useful for rolling out features to a small fixed set of
> users). The client needs to make sense of this policy and honor it,
> usually with the help of a client library, so that the policy honoring
> logic does not have to be re-implemented by each service.
>
> **Asynchronous Communication**
>
> For asynchronous communication we’ve learned of various approaches
> that range from using polling mechanisms all the way down to
> full-fledged async solutions based on Kafka. We believe that a good
> philosophy for async communication is to use it almost exclusively for
> notifications with minimal data. For instance, services notify other
> services when the data or resources they own changes. The Account
> service will notify other services if ‘yolanda’ changes her role.
> These notifications should only contain the primary key of the
> elements that have changed, so they can be really short and generally
> won’t carry sensitive information. If a service wants to learn more
> after having received an async invalidation message it can go and
> fetch more info about it via synchronous communication as described
> above. This allows us to focus on securing synchronous messages only
> and avoids duplicate effort in that regard.
>
> **Monitoring and Debugging**
>
> A few important areas where microservice architectures need careful
> consideration are monitoring and debugging. In a traditional
> standalone system monitoring is attached to a few vitals and KPIs,
> debugging is done after-the-fact and via inspecting the logs. On top
> of this, when dealing with hundreds of services, it is imperative to
> have uniform mechanisms to ensure monitoring is done in a consistent
> and pervasive manner.Also, logs need to be aggregated, ideally with
> the possibility to rapidly trace individual requests and understand
> their ‘communication tree’.
>
> Most of the challenges are around dealing the scale: multiplicity of
> services with tons of requests that bounce back and forth between
> them. Uniforming the instrumentation mechanisms as well as allowing
> the monitoring of the network itself (and not just what happens inside
> each service) are key ingredients in the solutions we’ve discussed.
>
> A key insight is to think of the log and its messages as a stream of
> real-time events, and not so much as just a text file that’s to be
> stored in disk.
>
> **Final thoughts**
>
> Finally, a common theme among companies adopting microservice
> architectures is that they acknowledged devoting a big chunk of their
> engineering efforts towards building and maintaining these core
> services such as service discovery or inter-service communication. For
> big companies this is manageable, but it remains to be seen how well
> it can be replicated in smaller, more product-driven companies.
>
> In short, microservice architectures are still far from being a
> turn-key solution. While success stories abound, there is a big price
> tag attached in terms of engineering effort and innumerable failed
> attempts. At Medallia, we’re at the early days of something bigger
> than ourselves. We are in this to learn from the early adopters — and
> in doing so, become a smarter early adopter ourselves.
>
>  
>
>  
>
> From
> &lt;<https://engineering.medallia.com/blog/microservice-architectures-lessons-learnt-from-the-early-adopters/?ref=slicedham>&gt;
>
>  
>
>  
>
>  

 

 

JWT

Monday, February 08, 2016

12:26

 

> JSON Web Tokens are used in the industry more and more. The spec which
> defines them ([RFC7519](https://tools.ietf.org/html/rfc7519))
> describes them as a compact, URL-safe means of representing claims
> between parties by encoding them as JSON objects which can be
> digitally signed or encrypted. There are several algorithms which take
> place in this process, we will explore some of the most common ones
> below. Read on!
>
>  
>
> **JSON Web Token**
>
> A JSON Web Token encodes a series of *claims* in a JSON object. Some
> of these claims have specific meaning, while others are left to be
> interpreted by the users. Common claims are:

-   Issuer (iss)

-   Subject (sub)

-   Audience (aud)

-   Expiration time (exp)

-   Not before (nbf)

-   Issued at (iat)

-   JWT ID (jti)

> Some of these claims are very common. The subject claim (sub) normally
> describes to whom or to which application the JWT is issued. The
> issued at claim (iat) can be used to store the time at which the JWT
> is created, thus allowing JWTs to be invalidated after a certain
> amount of time. Other custom claims can be added.
>
> A JWT is usually complemented with a signature or encryption. These
> are handled in their own specs as [JSON Web Signature
> (JWS)](https://tools.ietf.org/html/rfc7515) and [JSON Web Encryption
> (JWE)](https://tools.ietf.org/html/rfc7516).
>
> A signature allows a JWT to be *validated* against modifications.
> Encryption, on the other hand, makes sure the content of the JWT is
> only readable by certain parties.
>
> **JOSE header**
>
> Signed and encrypted JWTs carry a header known as the JOSE header
> (JSON Object Signing and Encryption). This header describes what
> algorithm (signing or encryption) is used to process the data
> contained in the JWT. The JOSE header typically defines two
> attributes: alg and typ.

-   alg: the algorithm used to sign or encrypt the JWT

-   typ: the content that is being signed or encrypted (usually 'JWT').

> **Compact Representation**
>
> JWS also defines a *compact* representation for a signed JWT:
>
> BASE64URL(UTF8(JWS Protected Header)) + '.' +\
> BASE64URL(JWS Payload) + '.' +\
> BASE64URL(JWS Signature)
>
> The compact representation is basically the concatenation of the JOSE
> header, the JWT and the details of the signature. Each component es
> BASE64 encoded and separated by a single dot ('.').
>
> This results in the typical JWT representation we find in the web:
>
> eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
>
> [jwt.io](http://jwt.io/) is an excellent playfield to test JWTs. Go
> to [http://jwt.io](http://jwt.io/) and input the string above in the
> encoded field.
>
> **Compact Representation for Encrypted JWTs**
>
> The compact representation for encrypted JWTs is somewhat different:
>
> BASE64URL(UTF8(JWE Protected Header)) + '.' +\
> BASE64URL(JWE Encrypted Key) + '.' +\
> BASE64URL(JWE Initialization Vector) + '.' +\
> BASE64URL(JWE Ciphertext) + '.' +\
> BASE64URL(JWE Authentication Tag)
>
> The ciphertext would normally contain a JWT.
>
> Signed and encrypted JWTs are usually *nested*. That means that a
> signed JWT is first produced and then an encrypted version of the
> signed result is then created. This provides two benefits:

-   The signature can't be stripped.

-   The signature is private (can't be seen by others).

> **Common JWT Signing Algorithms**
>
> Most JWTs in the wild are just signed. The most common algorithms are:

-   HMAC + SHA256

-   RSASSA-PKCS1-v1\_5 + SHA256

-   ECDSA + P-256 + SHA256

> *The specs defines many more algorithms for signing. You can find them
> all in [RFC 7518](https://tools.ietf.org/html/rfc7518#section-3).*
>
> **HMAC algorithms**
>
> This is probably the most common algorithm for signed JWTs.
>
> Hash-Based Message Authentication Codes (HMACs) are a group of
> algorithms that provide a way of signing messages by means of a shared
> key. In the case of HMACs, a cryptographic hash function is used (for
> instance SHA256). The strength (i.e. how hard it is to forge an HMAC)
> depends on the hashing algorithm being used.
>
> The main objective in the design of the algorithm was to allow the
> combination of a key with a message while providing strong guarantees
> against tampering. Ad-hoc solutions (for example, appending the key to
> the message and then hashing the result) suffer from mathematical
> flaws that allow potential attackers to forge the signature. The HMAC
> algorithm is designed against that.
>
> The algorithm per-se is quite simple (JavaScript pseudo-code with
> Node.js extensions):
>
> // Key: Buffer with key, Message: Buffer with message\
> function hmacSha256(key, message) {\
> // The algorithm requires the key to be of the same length as the\
> // "block-size" of the hashing algorithm (SHA256 = 64-byte blocks).\
> // Extension is performed by appending zeros.\
> var fullLengthKey = extendOrTruncateKey(key);
>
> var outterKeyPad = 0x5c; // A constant defined by the spec.\
> var innerKeyPad = 0x36; // Another constant defined by the spec.
>
> var outterKey = new Buffer(fullLengthKey.length);\
> var innerKey = new Buffer(fullLengthKey.length);\
> for(var i = 0; i &lt; fullLengthKey.length; ++i) {\
> outterKey\[i\] = outterKeyPad \^ fullLengthKey\[i\];\
> innerKey\[i\] = innerKeyPad \^ fullLengthKey\[i\];\
> }
>
> // sha256(outterKey + sha256(innerKey, message))\
> // (Buffer.concat makes this harder to read)\
> return sha256(Buffer.concat(\[outterKey,
> sha256(Buffer.concat(\[innerKey, message\]))\]));\
> }
>
> HMACs are used with JWTs when you want a simple way for all parties to
> create and validate JWTs. Any party knowing the key can create new
> JWTs. In other words, with shared keys, it is possible for party to
> impersonate another one: HMAC JWTs do not provide guarantees with
> regards to the creator of the JWT. Anyone knowing the key can create
> one. For certain use cases, this is too permissive. This is where
> asymmetric algorithms come into play.
>
> **RSA and ECDSA algorithms**
>
> Both RSA and ECDSA are asymmetric encryption and digital signature
> algorithms. What asymmetric algorithms bring to the table is the
> possibility of verifying or decrypting a message without being able to
> create a new one. This is key for certain use cases. Picture a big
> company where data generated by the sales team needs to be verified by
> the accounting team. If an HMAC were to be used to sign the data, then
> both the sales team and the accounting team would need to know the
> same key. This would allow the sales team to sign data and make it
> pass as if it were from the accounting team. Although this might seem
> unlikely, especially in the context of a corporation, there are times
> when the ability to verify the creator of a signature is essential.
> JWTs signed or encrypted with RSA or ECDSA provide this capability. A
> party uses its private party to sign a JWT. Receivers in turn use the
> public key (which must be shared in the same way as an HMAC shared
> key) of that party to verify the JWT. The receiving parties cannot
> create new JWTs using the public key of the sender.
>
> Both RSA and ECDSA algorithms are more complex than HMAC. If you are
> interested in the gritty details, read [RFC
> 3447](https://tools.ietf.org/html/rfc3447) for RSA encryption, and the
> original [ECDSA
> paper](http://cs.ucsb.edu/~koc/ccs130h/notes/ecdsa-cert.pdf).
>
> The main difference between RSA and ECDSA lies in speed and key size.
> ECDSA requires smaller keys to achieve the same level of security as
> RSA. This makes it a great choice for small JWTs. RSA, however, is
> usually faster than ECDSA. As usual, pick the one that best aligns
> with your requirements.
>
> **Aside: JWTs are everywhere at Auth0**
>
> At Auth0 we rely heavily on the fetures of JWTs. All of our APIs
> handle authentication and authorization through JWTs. For instance,
> our Lock library returns a JWT that you can store client side and use
> for future requests to your own APIs. Thanks to JWS and JWE, the
> contents of the client-side JWTs are safe.
>
> The following code shows a client-side script that performs
> authentication using our Lock library (plus jQuery) and stores the
> returned JWT as a local storage item:
>
> var lock = null;\
> \$(document).ready(function() {\
> lock = new Auth0Lock('YOUR\_CLIENT\_ID', 'YOUR\_ACCOUNT.auth0.com');\
> });
>
> var userProfile;
>
> \$('.btn-login').click(function(e) {\
> e.preventDefault();\
> lock.show(function(err, profile, token) {\
> if (err) {\
> // Error callback\
> alert('There was an error');\
> } else {\
> // Success callback
>
> // Save the JWT token.\
> localStorage.setItem('userToken', token);
>
> // Save the profile\
> userProfile = profile;\
> }\
> });\
> });
>
> For any future request, the returned JWT can be included as part of
> the HTTP call (jQuery AJAX setup):
>
> \$.ajaxSetup({\
> 'beforeSend': function(xhr) {\
> if (localStorage.getItem('userToken')) {\
> xhr.setRequestHeader('Authorization',\
> 'Bearer ' + localStorage.getItem('userToken'));\
> }\
> }\
> });
>
> **Conclusion**
>
> JWTs are convenient way of representing authentication and
> authorization claims for your application. They are easy to parse,
> human readable and compact. But the killer features are in the JWS and
> JWE specs. With JWS and JWE all claims can be conveniently signed and
> encrypted, while remaining compact enough to be part of every API
> call. Solutions such as session-ids and server-side tokens seem old
> and cumbersome when compared to the power of JWTs. If you haven't
> worked with these technologies yet, we strongly recommend you do so in
> your next project. You won't be disappointed.
>
>  
>
> From
> &lt;<https://auth0.com/blog/2015/12/17/json-web-token-signing-algorithms-overview/>&gt;
>
>  
>
>  
>
> **TL;DR:** Traditional session-based authentication with cookies
> presents difficulties, especially for modern web applications. We can
> instead use JSON Web Tokens (JWT), which make our apps stateless.
> Migrating a legacy app over to JWT authentication can be done piece by
> piece, and if we need to, we can use cookies to handle JWTs. To see
> how this is done, take a look at
> the [repo](https://github.com/auth0/cookie-jwt-auth) for this
> tutorial.
>
>  
>
> Authentication for web applications has historically been fairly
> straightforward and followed a common pattern, but this has been
> changing significantly in recent years. There are several reasons for
> these changes, and the prominent ones are related to the way in which
> modern applications are built and distributed. In this article, we'll
> see how things have changed and also some ways we can adapt legacy
> applications to modern day practices.
>
> **Traditional Web Applications**
>
> In a general sense, traditional websites and applications typically
> implement user authentication using **sessions** and **cookies**. When
> a user logs in to a site, his or her username and password are matched
> against database entries. If the login is successful, the server saves
> the user's authentication state in memory and sends a cookie back in
> the reponse that contains some data, which in most cases includes the
> user's ID. Browsers will save the cookie for the domain from which it
> came and then automatically send it back when subsequent requests are
> made. For example, if a cookie is saved with a domain of auth0.com, it
> will be sent back on any future request to auth0.com as long as it is
> valid. This works great for traditional web apps.
>
> ![](media/image18.png){width="6.0in" height="2.4791666666666665in"}
>
> Even though we've labeled the process described above as being
> "traditional", it should be noted that *most* of the web still
> operates this way. While this approach is still perfectly valid for a
> lot of use cases, we're going to explore some of the reasons why
> relying on it has become challenging for modern web applications.
>
> **Authentication Challenges for Modern Web Apps**
>
> Modern web applications present a few challenges for authentication
> that are difficult to solve using conventional methods. The reasons
> for this have to do with how applications are crafted and the
> environment in which applications reside.
>
> **1. Apps are distributed across many servers**
>
> Many of today's applications aren't deployed the same way they were in
> the past. It is now very common--and often necessary--for apps to be
> distributed across many servers so that up-time is increased and
> latency issues are mitigated. With this comes the side effect that,
> when a user accesses an application, it is no longer guaranteed that
> they are always accessing the same server.
>
> Since traditional authentication relies on the server to keep the
> user's authentication state in memory, things break down when the app
> is accessed from different servers. The user might be logged in on one
> server but not on the others that the application is distributed
> across.
>
> We can get around this by using methods like [**sticky
> sessions**](http://stackoverflow.com/questions/10494431/sticky-and-non-sticky-sessions).
> A sticky session will essentially route the user to the server
> instance from which they logged in so that the authentication state
> can be presevered. This type of workaround will do the job, but as
> we'll see, stateful servers in general don't play that well with
> modern applications.
>
> **2. Apps use APIs for data**
>
> A common pattern for modern applications, especially single-page apps,
> is to retrieve and consume JSON data from a [RESTful
> API](http://www.restapitutorial.com/). Serving data from an API has
> several distinct advantages, one of them being the ability for data to
> be used in more than just one application. For example, an
> organization might start with the intent to build an internally facing
> application, but may soon realize that some of its functionality could
> be used in a public-facing app. Down the road, the organization might
> also decide that some of its data should be accessible by other
> application developers to build third-party apps with. This can all be
> made possible with an API.
>
> Using APIs in this fashion is great, but things can become challenging
> when it comes to authentication. The traditional approach of using
> sessions and cookies for the user's identity doesn't work so well in
> these cases because their use introduces **state** to the application.
> One of the tenets of a RESTful API is that it should be **stateless**,
> meaning that, when a request is made, a response within certain
> parameters can always be anticipated without side effects. A user's
> authentication state introduces such a side effect, which breaks this
> principle. Keeping the API stateless and therefore without side effect
> means that maintainability and debugging are made much easier.
>
> Another challenge here is that it is quite common for an API to be
> served from one server and for the actual application to consume it
> from another. To make this happen, we need to enable [Cross-Origin
> Resource Sharing
> (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS).
> Since cookies can only be used for the domain from which they
> originated, they aren't much help for APIs on different domains than
> the application.
>
> **3. Apps rely on downstream services**
>
> Another common pattern seen with modern web applications is that they
> often rely on downstream services. For example, a call to the main
> application server might make a request to a downstream server before
> the original request is resolved. The issue here is that cookies don't
> "flow" easily to the downstream servers and can't tell those servers
> about the user's authentication state. Since each server has its own
> scheme for cookies, there is a lot of resistance to flow, and
> connecting to them is difficult.
>
> **A Modern Alternative: The JSON Web Token (JWT)**
>
> To combat the issues detailed above, we can take a token-based
> approach by using JSON Web Tokens (JWTs) for authentication. A JWT
> contains three parts:
>
> **1. Header**
>
> The header tells us about the algorithm and token type. It is
> Base64URL encoded.
>
> **2. Payload**
>
> The payload contains any arbitrary information in the form of claims
> that we as developers find useful for our applications. The user's ID
> must be sent as a sub claim, but we can also send other useful
> information, such as the username, email, and more. The payload is
> also Base64URL encoded.
>
> **3. Signature**
>
> The signature is used to verify the authenticity of the JWT. There are
> several different algorithms that can be used for the signature. Some
> algorithms implement a shared secret (HMAC), and others use
> public-private key secrets (RSA).
>
> ![](media/image19.png){width="6.0in" height="6.75in"}
>
> From the user's perspective, logging in to an application that uses
> JWTs looks much like traditional authentication. The user enters his
> or her credentials as usual, but instead of the server creating a
> session and returning a cookie, it will respond with a JSON object
> that contains a JWT. The JWT then needs to be saved locally, which is
> normally done with local storage. However, as we'll see in the next
> section, it is possible to save the JWT in a cookie.
>
> The JWT must be sent to the server to access protected routes, and it
> is typically sent as an Authorization header. The scheme used for this
> header is Bearer, so the full header looks like this:
>
> Authorization: Bearer &lt;token&gt;
>
> Middleware on the protected API routes will check for a valid JWT, and
> if there is one, it will let the request through and return the data
> being requested. Since the user's information is contained within the
> JWT itself, there is no need to look the user up in a database, so
> there is less latency in the application.
>
> It should be reiterated that the user's state is never saved in memory
> on the server, meaning that the user isn't "logged in" in the
> conventional sense. However, a valid JWT gives the user the keys to
> access data each time a request is made, and in this way, a stateless
> authentication mechanism is in place.
>
> ![](media/image20.png){width="6.0in" height="2.4166666666666665in"}
>
> Using a JWT for authentication helps to solve the challenges noted
> above. We can fully rely on data APIs that are stateless and even make
> requests to downstream services. Since JWT is a
> specification [implemented nearly everywhere](http://jwt.io/),
> connecting to downstream services built on a stack other than our own
> is easy. It also doesn't matter which domain is serving our API, nor
> does it matter which specific server a request goes to if the app is
> deployed across many.
>
> **Bridging the Gap: Using JWTs in Cookies**
>
> Modernizing legacy applications by implementing token-based
> authentication can lead to many gains. If it isn't feasible for an
> organization to totally throw away cookies, there are still ways to
> make token authentication viable. Let's take a look at how this can be
> done with NodeJS and the **express-jwt** package.
>
> **Step 1: Set Up a Back End**
>
> To follow along, you can download Auth0's [NodeJS seed
> project](https://auth0.com/docs/node-auth0/master/create-package?path=examples/nodejs-api&filePath=&type=server) from
> the[docs page](https://auth0.com/docs/quickstart/backend/nodejs/).
> Even though we're using an Auth0 seed project here, doing cookie-based
> authentication in this way will work with any service.
>
> **Step 2: Install Cookie Parser**
>
> Once the dependencies for the seed project are installed by following
> the[installation
> steps](https://github.com/auth0/node-auth0/tree/master/examples/nodejs-api),
> we'll need to add one more package: **cookie-parser**. This package
> will allow us to read JWTs from cookies that are sent to the server.
>
> npm install cookie-parser --save
>
> With **cookie-parser** installed, we now need to require and use it
> inserver.js.
>
> // server.js
>
> ...
>
> var cookieParser = require('cookie-parser');
>
> ...
>
> app.configure(function() {
>
> app.use(cookieParser());
>
> ...
>
> });
>
> **Step 3: Save the JWT as a Cookie**
>
> We'll need to retrieve a JWT for a user and save it locally as a
> cookie. If you're using Auth0 for this tutorial, you can find out more
> about retrieving JWTs for users in your Auth0 account by reading
> the [API documentation](https://auth0.com/docs/api/v2). We'll use
> jQuery in this example to make the AJAX calls easy.
>
> Lets make a call to Auth0 to get a JWT.
>
> // app.js
>
> \$('.btn-login').click(function() {\
> \$.ajax({\
> type: 'POST',\
> url: '',\
> data: {\
> client\_id: '{your-client-id}',\
> username: document.querySelector('\#username').value,\
> password: document.querySelector('\#password').value,\
> grant\_type: 'password',\
> scope: 'openid',\
> connection:'Username-Password-Authentication'\
> },\
> success: function(data) {\
> getJwtCookie(data.id\_token);\
> },\
> error: function(error) {\
> console.log('There was an error: ' + error)\
> }
>
> });\
> });
>
> In the success handler, we're calling a function
> called getJwtCookie and passing in the token that was received from
> Auth0. We need to create an endpoint on our application server that
> can validate the JWT that was received from Auth0 and send it back to
> us as a cookie, and we can do that in the getJwtCookie function.
>
> // app.js
>
> function getJwtCookie(token) {\
> \$.ajax({\
> type: 'POST',\
> url: '<http://localhost:3001/secured/authorize-cookie>',\
> data: {\
> token: token\
> },\
> headers: {\
> 'Authorization' : 'Bearer ' + token\
> },\
> success: function() {\
> console.log('Cookie received!');\
> },\
> error: function() {\
> console.log('Problem with cookie');\
> }\
> });\
> }
>
> Next, lets set up the authorize-cookie endpoint to handle this call.
>
> // server.js
>
> app.post('/secured/authorize-cookie', authenticate, function(req, res)
> {\
> res.cookie('id\_token', req.body.token, {\
> expires: new Date(Date.now() + 36000),\
> httpOnly: true\
> });\
> res.send(200, { message: 'Cookie set!' });\
> });
>
> In the next step, we'll set up our **express-jwt** middleware, but
> we're making use of it already in the authorize-cookie route by
> passing it in as the second argument, authenticate. The middleware
> secures the endpoint and a valid JWT will be needed to access it. If
> the JWT is valid, we simply reflect it back as a cookie and set
> the httpOnly flag to true so that the cookie can only be accessed by
> the server. This route accomplishes the steps of validating the JWT
> that was received from Auth0, as well as the step of setting a cookie
> with the JWT.
>
> **Note:** We are using an Authorization header to accomplish our
> cookie JWT in this example. This is the only place we would need to
> make a request using this header--the rest of the application will
> handle JWTs with cookies.
>
> **Step 4: Set Up Middleware to Check for the Cookie**
>
> Normally, the **express-jwt** middleware will look for the presence of
> a header and retrieve the JWT from there. However, we can also create
> a custom function to define how the token should be retrieved.
>
> // server.js
>
> ...
>
> var authenticate = jwt({\
> secret: new Buffer(process.env.AUTH0\_CLIENT\_SECRET, 'base64'),\
> audience: process.env.AUTH0\_CLIENT\_ID,\
> // Custom function to retrieve the JWT\
> // We first look for the JWT in a header and if it isn't there,\
> // we look for it in a cookie\
> getToken: function fromHeaderOrCookie(req) {\
> if(req.headers.authorization && req.headers.authorization.split('
> ')\[0\] === 'Bearer') {\
> return req.headers.authorization.split(' ')\[1\];\
> } else if(req.cookies && req.cookies.id\_token) {\
> return req.cookies.id\_token;\
> }\
> return null;\
> }\
> });
>
> ...
>
> We've added the getToken function as an option on the object that is
> passed into jwt. Our implementation here says that we want to first
> look for the presence of a JWT as an Authorization header, and if
> there isn't anything there, we want to check whether there is a cookie
> with the nameid\_token.
>
> **Step 5: Test the Secured Route**
>
> With the id\_token cookie in place, we can see that requests to
> thesecured/ping endpoint go through just fine.
>
> ![](media/image21.png){width="6.0in" height="3.09375in"}
>
> **Aside: JWT Authentication Is Easy with Auth0**
>
> Auth0 issues [JSON Web Tokens](http://jwt.io/) on every login for your
> users. This means that you can have a solid [identity
> infrastructure](https://auth0.com/docs/identityproviders),
> including [Single Sign On](https://auth0.com/docs/sso/single-sign-on),
> User Management, support for Social (Facebook, Github, Twitter, etc.),
> Enterprise (Active Directory, LDAP, SAML, etc.) and your own database
> of users with just a few lines of code. Auth0 is perfect for [Single
> Page Applications](https://auth0.com/docs/sequence-diagrams) and very
> easy to set up.
>
> As we saw in this tutorial, switching to JWT authentication from
> traditional session-based authentication is very easy, and there are
> many advantages to doing so. Using Auth0 for JWT authentication makes
> the process of switching to JWT authentication even easier. If you'd
> like to see how Auth0 can be used in your legacy application, feel
> free to [get in touch](mailto:support@auth0.com)-we're here to help!
>
> **Wrapping Up**
>
> As we've seen, modern web applications are crafted and deployed in
> ways that make conventional user authentication challenging. JWT
> authentication is an excellent way to get around these challenges and
> allows us to keep our application server stateless. If we need to lean
> on old practices, such as using cookies, we can do so and still
> support JWT authentication with a little tweaking on the server.
>
>  
>
> From
> &lt;<https://auth0.com/blog/2015/09/28/5-steps-to-add-modern-authentication-to-legacy-apps-using-jwts/>&gt;
>
>  
>
>  

 

 

JWT 2

Monday, February 08, 2016

13:50

> *tl;dr If you are
> using [node-jsonwebtoken](https://github.com/auth0/node-jsonwebtoken), [pyjwt](https://github.com/jpadilla/pyjwt/), [namshi/jose](https://github.com/namshi/jose), [php-jwt](https://github.com/firebase/php-jwt)or [jsjwt](https://github.com/kjur/jsjws) with
> asymmetric keys (RS256, RS384, RS512, ES256, ES384, ES512) please
> update to the latest version. See [jwt.io](http://jwt.io/) for more
> information on the vulnerable libraries. (Updated 2015-04-20)*
>
> *This is a guest post from Tim McLean, who is a member of the [Auth0
> Security Researcher Hall of
> Fame](https://auth0.com/whitehat#hall-of-fame). Tim normally blogs
> at[www.timmclean.net](https://www.timmclean.net/).*
>
> Recently, while reviewing the security of various JSON Web Token
> implementations, I found many libraries with critical vulnerabilities
> allowing attackers to bypass the verification step. The same two flaws
> were found across many implementations and languages, so I thought it
> would be helpful to write up exactly where the problems occur. I
> believe that a change to the standard could help prevent future
> vulnerabilities.
>
> For those who are unfamiliar, JSON Web Token (JWT) is a standard for
> creating tokens that assert some number of claims. For example, a
> server could generate a token that has the claim "logged in as admin"
> and provide that to a client. The client could then use that token to
> prove that they are logged in as admin. The tokens are signed by the
> server's key, so the server is able to verify that the token is
> legitimate.
>
> JWTs generally have three parts: a header, a payload, and a signature.
> The header identifies which algorithm is used to generate the
> signature, and looks something like this:
>
> header = '{"alg":"HS256","typ":"JWT"}'
>
> HS256 indicates that this token is signed using HMAC-SHA256.
>
> The payload contains the claims that we wish to make:
>
> payload = '{"loggedInAs":"admin","iat":1422779638}'
>
> As suggested in the JWT spec, we include a timestamp called iat, short
> for "issued at".
>
> The signature is calculated by base64url encoding the header and
> payload and concatenating them with a period as a separator:
>
> key = 'secretkey'\
> unsignedToken = encodeBase64(header) + '.' + encodeBase64(payload)\
> signature = HMAC-SHA256(key, unsignedToken)
>
> To put it all together, we base64url encode the signature, and join
> together the three parts using periods:
>
> token = encodeBase64(header) + '.' + encodeBase64(payload) + '.' +
> encodeBase64(signature)
>
> \# token is now:\
> eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJsb2dnZWRJbkFzIjoiYWRtaW4iLCJpYXQiOjE0MjI3Nzk2Mzh9.gzSraSYS8EXBxLN\_oWnFSRgCzcmJmMjLiuyu5CSpyHI
>
> **Great. So, what's wrong with that?**
>
> Well, let's try to verify a token.
>
> First, we need to determine what algorithm was used to generate the
> signature. No problem, there's an alg field in the header that tells
> us just that.
>
> But wait, we haven't validated this token yet, which means that we
> haven't validated the header. This puts us in an awkward position: in
> order to validate the token, we have to allow attackers to select
> which method we use to verify the signature.
>
> This has disastrous implications for some implementations.
>
> **Meet the "none" algorithm**
>
> The none algorithm is a curious addition to JWT. It is intended to be
> used for situations where the integrity of the token has already been
> verified. Interestingly enough, it is one of only two algorithms that
> are mandatory to implement (the other being HS256).
>
> Unfortunately, some libraries treated tokens signed with
> the nonealgorithm as a valid token with a verified signature. The
> result? Anyone can create their own "signed" tokens with whatever
> payload they want, allowing arbitrary account access on some systems.
>
> Putting together such a token is easy. Modify the above example header
> to contain "alg": "none" instead of HS256. Make any desired changes to
> the payload. Use an empty signature (i.e. signature = "").
>
> Most (hopefully all?) implementations now have a basic check to
> prevent this attack: if a secret key was provided, then token
> verification will fail for tokens using the none algorithm. This is a
> good idea, but it doesn't solve the underlying problem: attackers
> control the choice of algorithm. Let's keep digging.
>
> **RSA or HMAC?**
>
> The JWT spec also defines a number of asymmetric signing algorithms
> (based on RSA and ECDSA). With these algorithms, tokens are created
> and signed using a private key, but verified using a corresponding
> public key. This is pretty neat: if you publish the public key but
> keep the private key to yourself, only you can sign tokens, but anyone
> can check if a given token is correctly signed.
>
> Most of the JWT libraries that I've looked at have an API like this:
>
> \# sometimes called "decode"\
> verify(string token, string verificationKey)\
> \# returns payload if valid token, else throws an error
>
> In systems using HMAC signatures, verificationKey will be the server's
> secret signing key (since HMAC uses the same key for signing and
> verifying):
>
> verify(clientToken, serverHMACSecretKey)
>
> In systems using an asymmetric algorithm, verificationKey will be the
> public key against which the token should be verified:
>
> verify(clientToken, serverRSAPublicKey)
>
> Unfortunately, an attacker can abuse this. If a server is expecting a
> token signed with RSA, but actually receives a token signed with
> HMAC, **it will think the public key is actually an HMAC secret key**.
>
> How is this a disaster? HMAC secret keys are supposed to be kept
> private, while public keys are, well, public. This means that your
> typical [ski mask-wearing
> attacker](https://i.imgur.com/18fM5ja.jpg) has access to the public
> key, and can use this to forge a token that the server will accept.
>
> Doing so is pretty straightforward. First, grab your favourite JWT
> library, and choose a payload for your token. Then, get the public key
> used on the server as a verification key (most likely in the
> text-based PEM format). Finally, sign your token using the
> PEM-formatted public key as an HMAC key. Essentially:
>
> forgedToken = sign(tokenPayload, 'HS256', serverRSAPublicKey)
>
> The trickiest part is making sure that serverRSAPublicKey is identical
> to the verification key used on the server. The strings must match
> exactly for the attack to work -- exact same format, and no extra or
> missing line breaks.
>
> End result? Anyone with knowledge of the public key can forge tokens
> that will pass verification.
>
> **Recommendations for Library Developers**
>
> I suggest that JWT libraries add an algorithm parameter to their
> verification function:
>
> verify(string token, string algorithm, string verificationKey)
>
> The server should already know what algorithm it uses to sign tokens,
> and it's not safe to allow attackers to provide this value.
>
> Some might argue that some servers need to support more than one
> algorithm for compatibility reasons. In this case, a separate key can
> (and should) be used for each supported algorithm. JWT conveniently
> provides a "key ID" field (kid) for exactly this purpose. Since
> servers can use the key ID to look up the key and its corresponding
> algorithm, attackers are no longer able to control the manner in which
> a key is used for verification. In any case, I don't think JWT
> libraries should even look at the alg field in the header, except
> maybe to check that it matches what was the expected algorithm.
>
> Anyone using a JWT implementation should make sure that tokens with a
> different signature type are guaranteed to be rejected. Some libraries
> have an optional mechanism for whitelisting or blacklisting
> algorithms; take advantage of it or you might end up at risk. Even
> better: have a policy of performing security audits on any open source
> libraries that you use to provide mission-critical funtionality.
>
> **Improving the JWT/JWS standard**
>
> I would like to propose deprecating the header's alg field. As we've
> seen here, its misuse can have a devastating impact on the security of
> a JWT/JWS implementation. As far as I can tell, key IDs provide an
> adequate alternative. This warrants a change to the spec: JWT
> libraries continue to be written with security flaws due to their
> dependence on alg.
>
> JWT (and JOSE) present the opportunity to have a cross-platform suite
> of secure cryptography implementations. With these fixes, hopefully
> we're a little bit closer to making that a reality.
>
>  
>
> From
> &lt;<https://auth0.com/blog/2015/03/31/critical-vulnerabilities-in-json-web-token-libraries/>&gt;
>
>  
>
>  
>
> Most APIs today use an **API Key** to authenticate legitimate
> clients. **API Keys** are very simple to use from the consumer
> perspective:

1.  You get an **API key** from the service (in essence a
    > shared secret).

2.  Add the key to an Authorization header.

3.  Call the API.

> It can't get simpler than that, but this approach has some
> limitations.
>
> The last couple of months, we've been working on our [API
> v2](https://docs.auth0.com/apiv2). We wanted to share what we've
> learnt implementing a more powerful security model using [JSON Web
> Tokens](http://jwt.io/).
>
> Using a JSON Web Token offers many advantages:

1.  **Granular Security**: API Keys provide an all-or-nothing access.
    > JSON Web Tokens can provide much finer grained control.

2.  **Homogenous Auth Architecture**: Today we use cookies, API keys,
    > home grown SSO solutions, OAuth etc. Standardizing on JSON Web
    > Tokens gives you an homogenous token format across the board.

3.  **Decentralized Issuance**: API keys depend on a central storage and
    > a service to issue them. JSON Web Tokens can be "self-issued" or
    > be completely externalized, opening interesting scenarios as we
    > will see below.

4.  **OAuth2 Compliance**: OAuth2 uses an opaque token that relies on a
    > central storage. You can return a stateless JWT instead, with the
    > allowed scopes and expiration.

5.  **Debuggability**: API keys are opaque random strings. JSON Web
    > Tokens can be inspected.

6.  **Expiration Control**: API keys usually don't expire unless you
    > revoke them. JSON Web Tokens can (and often do) have
    > an expiration.

7.  **Devices**: You can't put an API key that has full access on a
    > device, because what is on a phone or tablet can easily be stolen.
    > But you can put a JWT with the right set of permissions.

> **Granular Security**
>
> One of the most interesting benefits of using JWTs is the first one
> listed above. Back in the old days, when databases were at the center
> of our client-server applications, we could create users with specific
> permissions on the database:
>
> ![](media/image22.png){width="6.0in" height="3.0416666666666665in"}
>
> *Remember this?*
>
> APIs are becoming central pieces of our distributed systems
> architecture. They are now the "gatekeepers" of our data. But in
> contrast with what was available in databases, virtually all API keys
> provide all-or-nothing access. Readers will likely be familiar with
> the scope parameter of OAuth2 based systems that offers this finer
> grained consent to access.
>
> There are many situations in which you want to keep the simplicity of
> an**API Key** but only for a subset of all possible API operations.
>
> [GitHub acknowledged this
> requirement](https://help.github.com/articles/creating-an-access-token-for-command-line-use/) and
> now provides a way of creating a token with the scopes you need
> (mimicking the OAuth2 consent):
>
> ![](media/image23.gif){width="6.0in" height="5.270833333333333in"}
>
> In the next section, we will go through the details of how this can be
> implemented.
>
> **How to implement it?**
>
> We don't know how GitHub implemented it (they probably used Ruby), but
> we will use it as an example. Let's say we want to implement an
> endpoint in the API to **create new repos**. You could model this with
> the following**JSON Web Token** payload. If you provide any of those
> scopes, then you can create repos:
>
> {\
> iat: 1416929109, // when the token was issued (seconds since epoch)\
> jti: "aa7f8d0a95c", // a unique id for this token (for revocation
> purposes)\
> scopes: \["repo", "public\_repo"\] // what capabilities this token
> has\
> }
>
> *Look at this token
> in [jwt.io](http://jwt.io/?value=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE0MTY5MjkxMDksImp0aSI6ImFhN2Y4ZDBhOTVjIiwic2NvcGVzIjpbInJlcG8iLCJwdWJsaWNfcmVwbyJdfQ.XCEwpBGvOLma4TCoh36FU7XhUbcskygS81HE1uHLf0E)*
>
> The API endpoint would simply check for the presence of the
> right **scope**atribute (this example is written in node.js but any
> language would work):
>
> // intercept all calls to API and validae the token\
> app.use('/api', express\_jwt({secret: SECRET, userProperty:
> 'token\_payload'}));
>
> // for POST /user/repo validate that there is a scope \`repo\` or
> \`public\_repo\`\
> app.post('/api/user/repo',\
> check\_scopes(\['repo', 'public\_repo'\]),\
> function(req, res, next) {\
> // create a repo\
> ....\
> });
>
> Notice the check\_scopes middleware on the /api/user/repo route. This
> is how the check\_scopes function is implemented:
>
> function check\_scopes(scopes) {\
> return function(req, res, next) {\
> //\
> // check if any of the scopes defined in the token,\
> // is one of the scopes declared on check\_scopes\
> //\
> var token = req.token\_payload;\
> for (var i =0; i&lt;token.scopes.length; i++){\
> for (var j=0; j&lt;scopes.length; j++){\
> if(scopes\[j\] === token.scopes\[i\]) return next();\
> }\
> }
>
> return res.send(401, 'insufficient scopes')\
> }\
> }
>
> *Notice that no one can change the scopes variables. JWTs are
> digitally signed, so its content cannot be tampered with.*
>
> Documenting an API is equally important. What would be a good way for
> surfacing this on an API explorer?
>
> For Auth0, we decided to build our own documentation
> using [swagger](http://swagger.io/). Since we are a multi-tenant
> system, each tenant has an API Key and Secret that is used to sign the
> token. As a developer, you mark which scopes you need and a token will
> be auto-generated. You can copy and paste it
> to [jwt.io](http://jwt.io/)to see the structure (this is
> the **debuggable** piece, by the way).
>
> ![](media/image24.gif){width="6.0in" height="4.791666666666667in"}
>
> Scopes required by each operation are clearly identified:
>
> ![](media/image25.png){width="6.0in" height="3.1354166666666665in"}
>
> Our token format is a bit different from the one in the example we
> showed for GitHub. The good thing about JWTs is that they can
> contain *any* data structure:
>
> {\
> iat: 1416929061,\
> jti: "802057ff9b5b4eb7fbb8856b6eb2cc5b",\
> scopes: {\
> users: {\
> actions: \['read', 'create'\]\
> },\
> users\_app\_metadata: {\
> actions: \['read', 'create'\]\
> }\
> }\
> }
>
> The string representation of the scope is read:users but in the JSON
> Web Token, we are using a more structured representation (note the
> hierarchy), this allows us to be more consistent. It also allows us to
> have an easy way to extend it for other scenarios.
>
>  
>
> From
> &lt;<https://auth0.com/blog/2014/12/02/using-json-web-tokens-as-api-keys/>&gt;
>
>  
>
>  
>
>  
>
> **tl;dr**: if you understand why and how to support blacklisting JWTs,
> then skip to
> the [code](https://auth0.com/blog/2015/03/10/blacklist-json-web-token-api-keys/#impl).
>
> On a [previous
> post](https://auth0.com/blog/2014/12/02/using-json-web-tokens-as-api-keys/) we
> proposed an approach to using JSON Web Tokens as API Keys, going over
> some of the benefits of doing so and also providing some examples
> based on our [API v2 scenarios](https://auth0.com/docs/apiv2). This
> post follows up by explaining an aspect that was not covered before:
> how to blacklist a JWT API key so it is no longer valid.
>
> **A real world example**
>
> Let's for a second assume that GitHub used JSON Web Tokens as API Keys
> and one of them was accidentaly published on the web. You would want
> to make sure an app can no longer access your information by revoking
> that token:
>
> ![](media/image26.png){width="6.0in" height="2.1145833333333335in"}
>
> **Framing the problem**
>
> Providing support for blacklisting JWTs poses the following questions:

1.  How are JWTs individually identified?

2.  Who should be able to revoke JWTs?

3.  How are tokens revoked?

4.  How do we avoid adding overhead?

> This blog post aims to answer the previous questions by leveraging our
> experience from implementing this feature in our [API
> v2](https://docs.auth0.com/apiv2).
>
> **1. How are JWTs individually identified?**
>
> To revoke a JWT we need to be able to tell one token apart from
> another one. The JWT spec proposes
> the [jti](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html#jtiDef) (JWT
> ID) as a means to identify a token. From the specification:
>
> *The jti (JWT ID) claim provides a unique identifier for the JWT. The
> identifier value MUST be assigned in a manner that ensures that there
> is a negligible probability that the same value will be accidentally
> assigned to a different data object; if the application uses multiple
> issuers, collisions MUST be prevented among values produced by
> different issuers as well.*
>
> As a quick reminder, this is how the claims section of one of our JWT
> API tokens looks like: 
>
> ![](media/image27.png){width="6.0in" height="3.4791666666666665in"}
>
> The tokens accepted by our API use the aud claim to determine the
> tenant for which the JWT is valid. If we use the (aud, jti) pair as
> the token's identifier then each tenant is in charge of guaranteeing
> that there's no duplication among their tokens.
>
> Similarly, if a token does not include the jti claim we do not allow
> it to be revoked.
>
> **2. Who should be able to revoke JWTs?**
>
> If anyone could revoke our API keys then unfortunately they wouldn't
> be of much use. We need a way of restricting who can revoke a JWT.
>
> The way we solved it in our API is by defining a specific scope
> (permission) that allows blacklisting tokens. If you generate a JWT
> like the one shown in the next figure you will be able to revoke
> JWTs: 
>
> ![](media/image27.png){width="6.0in" height="3.4791666666666665in"}
>
> *Notice the blacklist action nested inside the scopes object.*
>
> **3. How are tokens revoked?**
>
> To blacklist/revoke a token, you need a JWT API key (referred to
> asJWT\_API\_KEY) like the one described in \#2. With it you can issue
> a POSTrequest to /api/v2/blacklists/tokens as shown below (new lines
> added for clarity):
>
> curl -H "Authorization: Bearer {JWT\_API\_KEY}"\
> -X POST\
> -H "Content-Type: application/json"\
> -d '{"aud":"u6nnAxGVjbBd8etXjj554YKGAG5HuVrp","jti":"test-token"}'\
> <https://login.auth0.com/api/v2/blacklists/tokens>
>
> The complete documentation for the endpoint
> is [here](https://auth0.com/docs/apiv2#!/blacklists/post_tokens) but
> basically you need to:

1.  Send the aud and jti claims of the JWT to revoke.

2.  Send the JWT with the permissions necessary to blacklist tokens in
    > the**Authorization** header.

> To get the revoked tokens you can issue
> a GET to/api/v2/blacklists/tokens. You can use
> the [docs](https://auth0.com/docs/apiv2#!/blacklists/get_tokens) to
> figure out the how.
>
> **4. How do we avoid adding overhead?**
>
> You might be thinking:
>
> *Wasn't the whole point of using JWTs avoiding a DB query?*
>
> Well, that is a benefit, though harshly the *whole point*. There is a
> caveat though: that question only applies if you have an application
> with a single issuer, not a multi-tenant system.
>
> If there is more than one tenant, you don't want all of them to share
> the same secret. You still have to perform a database query to map
> the audclaim to the required secret.
>
> With that in mind, these are some of the optimizations that you can
> implement:

1.  **Optimization 1**: The aforementioned operation involves I/O so it
    > can be performed in parallel with our query to verify if a token
    > has been revoked.\
    > *Of course, you can also add a caching layer with a reasonable
    > expiration time to avoid the DB trips altogether.*

2.  **Optimization 2**: Skip the expiration check if the jti claim is
    > not part of the JWT.

3.  **Optimization 3**: To reduce the size of the revoked tokens store
    > you could automatically remove JWTs from it once
    > their [exp](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html#expDef) is
    > reached (assuming there is one).

> **Implementation**
>
> We have shipped version 1.3.0 of the open
> source [express-jwt](https://github.com/auth0/express-jwt) with
> support
> for [multi-tenancy](https://github.com/auth0/express-jwt#multi-tenancy) and [blacklisted
> tokens](https://github.com/auth0/express-jwt#revoked-tokens). We also
> put together
> a [sample](https://github.com/auth0/multitenant-jwt-auth)that shows
> everything working together. The sample is based on our [API
> v2](https://docs.auth0.com/apiv2)implementation.
>
> The following code snippets use show the core sample parts:
>
> **Securing the endpoint**
>
> The first thing we have is an API that we would like to protect.
> The express-jwt middleware is configured by providing:

1.  secret - A function in charge of retrieving the secret.

2.  isRevoked - A function in charge of checking if a JWT is revoked.

> var expressJwt = require('express-jwt');\
> // to protect /api routes with JWTs\
> app.use('/api', expressJwt({\
> secret: secretCallback,\
> isRevoked: isRevokedCallback\
> }));
>
> **Handling multi-tenancy**
>
> The implementation for the secretCallback function reads the backing
> data store to retrieve the secret for a tenant. It caches the secrets
> using the tenant identifier as the cache key.
>
> If the data layer provides an encrypted tenant secret, it needs to be
> decrypted before calling done.
>
> var LRU = require('lru-cache');
>
> var secretsCache = LRU({ /\* options \*/ });
>
> var secretCallback = function(req, payload, done){\
> var audience = payload.aud;\
> var cachedSecret = secretsCache.get(audience);
>
> if (cachedSecret) { return done(null, cachedSecret); }
>
> data.getTenantByIdentifier(audience, function(err, tenant){\
> if (err) { return done(err); }\
> if (!tenant) { return done(new Error('missing\_secret')); }
>
> var secret = utilities.decrypt(tenant.secret);\
> secretsCache.set(audience, secret);\
> done(null, secret);\
> });\
> };
>
> **Supporting revoked JWTs**
>
> Similarly, the isRevokedCallback implementation caches whether a token
> is revoked or not using the (aud, jti) pair as the cache key. It also
> skips the check in case the jti claim is not present.
>
> var jtiCache = LRU({ /\* options \*/ });
>
> var isRevokedCallback = function(req, payload, done){\
> var tokenId = payload.jti;\
> if (!tokenId){\
> // if it does not have jti it cannot be revoked\
> return done(null, false);\
> }
>
> var tokenIdentifier = payload.aud + ':' + payload.jti;\
> var blacklisted = jtiCache.get(tokenIdentifier);\
> if (typeof blacklisted !== 'undefined') { return done(null,
> blacklisted); }
>
> data.getRevokedTokenByIdentifier(tokenIdentifier, function(err,
> token){\
> if (err) { return done(err); }\
> blacklisted = !!token;\
> jtiCache.set(tokenIdentifier,blacklisted)\
> return done(null, blacklisted);\
> });\
> };
>
> From
> &lt;<https://auth0.com/blog/2015/03/10/blacklist-json-web-token-api-keys/>&gt;
>
>  
>
>  

 

 

JWT for java

Monday, February 08, 2016

14:10

Token Authentication for Java Applications

***BY MICAH SILVERMAN *-* AUGUST 13 2015***

In my [last
post](https://stormpath.com/blog/secure-single-page-app-problem/), we
covered a lot of ground, including how we traditionally go about
securing websites, some of the pitfalls of using cookies and sessions,
and how to address those pitfalls by traditional means.

In this post we’ll go beyond the traditional and take a deep dive into
how token authentication with JWTs (JSON Web Tokens) not only addresses
these concerns, but also gives us the benefit of inspectable meta-data
and strong cryptographic signatures.

Token Authentication to the Rescue!

Let’s first examine what we mean by authentication and token in this
context.

Authentication is proving that a user is who they say they are.

A token is a self-contained singular chunk of information. It could have
intrinsic value or not. We are going to look at a particular type of
token that *does* have intrinsic value and addresses a number of the
concerns with session IDs.

JSON Web Tokens (JWTs)

JWTs are a URL-safe, compact, self-contained string with meaningful
information that is usually digitally signed or encrypted. They’re
quickly becoming a de-facto standard for token implementations across
the web.

URL-safe is a fancy way of saying that the entire string is encoded so
there are no special characters and the token can fit in a URL.

The string is opaque and can be used standalone in much the same way
that session IDs are used. By opaque, I mean that looking at the string
itself provides no additional information.

However, the string can also be decoded to pull out-meta data and it’s
signature can be cryptographically verified so that your application
knows that the token has not been tampered with.

JWTs and Oauth2 Access Tokens

Many OAuth2 implementations are using JWTs for their access tokens. It
should be stated that the OAuth2 and JWT specifications are completely
separate from each other and don’t have any dependencies on each other.
Using JWTs as the token mechanism for OAuth2 affords a lot of benefit as
we’ll see below.

JWTs can be stored in cookies, but all the rules for cookies we
discussed [before](https://stormpath.com/blog/secure-single-page-app-problem/) still
apply. You can entirely replace your session id with a JWT. You can then
gain the additional benefit of accessing the meta-information directly
from that session id.

In the wild, they look like just another ugly string:

eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vdHJ1c3R5YXBwLmNvbS8iLCJleHAiOjEzMDA4MTkzODAsInN1YiI6InVzZXJzLzg5ODM0NjIiLCJzY29wZSI6InNlbGYgYXBpL2J1eSJ9.43DXvhrwMGeLLlP4P4izjgsBB2yrpo82oiUPhADakLs

If you look carefully, you can see that there are two periods in the
string. These are significant as they delimit different sections of the
JWT.

eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9\
.\
eyJpc3MiOiJodHRwOi8vdHJ1c3R5YXBwLmNvbS8iLCJleHAiOjEzMDA4MTkzODAsInN1YiI6InVzZXJzLzg5ODM0NjIiLCJzY29wZSI6InNlbGYgYXBpL2J1eSJ9\
.\
43DXvhrwMGeLLlP4P4izjgsBB2yrpo82oiUPhADakLs

JWT Structure

JWTs have a three part structure, each of which is base64-encoded:

![](media/image28.png){width="6.0in" height="2.6041666666666665in"}

Here are the parts decoded:

**Header**

{\
"typ": "JWT",\
"alg": "HS256"\
}

**Claims**

{\
"iss":"http://trustyapp.com/",\
"exp": 1300819380,\
"sub": "users/8983462",\
"scope": "self api/buy"\
}

**Cryptographic Signature**

tß´—™à%O˜v+nî…SZu¯µ€U…8H×

JWT Claims

Let’s examine the claims sections. Each type of claim that is part of
the JWT Specification can be
found [here](https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32).

iss is who issued the token. exp is when the token expires. sub is the
subject of the token. This is usually a user identifier of some sort.

The above parts of the claim are all included in the JWT
specification. scope is not included in the specification, but it is
commonly used to provide authorization information. That is, what parts
of the application the user has access to.

One advantage of JWTs is that arbitrary data can be encoded into the
claims as with scope above. Another advantage is that the client can now
react to this information without any further interaction with the
server. For instance, a portion of the page may be hidden based on the
data found in thescope claim.

**NOTE**: It is still critical and a best practice for the server to
always verify actions taken by the client. If, for instance, some
administrative action was being taken on the client, you would still
want to verify on the application server that the current user had
permission to perform that action. You would never rely on client side
authorization information alone.

You may have picked up on another advantage: the cryptographic
signature. The signature can be verified which proves that the JWT has
not been tampered with. Note that the presence of a crytpographic
signature does not guarantee confidentiality. Confidentiality is ensured
only when the JWT is encrypted *as well as* signed.

Now, for the big kicker: **statelessness**. While the server will need
to generate the JWT, it does not need to store it anywhere as all of the
user meta-data is encoded right in to the JWT. The server and client
could pass the JWT back and forth and never store it. This scales very
well.

Managing Bearer Token Security

Implicit trust is a tradeoff. These types of tokens are often referred
to as Bearer Tokens because all that is required to gain access to the
protected sections of an application is the presentation of a valid,
unexpired token.

You have to address issues like: How long should the token be good for?
How will you revoke it? (There’s a whole other post we could do
on [refresh tokens](http://tools.ietf.org/html/rfc6749#section-1.5).)

You have to be mindful of what you store in the JWT if they are not
encrypted. Do *not* store any sensitive information. It is generally
accepted practice to store a user identifier in the form of
thesub claim. When a JWT is signed, it’s referred to as a JWS. When it’s
encrypted, it’s referred to as a JWE.

Java, JWT and You!

We are very proud of the [JJWT](https://github.com/jwtk/jjwt) project on
Github. Primarily authored by Stormpath’s own CTO, [Les
Hazlewood](https://github.com/lhazlewood), it’s a fully open-source JWT
solution for Java. It’s the easiest to use and understand library for
creating and verifying JSON Web Tokens on the JVM.

How do you create a JWT? Easy peasy!

import io.jsonwebtoken.Jwts;\
import io.jsonwebtoken.SignatureAlgorithm;

byte\[\] key = getSignatureKey();

String jwt =\
Jwts.builder().setIssuer("http://trustyapp.com/")\
.setSubject("users/1300819380")\
.setExpiration(expirationDate)\
.put("scope", "self api/buy")\
.signWith(SignatureAlgorithm.HS256,key)\
.compact();

The first thing to notice is
the [fluent](https://en.wikipedia.org/wiki/Fluent_interface) builder api
used to create a JWT. Method calls are chained culminating in
the compact call which returns the final JWT string.

Also notice that when we are setting one of the claims from the
specification, we use a setter. For
example: .setSubject("users/1300819380"). When a custom claim is set, we
use a call to put and specify both the key and value. For
example: .put("scope", "self api/buy")

It’s just as easy to verify a JWT.

String subject = "HACKER";\
try {\
Jws&lt;Claims&gt; jwtClaims =\
Jwts.parser().setSigningKey(key).parseClaimsJws(jwt);

subject = claims.getBody().getSubject();

//OK, we can trust this JWT

} catch (SignatureException e) {

//don't trust the JWT!\
}

If the JWT has been tampered with in any way, parsing the claims will
throw aSignatureException and the value of the subject variable will
stay HACKER. If it’s a valid JWT, then subject will be extracted from
it: claims.getBody().getSubject()

What is OAuth?

In the next section, we’ll look at an example using Stormpath’s OAuth2
implementation, which makes use of JWTs.

There’s a lot of confusion around the OAuth2 spec. That’s, in part,
because it is really an über spec – it has a lot of complexity. It’s
also because OAuth1.a and OAuth2 are very different beasts. We are going
to look at a very specific, easy to use, subset of the OAuth2 spec. We
have an excellent post that goes into much more detail on [What the Heck
is OAuth](https://stormpath.com/blog/what-the-heck-is-oauth/). Here,
we’ll give some brief background and then jump right into the examples.

OAuth2 is basically a protocol that supports **authorization
workflows**. What this means is that it gives you a way to ensure that a
specific user has permissions to do something.

That’s it.

OAuth2 *isn’t* meant to do stuff like validate a user’s identity —
that’s taken care of by an Authentication service. Authentication is
when you validate a user’s identity (*like asking for a username /
password to log in*), whereas authorization is when you check to see
what permissions an existing user already has.

Just remember that OAuth2 is a protocol for *authorization*.

Using OAuth Grant Types for Authorization

Let’s look at a typical OAuth2 interaction.

POST /oauth/token HTTP/1.1\
Origin: <https://foo.com>\
Content-Type: application/x-www-form-urlencoded

grant\_type=password&username=username&password=password

grant\_type is required. The application/x-www-form-urlencoded content
type is required for this type of interaction as well. Given that you
are passing the username and password over the wire, you
would *always* want the connection to be secure. The good thing,
however, is that the response will have an OAuth2 bearer token. This
token will then be used for every interaction between the browser and
server going forward. There is a very brief exposure here where the
username and password are passed over the wire. Assuming the
authentication service on the server verifies the username and password,
here’s the response:

HTTP/1.1 200 OK\
Content-Type: application/json;charset=UTF-8\
Cache-Control: no-store\
Pragma: no-cache

{\
"access\_token":"2YotnFZFEjr1zCsicMWpAA...",\
"token\_type":"example",\
"expires\_in":3600,\
"refresh\_token":"tGzv3JOkF0XG5Qx2TlKWIA...",\
"example\_parameter":"example\_value"\
}

Notice the Cache-Control and Pragma headers. We don’t want this response
being cached anywhere. The access\_token is what will be used by the
browser in subsequent requests. Again, there is not direct relationship
between OAuth2 and JWT. However, the access\_token can be a JWT. That’s
where the extra benefit of the encoded meta-data comes in. Here’s how
the access token is leveraged in future requests:

GET /admin HTTP/1.1\
Authorization: Bearer 2YotnFZFEjr1zCsicMW...

The Authorization header is a standard header. No custom headers are
required to use OAuth2. Rather than the type being Basic, in this case
the type is Bearer. The access token is included directly after
the Bearer keyword. This completes the OAuth2 interaction for the
password grant type. Every subsequent request from the browser can use
the Authorizaion: Bearer header with the access token.

There’s another grant type known as client\_credentials which
uses client\_id andclient\_secret, rather than username and password.
This grant type is typically used for API interactions. While the client
id and slient secret function similarly to a username and password, they
are usually of a higher quality security and not necessarily human
readable.

Take Us Home: OAuth2 Java Example

We’ve arrived! It’s time to dig into some specific code that
demonstrates JWTs in action.

Spring Boot Web MVC

There are a number of examples in the [Stormpath Java
SDK](https://github.com/stormpath/stormpath-sdk-java). Here, we are
going to look at a Spring Boot Web MVC example. Here’s
the [HelloController](https://github.com/stormpath/stormpath-sdk-java/blob/master/examples/spring-boot-webmvc/src/main/java/tutorial/HelloController.java) from
the example:

@RestController\
public class HelloController {

@RequestMapping("/")\
String home(HttpServletRequest request) {

String name = "World";

Account account = AccountResolver.INSTANCE.getAccount(request);\
if (account != null) {\
name = account.getGivenName();\
}

return "Hello " + name + "!";\
}

}

The key line, for the purposes of this demonstration is:

Account account = AccountResolver.INSTANCE.getAccount(request);

Behind the scenes, account will resolve to an Account object (and not
be null) ONLY if an authenticated session is present.

Build and Run the Example Code

To build and run this example, do the following:

☺ dogeared jobs:0 \~/Projects/StormPath/stormpath-sdk-java
(master|8100m)\
➥ cd examples/spring-boot-webmvc/\
☺ dogeared jobs:0
\~/Projects/StormPath/stormpath-sdk-java/examples/spring-boot-webmvc
(master|8100m)\
➥ mvn clean package\
\[INFO\] Scanning for projects...\
\[INFO\]\
\[INFO\]
------------------------------------------------------------------------\
\[INFO\] Building Stormpath Java SDK :: Examples :: Spring Boot Webapp
1.0.RC4.6-SNAPSHOT\
\[INFO\]
------------------------------------------------------------------------

... skipped output ...

\[INFO\]
------------------------------------------------------------------------\
\[INFO\] BUILD SUCCESS\
\[INFO\]
------------------------------------------------------------------------\
\[INFO\] Total time: 4.865 s\
\[INFO\] Finished at: 2015-08-04T11:46:05-04:00\
\[INFO\] Final Memory: 31M/224M\
\[INFO\]
------------------------------------------------------------------------\
☺ dogeared jobs:0
\~/Projects/StormPath/stormpath-sdk-java/examples/spring-boot-webmvc
(master|8100m)

Launch the Spring Boot Example

You can then launch the Spring Boot example like so:

☺ dogeared jobs:0
\~/Projects/StormPath/stormpath-sdk-java/examples/spring-boot-webmvc
(master|8104m)\
➥ java -jar
target/stormpath-sdk-examples-spring-boot-web-1.0.RC4.6-SNAPSHOT.jar

. \_\_\_\_ \_ \_\_ \_ \_\
/\\\\ / \_\_\_'\_ \_\_ \_ \_(\_)\_ \_\_ \_\_ \_ \\ \\ \\ \\\
( ( )\\\_\_\_ | '\_ | '\_| | '\_ \\/ \_\` | \\ \\ \\ \\\
[\\\\/](NULL) \_\_\_)| |\_)| | | | | || (\_| | ) ) ) )\
' |\_\_\_\_| .\_\_|\_| |\_|\_| |\_\\\_\_, | / / / /\
=========|\_|==============|\_\_\_/=/\_/\_/\_/\
:: Spring Boot :: (v1.2.1.RELEASE)

2015-08-04 11:51:00.127 INFO 17973 --- \[ main\] tutorial.Application :
Starting Application v1.0.RC4.6-SNAPSHOT on MacBook-Pro.local with PID
17973

... skipped output ...

2015-08-04 11:51:04.558 INFO 17973 --- \[ main\]
s.b.c.e.t.TomcatEmbeddedServletContainer : Tomcat started on port(s):
8080 (http)\
2015-08-04 11:51:04.559 INFO 17973 --- \[ main\] tutorial.Application :
Started Application in 4.599 seconds (JVM running for 5.103)

**NOTE**: This assumes that you’ve already setup a Stormpath account and
that your api keys are located in \~/.stormpath/apiKey.properties.
Look [here](http://docs.stormpath.com/java/spring-boot-web/quickstart.html) for
more information on quick setup up of Stormpath with Spring Boot.

Authenticate with a JSON Web Token (or Not)

Now, we can exercise the example and show some JWTs in action! First,
hit your endpoint without any authentication. I like to
use [httpie](https://github.com/jkbrzt/httpie), but any command line
http client will do.

➥ http -v localhost:8080\
GET / HTTP/1.1\
Accept: \*/\*\
Accept-Encoding: gzip, deflate\
Connection: keep-alive\
Host: localhost:8080\
User-Agent: HTTPie/0.9.2

HTTP/1.1 200 OK\
Accept-Charset: big5, big5-hkscs, cesu-8, euc-jp, euc-kr, gb18030, ...\
Content-Length: 12\
Content-Type: text/plain;charset=UTF-8\
Date: Tue, 04 Aug 2015 15:56:41 GMT\
Server: Apache-Coyote/1.1

Hello World!

The -v parameter produces verbose output and shows all the headers for
the request and the response. In this case, the output message is
simply: Hello World!. This is because there is not an established
session.

Authenticate with the Stormpath OAuth Endpoint

Now, let’s hit the oauth endpoint so that our server can authenticate
with Stormpath. You may ask, “What oauth endpoint?” The controller above
doesn’t indicate any such endpoint. Are there other controllers with
other endpoints in the example? No, there are not! Stormpath gives you
oauth (and many other) endpoints right out-of-the-box. Check it out:

➥ http -v --form POST <http://localhost:8080/oauth/token> \\\
&gt; 'Origin:http://localhost:8080' \\\
&gt; grant\_type=password username=micah+demo.jsmith@stormpath.com
password=&lt;actual password&gt;\
POST /oauth/token HTTP/1.1\
Content-Type: application/x-www-form-urlencoded; charset=utf-8\
Host: localhost:8080\
Origin: <http://localhost:8080>\
User-Agent: HTTPie/0.9.2

grant\_type=password&username=micah%2Bdemo.jsmith%40stormpath.com&password=&lt;actual
password&gt;

HTTP/1.1 200 OK\
Cache-Control: no-store\
Content-Length: 325\
Content-Type: application/json;charset=UTF-8\
Date: Tue, 04 Aug 2015 16:02:08 GMT\
Pragma: no-cache\
Server: Apache-Coyote/1.1\
Set-Cookie:
account=eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiIxNDQyNmQxMy1mNThiLTRhNDEtYmVkZS0wYjM0M2ZjZDFhYzAiLCJpYXQiOjE0Mzg3MDQxMjgsInN1YiI6Imh0dHBzOi8vYXBpLnN0b3JtcGF0aC5jb20vdjEvYWNjb3VudHMvNW9NNFdJM1A0eEl3cDRXaURiUmo4MCIsImV4cCI6MTQzODk2MzMyOH0.wcXrS5yGtUoewAKqoqL5JhIQ109s1FMNopL\_50HR\_t4;
Expires=Wed, 05-Aug-2015 16:02:08 GMT; Path=/; HttpOnly

{\
"access\_token":
"eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiIxNDQyNmQxMy1mNThiLTRhNDEtYmVkZS0wYjM0M2ZjZDFhYzAiLCJpYXQiOjE0Mzg3MDQxMjgsInN1YiI6Imh0dHBzOi8vYXBpLnN0b3JtcGF0aC5jb20vdjEvYWNjb3VudHMvNW9NNFdJM1A0eEl3cDRXaURiUmo4MCIsImV4cCI6MTQzODk2MzMyOH0.wcXrS5yGtUoewAKqoqL5JhIQ109s1FMNopL\_50HR\_t4",\
"expires\_in": 259200,\
"token\_type": "Bearer"\
}

There’s a lot going on here, so let’s break it down.

On the first line, I am telling httpie that I want to make a form
url-encoded POST – that’s what the--form and POST parameters do. I am
hitting the /oauth/token endpoint of my locally running server. I
specify an Origin header. This is required to interact with Stormpath
for the security reasons we talked
about [previously](https://stormpath.com/blog/secure-single-page-app-problem).
As per the OAuth2 spec, I am passing upgrant\_type=password along with
a username and password.

The response has a Set-Cookie header as well as a JSON body containing
the OAuth2 access token. And guess what? That access token is also a
JWT. Here are the claims decoded:

{\
"jti": "14426d13-f58b-4a41-bede-0b343fcd1ac0",\
"iat": 1438704128,\
"sub":
"<https://api.stormpath.com/v1/accounts/5oM4WI3P4xIwp4WiDbRj80>",\
"exp": 1438963328\
}

Notice the sub key. That’s the full Stormpath URL to the account I
authenticated as. Now, let’s hit our basic Hello World endpoint again,
only this time, we will use the OAuth2 access token:

➥ http -v localhost:8080 \\\
&gt; 'Authorization: Bearer
eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiIxNDQyNmQxMy1mNThiLTRhNDEtYmVkZS0wYjM0M2ZjZDFhYzAiLCJpYXQiOjE0Mzg3MDQxMjgsInN1YiI6Imh0dHBzOi8vYXBpLnN0b3JtcGF0aC5jb20vdjEvYWNjb3VudHMvNW9NNFdJM1A0eEl3cDRXaURiUmo4MCIsImV4cCI6MTQzODk2MzMyOH0.wcXrS5yGtUoewAKqoqL5JhIQ109s1FMNopL\_50HR\_t4'\
GET / HTTP/1.1\
Authorization: Bearer
eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiIxNDQyNmQxMy1mNThiLTRhNDEtYmVkZS0wYjM0M2ZjZDFhYzAiLCJpYXQiOjE0Mzg3MDQxMjgsInN1YiI6Imh0dHBzOi8vYXBpLnN0b3JtcGF0aC5jb20vdjEvYWNjb3VudHMvNW9NNFdJM1A0eEl3cDRXaURiUmo4MCIsImV4cCI6MTQzODk2MzMyOH0.wcXrS5yGtUoewAKqoqL5JhIQ109s1FMNopL\_50HR\_t4\
Connection: keep-alive\
Host: localhost:8080\
User-Agent: HTTPie/0.9.2

HTTP/1.1 200 OK\
Content-Length: 11\
Content-Type: text/plain;charset=UTF-8\
Date: Tue, 04 Aug 2015 16:44:28 GMT\
Server: Apache-Coyote/1.1

Hello John!

Notice on the last line of the output that the message addresses us by
name. Now that we’ve established an authenticated session with Stormpath
using OAuth2, these lines in the controller retrieve the first name:

Account account = AccountResolver.INSTANCE.getAccount(request);\
if (account != null) {\
name = account.getGivenName();\
}

Summary: Token Authentication for Java Apps

In this post, we’ve looked at how token authentication with JWTs not
only addresses the concerns of traditional approaches, but also gives us
the benefit of inspectable meta-data and strong cryptographic
signatures.

We gave an overview of the OAuth2 protocol and went through a detailed
example of how Stormpath’s implementation of OAuth2 uses JWTs.

Here are some other links to posts on token based authentication, JWTs
and Spring Boot:

 

From
&lt;<https://stormpath.com/blog/token-auth-for-java/?ref=slicedham>&gt;

 

 

Refresh Token

Monday, February 08, 2016

13:41

 

> **Introduction**
>
> Modern authentication and/or authorization solutions have introduced
> the concept of *tokens* into their protocols. Tokens are specially
> crafted pieces of data that carry just enough information to
> either **authorize the user to perform an action**, or allow a client
> to **get additional information about the authorization** process (to
> then complete it). In other words, tokens are pieces of information
> that allow the authorization process to be performed. Whether this
> information is readable or parsable by the client (or any party other
> than the authorization server) is defined by the implementation. The
> important thing is: the client gets this information, and then uses it
> to **get access to a resource**. The JSON Web Token
> (JWT) [spec](https://tools.ietf.org/html/rfc7519) defines a way in
> which common token information may be represented by an
> implementation.
>
> **A short JWT recap**
>
> JWT defines a way in which certain common information pertaining to
> the process of authentication/authorization may be **represented**. As
> the name implies, the data format is **JSON**. JWTs carry
> certain **common fields** such as subject, issuer, expiration time,
> etc. JWTs become really useful when combined with other specs such
> as [JSON Web Signature
> (JWS)](https://tools.ietf.org/html/rfc7515) and [JSON Web Encryption
> (JWE)](https://tools.ietf.org/html/rfc7516). Together these specs
> provide not only all the information usually needed for an
> authorization token, but also a means to**validate the content** of
> the token so that it cannot be tampered with (JWS) and a way
> to **encrypt information** so that it remains **opaque** to the client
> (JWE). The simplicity of the data format (and its other virtues) have
> helped JWTs become one of the most common types of tokens. If you are
> interested in learning how to implement JWTs in your web apps, check
> this
> excellent [post](https://auth0.com/blog/2015/09/28/5-steps-to-add-modern-authentication-to-legacy-apps-using-jwts/) by
> Ryan Chenkie.
>
> **Token types**
>
> For the purposes of this post, we will focus on the two most common
> types of tokens: *access tokens* and *refresh tokens*.

-   **Access tokens** carry the necessary information to access a
    > resource directly. In other words, when a client passes an access
    > token to a server managing a resource, that server can use the
    > information contained in the token to decide whether the client is
    > authorized or not. Access tokens usually have an expiration date
    > and are short-lived.

> ![](media/image29.png){width="6.0in" height="3.75in"}

-   **Refresh tokens** carry the information necessary to get a new
    > access token. In other words, whenever an access token is required
    > to access a specific resource, a client may use a refresh token to
    > get a new access token issued by the authentication server. Common
    > use cases include getting new access tokens after old ones have
    > expired, or getting access to a new resource for the first time.
    > Refresh tokens can also expire but are rather long-lived. Refresh
    > tokens are usually subject to strict storage requirements to
    > ensure they are not leaked. They can also be blacklisted by the
    > authorization server.

> ![](media/image30.png){width="6.0in" height="3.75in"}
>
> Whether tokens are opaque or not is usually defined by the
> implementation. Common implementations allow for **direct
> authorization checks against an access token**. That is, when an
> access token is passed to a server managing a resource, the server can
> read the information contained in the token and decide itself whether
> the user is authorized or not (no checks against an authorization
> server are needed). This is one of the reasons tokens must be signed
> (using JWS, for instance). On the other hand, refresh tokens usually
> require a check against the authorization server. This split way of
> handling authorization checks allows for three things:

-   Improved access patterns against the authorization server (lower
    > load, faster checks)

-   Shorter windows of access for leaked access tokens (these expire
    > quickly, reducing the chance of a leaked token allowing access to
    > a protected resource)

-   Sliding-sessions (see below)

> **Sliding-sessions**
>
> Sliding-sessions are sessions that expire after a **period of
> inactivity**. As you can imagine, this is easily implemented using
> access tokens and refresh tokens. When a user performs an action, a
> new access token is issued. If the user uses an expired access token,
> the session is considered inactive and a new access token is required.
> Whether this token can be obtained with a refresh token or a new
> authentication round is required is defined by the requirements of the
> development team.
>
> **Security considerations**
>
> Refresh tokens are **long-lived**. This means when a client gets a
> refresh token from a server, this token must be **stored securely** to
> keep it from being used by potential attackers. If a refresh token is
> leaked, it may be used to obtain new access tokens (and access
> protected resources) until it is either blacklisted or it expires
> (which may take a long time). Refresh tokens must be issued to a
> single authenticated client to prevent use of leaked tokens by other
> parties. Access tokens must be kept secret, but as you may imagine,
> security considerations are less strict due to their shorter life.
>
> **Example: a refresh-token issuing server**
>
> For the purposes of this example we will use a simple server based
> on [node-oauth2-server](https://github.com/thomseddon/node-oauth2-server) that
> will issue access and refresh tokens. Access tokens will be required
> to access a protected resource. The client will be a simple CURL
> command. The code from this example is based on the [examples from
> node-oauth2-server](https://github.com/thomseddon/node-oauth2-server/tree/master/examples).
> We have modified the base examples to use JWT for access tokens.
>
> Node-oauth2-server uses a predefined API for the model. You can find
> the
> docs [here](https://github.com/thomseddon/node-oauth2-server/blob/master/Readme.md).
> The following code shows how to implement the model for JWT access
> tokens.
>
> DISCLAIMER: Please note the code in the following example is not
> production ready.
>
> model.generateToken = function(type, req, callback) {\
> //Use the default implementation for refresh tokens\
> console.log('generateToken: ' + type);\
> if(type === 'refreshToken') {\
> callback(null, null);\
> return;\
> }
>
> //Use JWT for access tokens\
> var token = jwt.sign({\
> user: req.user.id\
> }, secretKey, {\
> expiresIn: model.accessTokenLifetime,\
> subject: req.client.clientId\
> });
>
> callback(null, token);\
> }
>
> model.getAccessToken = function (bearerToken, callback) {\
> console.log('in getAccessToken (bearerToken: ' + bearerToken + ')');
>
> try {\
> var decoded = jwt.verify(bearerToken, secretKey, {\
> ignoreExpiration: true //handled by OAuth2 server implementation\
> });\
> callback(null, {\
> accessToken: bearerToken,\
> clientId: decoded.sub,\
> userId: decoded.user,\
> expires: new Date(decoded.exp \* 1000)\
> });\
> } catch(e) {\
> callback(e);\
> }\
> };
>
> model.saveAccessToken = function (token, clientId, expires, userId,
> callback) {\
> console.log('in saveAccessToken (token: ' + token +\
> ', clientId: ' + clientId + ', userId: ' + userId.id +\
> ', expires: ' + expires + ')');
>
> //No need to store JWT tokens.\
> console.log(jwt.decode(token, secretKey));
>
> callback(null);\
> };
>
> The OAuth2 token endpoint (/oauth/token) handles issuing of all types
> of grants (password and refresh tokens). All other endpoints are
> protected by the OAuth2 middleware that checks for the access token.
>
> // Handle token grant requests\
> app.all('/oauth/token', app.oauth.grant());
>
> app.get('/secret', app.oauth.authorise(), function (req, res) {\
> // Will require a valid access\_token\
> res.send('Secret area');\
> });
>
> So, for instance, assuming there is a user 'test' with password 'test'
> and a client 'testclient' with a client secret 'secret', one could
> request a new access token/refresh token pair as follows:
>
> \$ curl -X POST -H 'Authorization: Basic dGVzdGNsaWVudDpzZWNyZXQ=' -d
> 'grant\_type=password&username=test&password=test'
> localhost:3000/oauth/token
>
> {\
> "token\_type":"bearer",\
> "access\_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiVlx1MDAxNcKbwoNUwoonbFPCu8KhwrYiLCJpYXQiOjE0NDQyNjI1NDMsImV4cCI6MTQ0NDI2MjU2M30.MldruS1PvZaRZIJR4legQaauQ3\_DYKxxP2rFnD37Ip4",\
> "expires\_in":20,\
> "refresh\_token":"fdb8fdbecf1d03ce5e6125c067733c0d51de209c"\
> }
>
> The authorization header contains the client id and secret encoded as
> BASE64 (testclient:secret).
>
> To access a protected resource with that access token:
>
> \$ curl
> 'localhost:3000/secret?access\_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiVlx1MDAxNcKbwoNUwoonbFPCu8KhwrYiLCJpYXQiOjE0NDQyNjI1NDMsImV4cCI6MTQ0NDI2MjU2M30.MldruS1PvZaRZIJR4legQaauQ3\_DYKxxP2rFnD37Ip4'
>
> Secret area
>
> Access to the "secret area" will not cause a database lookup to
> validate the access token thanks to JWT.
>
> Once the token has expired:
>
> \$ curl
> 'localhost:3000/secret?access\_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiVlx1MDAxNcKbwoNUwoonbFPCu8KhwrYiLCJpYXQiOjE0NDQyNjI2MTEsImV4cCI6MTQ0NDI2MjYzMX0.KkHI8KkF4nmi9z6rAQu9uffJjiJuNnsMg1DC3CnmEV0'
>
> {\
> "code":401,\
> "error":"invalid\_token",\
> "error\_description":"The access token provided has expired."\
> }
>
> Now we can use the refresh token to get a new access token by hitting
> the token endpoint like so:
>
> curl -X POST -H 'Authorization: Basic dGVzdGNsaWVudDpzZWNyZXQ=' -d
> 'refresh\_token=fdb8fdbecf1d03ce5e6125c067733c0d51de209c&grant\_type=refresh\_token'
> localhost:3000/oauth/token
>
> {\
> "token\_type":"bearer",\
> "access\_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiVlx1MDAxNcKbwoNUwoonbFPCu8KhwrYiLCJpYXQiOjE0NDQyNjI4NjYsImV4cCI6MTQ0NDI2Mjg4Nn0.Dww7TC-d0teDAgsmKHw7bhF2THNichsE6rVJq9xu\_2s",\
> "expires\_in":20,\
> "refresh\_token":"7fd15938c823cf58e78019bea2af142f9449696a"\
> }
>
> DISCLAIMER: Please note the code in the previous example is not
> production ready.
>
> See the full
> code [here](https://github.com/auth0/blog-refresh-tokens-sample).
>
> **Aside: use refresh tokens in your Auth0 apps**
>
> At Auth0 we do the hard part of authentication for you. Refresh tokens
> are not an exception. Once you have [setup your
> app](https://auth0.com/docs) with us, follow the
> docs[here](https://auth0.com/docs/refresh-token) to learn how to get a
> refresh token.
>
> **Conclusion**
>
> Refresh tokens improve security and allow for reduced latency and
> better access patterns to authorization servers. Implementations can
> be simple using tools such as JWT + JWS. If you are interested in
> learning more about tokens (and cookies), check our
> article [here](https://auth0.com/blog/2014/01/27/ten-things-you-should-know-about-tokens-and-cookies/).
>
>  
>
> From
> &lt;<https://auth0.com/blog/2015/10/07/refresh-tokens-what-are-they-and-when-to-use-them/>&gt;

 

 

Single Sign On

Monday, February 08, 2016

13:47

> Nowadays, almost every website requires some form of authentication to
> access its features and content. With the number of websites and
> services rising, a centralized login system has become a necessity.
> Single-sign-on (SSO) is now required more than ever. In this two-piece
> post we will study how SSO is implemented for the web and provide a
> working example using OpenID Connect (in part 2). Read on!
>
>  
>
> **Federated identity glossary**
>
> The concept of a centralized or linked electronic identity is known
> as*federated identity*. Federated identity systems handle several
> concerns:

-   Authentication

-   Authorization

-   User attributes exchange

-   User management

> The **authentication** aspect deals with validating user credentials
> and establishing the identity of the user. **Authorization** is
> related to access restrictions (e.g., is the user allowed to access X
> resource?). The **attributes exchange** aspect deals with data sharing
> across different user management systems. For instance, fields such
> as *"real name"* may be present in multiple systems. A federated
> identity system prevents data duplication by linking the related
> attributes. Lastly, **user management** is related to the
> administration (creation, deletion, update) of user accounts. A
> federated identity system usually provides the means for
> administrators (or users) to handle accounts across domains or
> subsystems.
>
> SSO is strictly related to the **authentication** part of a federated
> identity system. Its only concern is establishing the identity of the
> user and then sharing that information with each subsystem that
> requires the data. Below, we focus on this crucial aspect of a
> federated identity system.
>
> **Single sign on (SSO)**
>
> Sooner or later web development teams face one problem: you have
> developed an application at domain X and now you want your new
> deployment at domain Y to use the same login information as the other
> domain. In fact, you want more: you want users who are **already
> logged-in**at domain X to be already logged-in at domain Y. This is
> what SSO is all about.
>
> ![](media/image31.png){width="6.0in" height="3.4895833333333335in"}
>
> The obvious solution to this problem is to **share session
> information**across different domains. However, for security reasons,
> browsers enforce a policy known as the *same origin policy*. This
> policy dictates that cookies (and other locally stored data)
> can **only be accessed by its creator** (i.e. the domain that
> originally requested the data to be stored). In other words, domain X
> cannot access cookies from domain Y or vice versa. This is what SSO
> solutions solve in one way or the other: sharing session information
> across different domains.
>
> ![](media/image32.png){width="6.0in" height="3.4895833333333335in"}
>
> Different SSO protocols share session information in different ways,
> but the essential concept is the same: there is a **central domain**,
> through which authentication is performed, and then the **session is
> shared** with other domains in some way. For instance, the central
> domain may generate a signed JSON Web Token (which may be encrypted
> using JWE). This token may then be passed to the client and used by
> the authentication domain as well as any other domains. The token can
> be passed to the original domain by a redirect and contains all the
> information needed to identify the user for the domain requiring
> authentication. As the token is signed, it cannot be modified in any
> way by the client.
>
> ![](media/image33.png){width="6.0in" height="3.4895833333333335in"}
>
> Whenever the user goes to a domain that requires authentication, he or
> she is **redirected** to the authentication domain. As the user
> is **already logged-in** at that domain, he or she can be immeditely
> redirected to the original domain with the necessary authentication
> token.
>
> ![](media/image34.png){width="6.0in" height="4.1875in"}
>
> **Different protocols**
>
> If you have been reading about SSO online, you have probably found
> that there are many different implementations: OpenID Connect,
> Facebook Connect, SAML, Microsoft Account (formerly known as
> Passport), etc. Our advice is to choose whatever is simplest for your
> development efforts. For instance, SAML is deeply entrenched in
> enterprise developments, so in some cases it will make sense to pick
> that. If you think you will need to integrate your development with
> more than one alternative, don't despair: there are frameworks that
> allow interoperability between different SSO solutions. In fact,
> that's one of the things we do at Auth0.
>
> **Aside: SSO with Auth0**
>
> If you are already using Auth0 in your developments, you know how easy
> it is to do SSO. If not, please see the [docs on single sign
> on](https://auth0.com/docs/sso/single-sign-on) and check out
> the[examples](https://github.com/auth0/auth0-sso-sample). Our SSO
> solution works as a *bridge* between different SSO frameworks. So
> whatever your existing apps are using, it has never been easier to
> integrate SSO into them. We do the hard work for you.
>
> ![](media/image35.png){width="6.0in" height="3.8333333333333335in"}
>
>  
>
> From
> &lt;<https://auth0.com/blog/2015/09/23/what-is-and-how-does-single-sign-on-work/>&gt;

 

 

GIT

Monday, February 08, 2016

13:54

It can be tough for your team to know exactly why they need the changes
you’re proposing in a pull request. What if we could give them more
context? There’s an episode of [The Weekly
Iteration](https://upcase.com/videos/tips-for-code-review) where a
simple trick was mentioned. After adopting it myself, I have noticed my
co-workers commenting on how useful these messages have been in
providing context.

**+**

The trick is simple. Split your PR message into two sections:

**+**

Some awesome title

Why:

\* ...

This change addresses the need by:

\* ...

**+**

Starting with this structure forces you to answer why the change is
necessary before outlining the changes that you have made towards this
goal.

**Automation!**

**+**

We can tell git to setup our commit messages with this structure. This
is done by settingcommit.template in \~/.gitconfig:

**+**

\[commit\]\
template = \~/.gitmessage

**+**

Then create \~/.gitmessage with our new default:

**+**

 

Why:

\*

This change addresses the need by:

\*

*\# 50-character subject line*\
*\#*\
*\# 72-character wrapped longer description.*

 

From
&lt;<https://robots.thoughtbot.com/better-commit-messages-with-a-gitmessage-template?ref=slicedham>&gt;

 

 

REST

Monday, February 08, 2016

14:00

 

> The Fundamentals of REST API Design
>
> Here at Stormpath, we give developers easy access to user management
> features – including authentication, authorization, and password reset
> – via our REST API and language-specific SDKs. Our team of experts
> began with already-significant knowledge about REST+JSON API design.
> In the process of building the REST API, they learned even more. Our
> CTO, Les Hazelwood, gave a well-received presentation to a group of
> Java developers on REST+JSON API design best practices, which you can
> watch here:
>
> We’ve also written posts on how best to [secure your REST
> API](https://stormpath.com/blog/secure-your-rest-api-right-way/), as
> well as [linking and resource expansion in REST
> APIs](https://stormpath.com/blog/linking-and-resource-expansion-rest-api-tips/).
> This post will give a high level summary of the key points that Les
> touches on in his talk – specifically the fundamentals of good
> REST+JSON API design.
>
> So Why REST?
>
> Keeping the goal of rapid adoption of an API in mind, what makes
> RESTful APIs so appealing? Per Dr. Roy Fielding’s thesis on the REST
> paradigm, there are 6 distinct advantages of REST:

1.  Scalability – not necessarily its performance, yet rather how easy
    > it is for RESTful APIs to adapt and grow and be plugged into
    > other systems.

2.  Use of HTTP – being able to use HTTP methods to manage resources
    > makes RESTful APIs easy to plug into other applications.

3.  Independency – with a REST API you can deploy or scale down specific
    > parts of the application, without having to shut down the entire
    > application or an entire web server form.

4.  Reduced latency due to caching – REST APIs prioritize caching, which
    > helps to improve latency. So always keep caching top of mind when
    > you’re developing your REST API.

5.  Security – HTTP specification lets you sport security via certain
    > HTTP headers, so you can leverage this to make your API secure.

6.  Encapsulation – there are parts of the application that don’t need
    > to be exposed to a REST caller, and REST as an architectural style
    > allows you to encapsulate those gritty details and only show
    > things that you need to show.

> And Why JSON?

1.  Ubiquity – over 57 percent of all web-based applications have JSON,
    > are built on JavaScript, or have JavaScript components.

2.  Human readable – it uses very simple grammar and language, so a
    > human can easily read it, including folks just starting to get
    > into software development.

3.  It’s easy to change or add new fields.

> What makes REST design difficult?
>
> RESTful APIs are difficult to design because REST is an architectural
> style, and not a specification. It has no standard governing body and
> therefore has no hard and fast design rules. What REST does have is an
> interpretation of how HTTP protocol works, which allows for lots of
> different approaches for designing a REST API. While use of HTTP
> methods is a core advantage of the REST approach, it also means that
> there are lots of different RESTful API designs. We’re going to focus
> on some of the best guidelines that we’ve come up with in designing
> our REST API.
>
> REST API Design Guidelines
>
> 1\. Keep your REST API resources coarse grained, not fine grained
>
> Basically, you don’t know how your user is going to interact with your
> resources. In the case of Stormpath, resources would be accounts,
> groups, or directories. There are lots of different actions they might
> run on those resources and if they are adding in lots of arguments to
> methods they’ve written for a particular resource, it can be difficult
> to manage. So we recommend that, for a given resource in your REST
> API, you write a method that takes the resource itself as an argument,
> and the method contains all the functionality needed for said
> resource.
>
> How else do you keep things coarse grained? You work with collection
> and instance resources. A collection resource is what it sounds like –
> basically a folder containing similar resources. An instance resource
> is a singular instance of its parent resource. This allows you to use
> HTTP behavior that affects an end point definition (an instance
> resource), but doesn’t actually create another url for each
> instance-behavior combination. So don’t add behavior to the actual end
> point definition.
>
> 2\. Use POST to take advantage of partial updates in your REST API
>
> Since REST APIs run on standard HTTP methods, you can use PUT or POST
> to either create or update resources. You might think of using PUT to
> create a resource and POST to update a resource, but you can actually
> use POST for both, and that’s recommended.
>
> Why would you want to use POST to both create and update a resource?
>
> Because with POST you don’t need to send over all fields for that data
> resource on every call you make, whereas with PUT, you do. This is
> important because if for every update you make you are also sending
> over fields that are not updating, then your data plan is consuming
> more than it needs to. Using POST instead of PUT can be beneficial if
> your REST API is metered as it limits the quantity of traffic.
> Furthermore, when you get into millions or hundreds of millions of
> requests per month, that impacts your REST API’s performance – so use
> POST to limit the traffic.
>
> And why can’t you do the same with PUT?
>
> Because per HTTP specification, PUT is idempotent, meaning it has to
> have all its properties included (or the result will not be the same).
> For example, if you first create an application without specifying a
> description, and then in a fourth call you send in the description,
> the state may have been different in between, therefore breaking the
> idempotency mandate.
>
> 3\. Have REST API documents link to other documents based on the notion
> of a media type
>
> A media type is a specification of a data format and a set of parsing
> rules associated with that specification. With your REST API, if
> you’re writing as a client, be sure to include your preferred data
> format you would like returned in the accept-header. Likewise, as the
> server, return back a content-type header that notes how the data is
> actually being returned. You can also add additional parsing rules to
> whatever data type you’re using. For example, you might have media
> type application/JSON+foo which tells the client not only is this JSON
> formatted data, but it’s also foo, which tells the client how to parse
> that data.
>
> So make sure to send through accept headers specifying what media type
> you want (if on the client side), send through content-type headers
> telling the client what data format you are returning (if on server
> side), and take advantage of customizing your own media types to make
> your rest API more flexible for your clients.
>
> Conclusion
>
> In this post we’ve covered the advantages of the RESTful API design
> approach, as well as the fundamentals for creating a
> developer-friendly REST API. This is merely a summary of Les’ points,
> and only the first 30 minutes at that, so be sure to check out the
> rest of the presentation.
>
>  
>
> From
> &lt;<https://stormpath.com/blog/fundamentals-rest-api-design/?ref=slicedham>&gt;
>
>  
>
> VIDEO: <https://stormpath.com/blog/designing-rest-json-apis/>
>
>  
>
> Security: <https://stormpath.com/blog/secure-your-rest-api-right-way/>
>
>  
>
>  
>
>  

 

 

Kafka

Monday, February 08, 2016

14:07

 

**Scaling With Kafka**

Posted by **Alex Etling** / Software Engineer at GameChanger 

February 3, 2016

At GameChanger(GC), we recently decided to
use [Kafka](http://kafka.apache.org/documentation.html) as a core piece
in our new data pipeline project. We chose Kafka for its consistency and
availability, ability to provide ordered messages logs, and its
impressive throughput. This is the second in a series 2 blog posts I
will be doing that describe how we found the best Kafka configuration
for GC. My [first blog
post](http://tech.gc.com/experimenting-with-kafka) discussed learning
about Kafka through experimentation and the scientific method.

In this blog post I am going to address a specific pain point I saw in
our Kafka setup: adding and removing boxes from the Kafka cluster. I
will start by examining the Kafka system and pain points I faced. Next I
will present a series of iterations that made the scaling process easier
and easier. Finally, I will show how our current setup allows for no
hassle box management.

To explain the problems I was facing with scaling Kafka, I need to give
some background on how Kafka boxes (brokers) work. When a new box starts
up, a broker.id must be specified in the server.properties file for that
box. Immediately this presents a set of problems that need to be
addressed. As mentioned in some of my
other [blog](http://tech.gc.com/adding-a-new-box-type-fun-with-kafka-1) [posts](http://tech.gc.com/adding-a-new-box-type-fun-with-kafka-2),
I set up our Kafka boxes using AWS’ auto scaling feature. This means all
of the boxes are essentially identical. How do I specify a
different broker.id for each box, if they all run the same launch
config? This problem makes just launching Kafka boxes hard.

The solution I developed was to create a distinct broker.id based off of
the box’s IP. This guaranteed uniqueness between boxes and allowed each
new box to easily get a broker.id. To do this I added a bash script to
the Kafka Docker image. The script is below:

FOURTHPOWER**=**\`echo '256\^3' | bc\`\
THIRDPOWER**=**\`echo '256\^2' | bc\`\
SECONDPOWER**=**\`echo '256\^1' | bc\`

ID**=**\`curl <http://169.254.169.254/latest/meta-data/local-ipv4%60>\
FOURTHIP**=**\`echo \$ID | cut -d '.' -f 1\`\
THIRDIP**=**\`echo \$ID | cut -d '.' -f 2\`\
SECONDIP**=**\`echo \$ID | cut -d '.' -f 3\`\
FIRSTIP**=**\`echo \$ID | cut -d '.' -f 4\`\
BROKER\_ID**=**\`expr \$FOURTHIP \\\* \$FOURTHPOWER + \$THIRDIP \\\*
\$THIRDPOWER + \$SECONDIP \\\* \$SECONDPOWER + \$FIRSTIP\`

The script gets the IP of the machine using AWS’ metadata endpoint. It
then constructs a 32 bit broker.id from this IP. This was a workable
first step, and allowed me to launch as many new boxes as I wanted. But
I still had issues.

In order to explain these issues, I need describe how Kafka partitions
work. To do this I need to define some terms:

![](media/image36.png){width="5.239583333333333in"
height="2.5104166666666665in"}

-   Broker - box with a unique broker.id

-   Partition - smallest bucket size at which data is managed in Kafka

-   Replication Factor - \# of brokers that have a copy of a partitions
    > data

-   Replica Set - set of brokers that a partition is assigned to live on

-   In Sync Replicas - brokers in the replica set whose copy of the
    > partition’s data is up to date

When a partition is created, it is assigned to a replica set of brokers.
This replica set does not change. For example, If I were to create a new
partition with replication factor 3 that ended up on brokers 1, 2, and
3, the replica set be brokers 1, 2, and 3. If broker 1 were to crash,
the replica set would stay 1, 2, and 3 but the in sync replicas would
shrink to 2 and 3.

So why is this implementation detail a pain point for Kafka? Imagine the
following scenario: (See the visual below)

-   One of our boxes on AWS was marked for retirement and needed to be
    > replaced with a new box in our cluster.

-   The way we were doing box names meant we were replacing a box with
    > broker.id X with a box with broker.id A.

-   If broker X is replaced with A, the partition whose replica set is
    > X,Y,Z does not change. Its in sync replicas just goes from X,Y,Z
    > -&gt; Y,Z.

-   The new broker A, does not join the replica set and does not start
    > helping with load. In essence the new box does nothing.

![](media/image37.png){width="6.0in" height="2.0208333333333335in"}

 

![](media/image38.png){width="6.0in" height="2.0416666666666665in"}

In order to enable A to start doing work in the cluster, I had to run a
time consuming and confusing script. To combat this issue, I could have
manually given the new box the same broker.id as the old box, but that
defeats the idea of an autoscaler. What could I do?

I needed a better algorithm to define the broker.id. I switched form
using the bash script using an IP -&gt; broker.idmapping to using the
following python script:

**import** os\
**from** kazoo.client **import** KazooClient

zk **=** KazooClient(hosts**=**os**.**getenv('ZOOKEEPER\_SERVER\_1'))\
zk**.**start()

zk\_broker\_ids **=** zk**.**get\_children('/brokers/ids')\
set\_broker\_ids **=** set(map(int, zk\_broker\_ids))\
possible\_broker\_ids **=** set(range(100))

broker\_id **=** sorted(possible\_broker\_ids **-**
set\_broker\_ids)\[0\]

**print** broker\_id

This algorithm checks with the zookeeper cluster to get all current
boxes. It then gets the lowest broker.id that is not taken by a
different box. This simple algorithm change makes all the difference for
ease of scaling.

Lets go back to a scenario where I needed to replace a box. I had boxes
1,2,3 and killed box 2. When the autoscaler launched a new box, the
broker was assigned the lowest available broker.id (2). After startup,
the new broker 2 saw that it should have had the data that the old,
removed broker 2 had. It then began to sync itself into the cluster, to
get full copies of all the data, and eventually became a leader of some
of the partitions. All of this happens with no manual work from
developers! (See the visual below)

![](media/image39.png){width="6.0in" height="2.0416666666666665in"}

 

![](media/image40.png){width="6.0in" height="2.0416666666666665in"}

 

![](media/image41.png){width="6.0in" height="2.0416666666666665in"}

I was getting to a place where switching out boxes and growing the
cluster was becoming very easy. There was still a limiting factor
though: time to sync in a node. Going back to the scenario where there
are 3 boxes with broker.id1,2,3 and say each box had upwards of 1 TB of
data on it. Box 3 now dies. It was very slow for new broker 3 to sync
into the cluster and for the cluster to get back to a completely safe
state. Could I shorten this time?

The answer was obviously yes, and to do it I needed to use two different
technologies: [AWS’ Elastic Block
Store](https://aws.amazon.com/ebs/)(EBS) and [Docker volume
mounts](https://docs.docker.com/engine/userguide/dockervolumes/). EBS
allows for specification of an independent storage device that can
attach to an EC2 box. So if I had a Kafka box running, I could mount an
EBS volume at / on that computer. I could then ensure that Kafka was
writing all of its data to / using Docker volume mounts. All the data
written to / will actually be written to the EBS volume. In a pinch, I
could manually take that EBS volume, detach it from the box, and mount
it on another machine. Suddenly, I had the ability to take all the data
from a box that was shutting down and move it to a new box quickly!

Through a series of steps and improvements, it is now fast, simple, and
easy to scale our Kafka infrastructure. When there is so much else I
have to put my attention on, scaling boxes should be kept out of site
and out of mind. I recommend taking similar steps in your own cluster to
make scaling Kafka easy.

 

From &lt;<http://tech.gc.com/scaling-with-kafka/?ref=slicedham>&gt;

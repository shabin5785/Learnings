 

Monday, April 25, 2016

11:02

Node.js is a very powerful JavaScript-based framework/platform built on
Google Chrome's JavaScript V8 Engine. It is used to develop I/O
intensive web applications like video streaming sites, single-page
applications, and other web applications. Node.js is a platform built on
Chrome's JavaScript runtime for easily building fast and scalable
network applications. Node.js uses an event-driven, non-blocking I/O
model that makes it lightweight and efficient, perfect for
data-intensive real-time applications that run across distributed
devices

 

***V8 Engine***

 

The V8 JavaScript Engine is an open source JavaScript engine developed
by The Chromium Project for the Google Chrome web browser.\[5\] It has
since seen use in many other projects, such as Couchbase, MongoDB and
Node.js that are used server side. V8 compiles JavaScript to native
machine code (IA-32, x86-64, ARM, or MIPS ISAs; has also been ported to
PowerPC\[7\] and IBM s390\[8\]\[9\] for use in servers)\[3\]\[10\]
before executing it, instead of more traditional techniques such as
interpreting bytecode or compiling the whole program to machine code and
executing it from a filesystem. The compiled code is additionally
optimized (and re-optimized) dynamically at runtime, based on heuristics
of the code's execution profile. Optimization techniques used include
inlining, elision of expensive runtime properties, and inline caching,
among many others.

 

***NodeJS features***

 

**Asynchronous and Event Driven*:*** All APIs of Node.js library are
asynchronous that is, non-blocking. It essentially means a Node.js based
server never waits for an API to return data. The server moves to the
next API after calling it and a notification mechanism of Events of
Node.js helps the server to get a response from the previous API call.

 

**Single Threaded but Highly Scalable** - Node.js uses a single threaded
model with event looping. Event mechanism helps the server to respond in
a non-blocking way and makes the server highly scalable as opposed to
traditional servers which create limited threads to handle requests.
Node.js uses a single threaded program and the same program can provide
service to a much larger number of requests than traditional servers
like Apache HTTP Server.

 

![](media/image1.png){width="6.09375in" height="3.53125in"}

 

REPL stands for **Read Eval Print Loop** and it represents a computer
environment like a window console or Unix/Linux shell where a command is
entered and system responds with an output in interactive mode. Node.js
or Node comes bundled with a REPL environment. It performs the following
desired tasks.

-   **Read** - Reads user's input, parse the input into JavaScript
    > data-structure and stores in memory.

-   **Eval** - Takes and evaluates the data structure

-   **Print** - Prints the result

-   **Loop** - Loops the above command until user press **ctrl-c** twice

 

Node Package Manager (npm) provides following two main functionalities:

-   Online repositories for node.js packages/modules which are
    > searchable on [search.nodejs.org](http://search.nodejs.org/)

-   Command line utility to install Node.js packages, do version
    > management and dependency management of Node.js packages.

> npm comes bundled with Node.js installables after v0.6.3 version

 

***Global vs Local installation***

 

By default, npm installs any dependency in the local mode. Here local
mode refers to the package installation in node\_modules directory lying
in the folder where Node application is present. Locally deployed
packages are accessible via require() method. For example when we
installed express module, it created node\_modules directory in the
current directory where it installed express module. Alternatively you
can use npm ls command to list down all the locally installed modules.

 

Globally installed packages/dependencies are stored in system directory.
Such dependencies can be used in CLI (Command Line Interface) function
of any node.js but can not be imported using require() in Node
application directly.

 

\$ npm install express -g

 

This will produce similar result but module will be installed globally.

You can use following command to check all the modules installed
globally:

\$ npm ls -g

 

***package.json***

 

package.json is present in the root directory of any Node
application/module and is used to define the properties of a package

 

**Attributes of Package.json**

name - name of the package

 

version - version of the package

 

description - description of the package

 

homepage - homepage of the package

 

author - author of the package

 

contributors - name of the contributors to the package

 

dependencies - list of dependencies. npm automatically installs all the
dependencies mentioned here in the node\_module folder of the package.

 

repository - repository type and url of the package

 

main - entry point of the package

 

keywords - keywords

 

***Uninstalling Modules***

 

Use following command to uninstall a Node.js module.

\$ npm uninstall express

 

Search package name using npm.

\$ npm search express

 

***Create a module***

Creation of module requires package.json to be generated. Let's generate
package.json using npm, which will generate basic skeleton of the
package.json.

\$ npm init

 

Use the following command to register yourself with npm repository site
using a valid email address.

\$ npm adduser

 

Now its time to publish your module:

\$ npm publish

 

 

***Callback***

 

Callback is an asynchronous equivalent for a function. A callback
function is called at the completion of a given task. Node makes heavy
use of callbacks. All APIs of Node are written is such a way that they
supports callbacks. For example, a function to read a file may start
reading file and return the control to execution environment immidiately
so that next instruction can be executed. Once file I/O is complete, it
will call the callback function while passing the callback function, the
content of the file as parameter. So there is no blocking or wait for
File I/O. This makes Node.js highly scalable, as it can process high
number of request without waiting for any function to return result.

 

 

***Event Driven Programming***

 

Node js is a single threaded application but it support concurrency via
concept of event and callbacks. As every API of Node js are asynchronous
and being a single thread, it uses async function calls to maintain the
concurrency. Node uses observer pattern. Node thread keeps an event loop
and whenever any task get completed, it fires the corresponding event
which signals the event listener function to get executed.

 

Node.js uses events heavily and it is also one of the reasons why
Node.js is pretty fast compared to other similar technologies. As soon
as Node starts its server, it simply initiates its variables, delcares
functions and then simply waits for event to occur. In an event-driven
application, there is generally a main loop that listens for events, and
then triggers a callback function when one of those events is detected.

 

![](media/image2.png){width="6.0in" height="2.34375in"}

While Events seems similar to what callbacks are. The difference lies in
the fact that callback functions are called when an asynchronous
function returns its result where as event handling works on the
observer pattern. The functions which listens to events acts as
Observers. Whenever an event gets fired, its listener function starts
executing. Node.js has multiple in-built events available through events
module and EventEmitter class which is used to bind events and event
listeners

 

// Import events module\
var events = require('events');

// Create an eventEmitter object\
var eventEmitter = new events.EventEmitter();

Following is the syntax to bind event handler with an event:

// Bind event and even handler as follows\
eventEmitter.on('eventName', eventHandler);

We can fire an event programatically as follows:

// Fire an event\
eventEmitter.emit('eventName');

 

***How Node Applications Work***

 

In Node Application, any async function accepts a callback as a last
parameter and the callback function accepts error as a first parameter

 

Many objects in Node emit events for example a net.Server emits an event
each time a peer connects to it, a fs.readStream emits an event when the
file is opened. All objects which emit events are instances of
**events.EventEmitter**

 

***EventEmitter Class***

 

As we have seen in previous section, EventEmitter class lies
in **events** module. It is accessibly via following syntax:

// Import events module\
var events = require('events');\
// Create an eventEmitter object\
var eventEmitter = new events.EventEmitter();

When an EventEmitter instance faces any error, it emits an 'error'
event. When new listener is added, 'newListener' event is fired and when
a listener is removed, 'removeListener' event is fired. EventEmitter
provides multiple properties like **on** and **emit**. **on** property
is used to bind a function with the event and **emit** is used to fire
an event.

 

Methods

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **S.N.**   **method & Description**
  ---------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  1          **addListener(event, listener)**
             
             Adds a listener to the end of the listeners array for the specified event. No checks are made to see if the listener has already been added. Multiple calls passing the same combination of event and listener will result in the listener being added multiple times. Returns emitter, so calls can be chained.

  2          **on(event, listener)**
             
             Adds a listener to the end of the listeners array for the specified event. No checks are made to see if the listener has already been added. Multiple calls passing the same combination of event and listener will result in the listener being added multiple times. Returns emitter, so calls can be chained.

  3          **once(event, listener)**
             
             Adds a one time listener for the event. This listener is invoked only the next time the event is fired, after which it is removed. Returns emitter, so calls can be chained.

  4          **removeListener(event, listener)**
             
             Remove a listener from the listener array for the specified event. Caution: changes array indices in the listener array behind the listener. removeListener will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified event, then removeListener must be called multiple times to remove each instance. Returns emitter, so calls can be chained.

  5          **removeAllListeners(\[event\])**
             
             Removes all listeners, or those of the specified event. It's not a good idea to remove listeners that were added elsewhere in the code, especially when it's on an emitter that you didn't create (e.g. sockets or file streams). Returns emitter, so calls can be chained.

  6          **setMaxListeners(n)**
             
             By default EventEmitters will print a warning if more than 10 listeners are added for a particular event. This is a useful default which helps finding memory leaks. Obviously not all Emitters should be limited to 10. This function allows that to be increased. Set to zero for unlimited.

  7          **listeners(event)**
             
             Returns an array of listeners for the specified event.

  8          **emit(event, \[arg1\], \[arg2\], \[...\])**
             
             Execute each of the listeners in order with the supplied arguments. Returns true if event had listeners, false otherwise.
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

Class Methods

  --------------------------------------------------------------
  **S.N.**   **method & Description**
  ---------- ---------------------------------------------------
  1          **listenerCount(emitter, event)**
             
             Return the number of listeners for a given event.
  --------------------------------------------------------------

Events

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **S.No.**   **Events & Description**
  ----------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  1           **newListener**
              
              -   **event** - String The event name
              
              -   **listener** - Function The event handler function
              
              This event is emitted any time a listener is added. When this event is triggered, the listener may not yet have been added to the array of listeners for the event.

  2           **removeListener**
              
              -   **event** - String The event name
              
              -   **listener** - Function The event handler function
              
              This event is emitted any time someone removes a listener. When this event is triggered, the listener may not yet have been removed from the array of listeners for the event.
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

**Both on and addListener are aliases for the same function.**

 

From
&lt;<http://stackoverflow.com/questions/8281979/in-node-js-whats-on>&gt;

 

 

 

***NodeJS Buffer***

 

Pure JavaScript is Unicode friendly but not nice to binary data. When
dealing with TCP streams or the file system, it's necessary to handle
octet streams. Node provides Buffer class which provides instances to
store raw data similar to an array of integers but corresponds to a raw
memory allocation outside the V8 heap.

Buffer class is a global class and can be accessed in application
without importing buffer module.

 

Node Buffer can be constructed in a variety of ways.

 

Method 1

Following is the syntax to create an uninitiated Buffer of 10 octets:

 

var buf = new Buffer(10);

Method 2

Following is the syntax to create a Buffer from a given array:

 

var buf = new Buffer(\[10, 20, 30, 40, 50\]);

Method 3

Following is the syntax to create a Buffer from a given string and
optionally encoding type:

 

var buf = new Buffer("Simply Easy Learning", "utf-8");

Though "utf8" is the default encoding but you can use either of the
encodings "ascii", "utf8", "utf16le", "ucs2", "base64" or "hex".

 

**Writing to Buffers**

 

buf.write(string\[, offset\]\[, length\]\[, encoding\])

*Parameters*

Here is the description of the parameters used:

-   **string** - This is string data to be written to buffer.

-   **offset** - This is the index of the buffer to start writing at.
    > Default value is 0.

-   **length** - This is the number of bytes to write. Defaults to
    > buffer.length

-   **encoding** - Encoding to use. 'utf8' is the default encoding

Return Value

This method returns number of octets written. If there is not enough
space in the buffer to fit the entire string, it will write a part of
the string.

 

buf = new Buffer(256);\
len = buf.write("Simply Easy Learning");

 

 

**Reading from Buffers**

 

 

buf.toString(\[encoding\]\[, start\]\[, end\])

*Parameters*

Here is the description of the parameters used:

-   **encoding** - Encoding to use. 'utf8' is the default encoding

-   **start** - Beginning index to start reading, defaults to 0.

-   **end** - End index to end reading, defaults is complete buffer.

Return Value

This method decodes and returns a string from buffer data encoded using
the specified character set encoding.

 

buf = new Buffer(26);\
for (var i = 0 ; i &lt; 26 ; i++) {\
buf\[i\] = i + 97;\
}

console.log( buf.toString('ascii')); // outputs:
abcdefghijklmnopqrstuvwxyz\
console.log( buf.toString('ascii',0,5)); // outputs: abcde\
console.log( buf.toString('utf8',0,5)); // outputs: abcde\
console.log( buf.toString(undefined,0,5)); // encoding defaults to
'utf8', outputs abcde

 

-   Following is the syntax of the method to convert a Node Buffer into
    > JSON object:

> buf.toJSON()
>
>  

-   Following is the syntax of the method to concatenate Node buffers to
    > a single Node Buffer

> Buffer.concat(list\[, totalLength\])
>
>  

-   buf.compare(otherBuffer);

-   buf.copy(targetBuffer\[, targetStart\]\[,
    > sourceStart\]\[, sourceEnd\])

-   buf.slice(\[start\]\[, end\])

-   buf.length;

 

***Streams***

 

Streams are objects that let you read data from a source or write data
to a destination in continous fashion. In Node.js, there are four types
of streams.

-   **Readable** - Stream which is used for read operation.

-   **Writable** - Stream which is used for write operation.

-   **Duplex** - Stream which can be used for both read and
    > write operation.

-   **Transform** - A type of duplex stream where the output is computed
    > based on input.

Each type of Stream is an **EventEmitter** instance and throws several
events at different instance of times. For example, some of the commonly
used events are:

-   **data** - This event is fired when there is data is available
    > to read.

-   **end** - This event is fired when there is no more data to read.

-   **error** - This event is fired when there is any error receiving or
    > writing data.

-   **finish** - This event is fired when all data has been flushed to
    > underlying system

 

 

> fs.readFile will load the entire file into memory as you pointed out,
> while as fs.createReadStreamwill read the file in chunks of the size
> you specify.
>
> The client will also start receiving data faster
> using fs.createReadStream as it is sent out in chunks as it is being
> read, while as fs.readFile will read the entire file out and only then
> start sending it to the client. This might be negligible, but can make
> a difference if the file is very big and the disks are slow.
>
> Think about this though, if you run these two functions on a 100MB
> file, the first one will use 100MB memory to load up the file while as
> the latter would only use at most 4KB.

 

 

***Piping streams***

 

Piping is a mechanism where we provide output of one stream as the input
to another stream. It is normally used to get data from one stream and
to pass output of that stream to another stream. There is no limit on
piping operations

 

 

***Chaining streams***

 

Chanining is a mechanism to connect output of one stream to another
stream and create a chain of multiple stream operations. It is normally
used with piping operations

 

***Node.js - File System***

 

Node implements File I/O using simple wrappers around standard POSIX
functions. Every method in fs module have synchronous as well as
asynchronous form. Asynchronous methods takes a last parameter as
completion function callback and first parameter of the callback
function is error. It is preferred to use asynchronous method instead of
synchronous method as former never block the program execution where as
the second one does.

 

Following is the syntax of the method to open a file in asynchronous
mode:

fs.open(path, flags\[, mode\], callback)

**Parameters**

Here is the description of the parameters used:

-   **path** - This is string having file name including path.

-   **flags** - Flag tells the behavior of the file to be opened. All
    > possible values have been mentioned below.

-   **mode** - This sets the file mode (permission and sticky bits), but
    > only if the file was created. It defaults to 0666, readable
    > and writeable.

-   **callback** - This is the callback function which gets two
    > arguments (err, fd).

Flags

Flags for read/write operations are:

  **Flag**   **Description**
  ---------- -------------------------------------------------------------------------------------------------------------------------------
  r          Open file for reading. An exception occurs if the file does not exist.
  r+         Open file for reading and writing. An exception occurs if the file does not exist.
  rs         Open file for reading in synchronous mode.
  rs+        Open file for reading and writing, telling the OS to open it synchronously. See notes for 'rs' about using this with caution.
  w          Open file for writing. The file is created (if it does not exist) or truncated (if it exists).
  wx         Like 'w' but fails if path exists.
  w+         Open file for reading and writing. The file is created (if it does not exist) or truncated (if it exists).
  wx+        Like 'w+' but fails if path exists.
  a          Open file for appending. The file is created if it does not exist.
  ax         Like 'a' but fails if path exists.
  a+         Open file for reading and appending. The file is created if it does not exist.
  ax+        Like 'a+' but fails if path exists.

 

 

Following is the syntax of the method to get the information about a
file:

fs.stat(path, callback)

**Parameters**

Here is the description of the parameters used:

-   **path** - This is string having file name including path.

-   **callback** - This is the callback function which gets two
    > arguments (err, stats) where **stats** is an object of fs.Stats
    > type

 

there are number of useful methods available in **fs.Stats** class which
can be used to check file type. These methods are given in the following
table.

  **Method**                  **Description**
  --------------------------- --------------------------------------------------
  stats.isFile()              Returns true if file type of a simple file.
  stats.isDirectory()         Returns true if file type of a directory.
  stats.isBlockDevice()       Returns true if file type of a block device.
  stats.isCharacterDevice()   Returns true if file type of a character device.
  stats.isSymbolicLink()      Returns true if file type of a symbolic link.
  stats.isFIFO()              Returns true if file type of a FIFO.
  stats.isSocket()            Returns true if file type of asocket.

 

Following is the syntax of one of the methods to write into a file:

fs.writeFile(filename, data\[, options\], callback)

This method will over-write the file if file already exists. If you want
to write into an existing file then you should use another method
available.

Parameters

Here is the description of the parameters used:

-   **path** - This is string having file name including path.

-   **data** - This is the String or Buffer to be written into the file.

-   **options** - The third parameter is an object which will hold
    > {encoding, mode, flag}. By default encoding is utf8, mode is octal
    > value 0666 and flag is 'w'

-   **callback** - This is the callback function which gets a single
    > parameter err and used to to return error in case of any
    > writing error.

 

Following is the syntax of one of the methods to read from a file:

fs.read(fd, buffer, offset, length, position, callback)

This method will use file descriptor to read the file, if you want to
read file using file name directly then you should use another method
available.

Parameters

Here is the description of the parameters used:

-   **fd** - This is the file descriptor returned by file fs.open()
    > method.

-   **buffer** - This is the buffer that the data will be written to.

-   **offset** - This is the offset in the buffer to start writing at.

-   **length** - This is an integer specifying the number of bytes
    > to read.

-   **position** - This is an integer specifying where to begin reading
    > from in the file. If position is null, data will be read from the
    > current file position.

-   **callback** - This is the callback function which gets the three
    > arguments, (err, bytesRead, buffer).

 

Following is the syntax of one of the methods to close an opened file:

fs.close(fd, callback)

**Parameters**

Here is the description of the parameters used:

-   **fd** - This is the file descriptor returned by file fs.open()
    > method.

-   **callback** - This is the callback function which gets no arguments
    > other than a possible exception are given to the
    > completion callback.

 

Following is the syntax of the method to delete a file:

fs.unlink(path, callback)

**Parameters**

Here is the description of the parameters used:

-   **path** - This is the file name including path.

-   **callback** - This is the callback function which gets no arguments
    > other than a possible exception are given to the
    > completion callback.

 

***Global Objects***

 

Node.js global objects are global in nature and they are available in
all modules. We do not need to include these objects in our application,
rather we can use them directly. These objects are modules, functions,
strings and object itself

 

\_\_filename

The **\_\_filename** represents the filename of the code being executed.
This is the resolved absolute path of this code file. For a main program
this is not necessarily the same filename used in the command line. The
value inside a module is the path to that module file.

 

\_\_dirname

The **\_\_dirname** represents the name of the directory that the
currently executing script resides in.

 

setTimeout(cb, ms)

The **setTimeout(cb, ms)** global function is used to run callback cb
after at least ms milliseconds. The actual delay depends on external
factors like OS timer granularity and system load. A timer cannot span
more than 24.8 days.

This function returns an opaque value that represents the timer which
can be used to clear the timer

 

 

setInterval(cb, ms)

The **setInterval(cb, ms)** global function is used to run callback cb
repeatedly after at least ms milliseconds. The actual delay depends on
external factors like OS timer granularity and system load. A timer
cannot span more than 24.8 days.

This function returns an opaque value that represents the timer which
can be used to clear the timer using the function **clearInterval(t)**.

 

  ----------------------------------------------------------------------------------------------------------------
  **S.N.**   **Module Name & Description**
  ---------- -----------------------------------------------------------------------------------------------------
  1          [**Console**](http://www.tutorialspoint.com/nodejs/nodejs_console.htm)
             
             Used to print information on stdout and stderr.

  2          [**Process**](http://www.tutorialspoint.com/nodejs/nodejs_process.htm)
             
             Used to get information on current process. Provides multiple events related to process activities.
  ----------------------------------------------------------------------------------------------------------------

 

 

There are number of utility modules available in Node.js module library.
These modules are very common and are frequently used while developing
any Node based applications.

  --------------------------------------------------------------------------------------------------------------------------------------
  **S.N.**   **Module Name & Description**
  ---------- ---------------------------------------------------------------------------------------------------------------------------
  1          [**OS Module**](http://www.tutorialspoint.com/nodejs/nodejs_os_module.htm)
             
             Provides basic operating-system related utility functions.

  2          [**Path Module**](http://www.tutorialspoint.com/nodejs/nodejs_path_module.htm)
             
             Provides utilities for handling and transforming file paths.

  3          [**Net Module**](http://www.tutorialspoint.com/nodejs/nodejs_net_module.htm)
             
             Provides both servers and clients as streams. Acts as a network wrapper.

  4          [**DNS Module**](http://www.tutorialspoint.com/nodejs/nodejs_dns_module.htm)
             
             Provides functions to do actual DNS lookup as well as to use underlying operating system name resolution functionalities.

  5          [**Domain Module**](http://www.tutorialspoint.com/nodejs/nodejs_domain_module.htm)
             
             Provides way to handle multiple different I/O operations as a single group.
  --------------------------------------------------------------------------------------------------------------------------------------

 

 

***Creating Web Server using Node***

 

Node.js provides http module which can be used to create either HTTP
client of server.

 

***Express Overview***

 

Express is a minimal and flexible Node.js web application framework that
provides a robust set of features to develop web and mobile
applications. It facilitates a rapid development of Node based Web
applications. Following are some of the core features of Express
framework:

 

Allows to set up middlewares to respond to HTTP Requests. Defines a
routing table which is used to perform different action based on HTTP
Method and URL. Allows to dynamically render HTML Pages based on passing
arguments to templates.

 

npm install express --save

Above command saves installation locally in **node\_modules** directory
and creates a directory express inside node\_modules. There are
following important modules which you should install along with express:

-   **body-parser** - This is a node.js middleware for handling JSON,
    > Raw, Text and URL encoded form data.

-   **cookie-parser** - Parse Cookie header and populate req.cookies
    > with an object keyed by the cookie names.

-   **multer** - This is a node.js middleware for
    > handling multipart/form-data.

 

 

1\) What is Express.js?

[Express.js](https://en.wikipedia.org/wiki/Express.js) is
a [Node.js](http://en.wikipedia.org/wiki/Node.js) framework. It's the
most popular framework as of now (the most starred on NPM).

.

It's built around configuration and granular simplicity of Connect
middleware. Some people compare Express.js to [Ruby
Sinatra](http://en.wikipedia.org/wiki/Sinatra_%28software%29) vs. the
bulky and opinionated [Ruby on
Rails](http://en.wikipedia.org/wiki/Ruby_on_Rails).

2\) What is the purpose of it with Node.js?

That you don't have to repeat same code over and over again. Node.js is
a low-level [I/O](http://en.wikipedia.org/wiki/Input/output) mechanism
which has an HTTP module. If you just use an HTTP module, a lot of work
like parsing the payload, cookies, storing sessions (in memory or
in [Redis](http://en.wikipedia.org/wiki/Redis_%28data_store%29)),
selecting the right route pattern based on [regular
expressions](http://en.wikipedia.org/wiki/Regular_expression) will **have** to
be re-implemented. With Express.js it there for you to use.

3\) Why do we actually need Express.js? How it is useful for us to use
with Node.js?

The first answer should answer your question. If no, then try to write a
small [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) API
server in plain Node.js (that is, using only core modules) and then in
Express.js. The latter will take you 5-10x less time and lines of code.

What is Redis? Does it come with Express.js?

Redis is a fast persistent key-value storage. You can optionally use it
for storing sessions with Express.js, but you don't need to. By default,
Express.js has memory storage for sessions. Redis also can be use for
queueing jobs, for example, email jobs.

Check out [my tutorial on REST API server with
Express.js](http://www.webapplog.com/intro-to-express-js-simple-rest-api-app-with-monk-and-mongodb/).

MVC but not by itself

Express.js is **not** an model-view-controller framework by itself. You
need to bring your own object-relationa mapping in to the stack. Library
such as Mongoose for MongoDB, Sequelize
([http://sequelizejs.com](http://sequelizejs.com/)) for SQL databases,
Waterline (<https://github.com/balderdashy/waterline>) for many
databases.

Alternatives

Other Node.js frameworks to consider
(<https://www.quora.com/Node-js/Which-Node-js-framework-is-best-for-building-a-RESTful-API>):

 

From
&lt;<http://stackoverflow.com/questions/12616153/what-is-express-js>&gt;

 

 

Routing refers to determining how an application responds to a client
request to a particular endpoint, which is a URI (or path) and a
specific HTTP request method (GET, POST, and so on).

 

Express provides a built-in middleware **express.static** to serve
static files, such as images, CSS, JavaScript etc.

You simply needs to pass the name of the directory where you keep your
static assets, to the **express.static** middleware to start serving the
files directly. For example, if you keep your images, CSS, and
JavaScript files in a directory named public, you can do this:

app.use(express.static('public'));

 

 

***REST***

 

REST stands for REpresentational State Transfer. REST is web standards
based architecture and uses HTTP Protocol. It revolves around resource
where every component is a resource and a resource is accessed by a
common interface using HTTP standard methods. A REST Server simply
provides access to resources and REST client accesses and modifies the
resources using HTTP protocol. Here each resource is identified by URIs/
global IDs. REST uses various representation to represent a resource
like text, JSON, XML but JSON is the most popular one

 

A web service is a collection of open protocols and standards used for
exchanging data between applications or systems. Software applications
written in various programming languages and running on various
platforms can use web services to exchange data over computer networks
like the Internet in a manner similar to inter-process communication on
a single computer. This interoperability (e.g., communication between
Java and Python, or Windows and Linux applications) is due to the use of
open standards. Web services based on REST Architecture are known as
RESTful web services. These webservices uses HTTP methods to implement
the concept of REST architecture. A RESTful web service usually defines
a URI, Uniform Resource Identifier a service, which provides resource
representation such as JSON and set of HTTP Methods.

 

***Scaling***

 

As Node.js runs in a single thread mode but it uses an event-driven
paradigm to handle concurrency. It also facilitates creation of child
processes to leverage parallel processing on multi-core cpu based
systems.

Child processes always have three
streams **child.stdin**, **child.stdout**, and**child.stderr** which may
be shared with the stdio streams of the parent process.

Node provides **child\_process** module which has following three major
ways to create child process.

-   **exec** - child\_process.exec method runs a command in a
    > shell/console and buffers the output.

-   **spawn** - child\_process.spawn launches a new process with a given
    > command

-   **fork** - The child\_process.fork method is a special case of
    > the spawn() to create child processes.

 

child\_process.exec method runs a command in a shell and buffers the
output.

 

 

 

 

 

Nodejs

Tuesday, April 26, 2016

19:56

 

> Node is single-threaded and uses a concurrency model based on an event
> loop. It is non-blocking, so it doesn't make the program wait, but
> instead it registers a callback and lets the program continue. This
> means it can handle concurrent operations without multiple threads of
> execution, so it can scale pretty well.
>
>  
>
> Node is ideal for I/O bound applications (or those that wait on user
> events), but not so great for CPU-heavy applications. Good examples
> include data-intensive realtime applications (DIRT), single page
> applications, JSON APIs, and data-streaming applications.
>
> Node owes a big part of its success to npm, the package manager that
> comes bundled with it. There are a lot of great things about npm:

-   It installs application dependencies locally, not globally.

-   It handles multiple versions of the same module at the same time.

-   You can specify tarballs or git repositories as dependencies.

-   It's really easy to publish your own module to the npm registry.

-   It's useful for creating CLI utilities that others can
    > install (with npm) and use right away

>  
>
> Java or Python use the import function to load other libraries, while
> PHP and Ruby use require. Node implements the CommonJS interface for
> modules. In Node you can also load other depencies using the
> **require** keyword.
>
> We can also require relative files:
>
> var myFile = require('./myFile'); // loads myFile.js
>
>  
>
> The nice thing about requiring Node modules is that they aren't
> automatically injected into the global scope, but instead you just
> assigned them to a variable of your choice. That means that you don't
> have to care about two or more modules that have functions with the
> same name.
>
>  
>
> When creating your own modules, all you have to do is take care when
> exporting something (wheather it's a function, an object, a number or
> so on). The first approach would be to export a single object. The
> second approach requires adding properties to the exports object. A
> thing to note about modules is that they don't share scope, so if you
> want to share a variable between different modules, you must include
> it into a separate module that is then required by the other modules.
> Another interesting thing you should remember is that modules are only
> loaded once, and after that they are cached by Node.
>
> Callbacks
>
> In asynchronous programming we do not return values when our functions
> are done, but instead we use the continuation-passing style (CPS).
> With this style, an asynchronous function invokes a callback (a
> function usually passed as the last argument) to continue the program
> once the it has finished.
>
>  
>
> In functional programming, continuation-passing style (CPS) is a style
> of programming in which control is passed explicitly in the form of a
> continuation. This is contrasted with direct style, which is the usual
> style of programming. A function written in continuation-passing style
> takes an extra argument: an explicit "continuation" i.e. a function of
> one argument. When the CPS function has computed its result value, it
> "returns" it by calling the continuation function with this value as
> the argument. That means that when invoking a CPS function, the
> calling function is required to supply a procedure to be invoked with
> the subroutine's "return" value. Expressing code in this form makes a
> number of things explicit which are implicit in direct style. These
> include: procedure returns, which become apparent as calls to a
> continuation; intermediate values, which are all given names; order of
> argument evaluation, which is made explicit; and tail calls, which
> simply call a procedure with the same continuation, unmodified, that
> was passed to the caller. The key to CPS is to remember that (a) every
> function takes an extra argument, its continuation, and (b) every
> argument in a function call must be either a variable or a lambda
> expression (not a more complex expression). This has the effect of
> turning expressions "inside-out" because the innermost parts of the
> expression must be evaluated first, so CPS explicates the order of
> evaluation as well as the control flow
>
>  
>
> Programming with continuations can also be useful when a caller does
> not want to wait until the callee completes. For example, in
> user-interface (UI) programming, a routine can set up dialog box
> fields and pass these, along with a continuation function, to the UI
> framework. This call returns right away, allowing the application code
> to continue while the user interacts with the dialog box. Once the
> user presses the "OK" button, the framework calls the continuation
> function with the updated fields. Although this style of coding uses
> continuations, it is not full CPS.
>
>  
>
>  
>
> var dns = require('dns');
>
> dns.resolve4('www.google.com', function (err, addresses) {
>
> if (err)
>
> throw err;
>
> console.log('addresses: ' + JSON.stringify(addresses));
>
> });
>
>  
>
> We have passed a callback (the inline anonymous function) as the
> second argument to the dns.resolve4 asynchronous function. Once the
> async function has the response ready for us it will invoke the
> callback, thus continuing the program execution. This is how we make
> use of CPS.
>
>  
>
> Events
>
>  
>
> The standard callback pattern works well for the use cases where we
> want to be notified when the async function finishes. However, there
> are situations that require being notified of different events that do
> not occur at the same time. The **EventEmitter** pattern allows
> implementors to emit an event to which the consumers can subscribe if
> they are interested. Node has an EventEmitter class in core which we
> can use to make our own EventEmitter objects
>
>  
>
> Streams
>
>  
>
> Streams represent an abstract interface for asynchronously
> manipulating a continuous flow of data. They are similar to Unix pipes
> and can be classified into five types: readable, writable, transform,
> duplex and "classic". As with Unix pipes, Node streams implement a
> composition operator called .pipe(). The main benefits of using
> streams are that you don't have to buffer the whole data into memory
> and they're easily composable.
>
>  
>
>  
>
> var crypto = require('crypto');
>
> var fs = require('fs');
>
> var zlib = require('zlib');
>
>  
>
> var password = new Buffer(process.env.PASS || 'password');
>
> var encryptStream = crypto.createCipher('aes-256-cbc', password);
>
>  
>
> var gzip = zlib.createGzip();
>
> var readStream = fs.createReadStream(\*\*filename); // current file
>
> var writeStream = fs.createWriteStream(\*\*dirname + '/out.gz');
>
>  
>
> readStream // reads current file
>
> .pipe(encryptStream) // encrypts
>
> .pipe(gzip) // compresses
>
> .pipe(writeStream) // writes to out file
>
> .on('finish', function () { // all done
>
> console.log('done');
>
> });
>
>  
>
> Here we take a readable stream, pipe it into an encryption stream,
> then pipe that into a gzip compression stream and finally pipe it into
> a write stream (writing the content to disk). The encryption and
> compression streams are transform streams, which
>
>  
>
>  
>
> Error Handling
>
> The "error-first" callback is a standard protocol for Node callbacks.
> It originated in Node core, but it has spread into userland as well to
> become today's standard. This is a very simple convention, with
> basically one rule: the first argument for the callback function
> should be the error object.
>
> That means that there are two possible scenarios:

-   If the error argument is null, then the operation was successful.

-   If the error argument is set, then an error occured and you need to
    > handle it.

>  
>
>  
>
> fs.readFile('/foo.txt', function(err, data) {
>
> // …
>
> });
>
>  
>
>  
>
> EventEmitter errors
>
>  
>
> We have to be careful when dealing with event emitters (that means
> streams too), because if there's an unhandled error event it will
> crash our application. Depending on your application this might be a
> fatal error (unrecoverable) or an error that should not crash your
> application (like failed sending an email for example). Either way you
> should attach an error event handler:
>
>  
>
>  
>
> emitter.on('error', function(err) {
>
> console.error('something went wrong with the ee:' + err.message);
>
> });
>
>  
>
>  
>
> With **verror**, we can wrap our errors to provide more descriptive
> messages. We will have to require the module at the beginning of the
> file and then wrap the error when invoking the callback
>
>  
>
> Debugging
>
>  
>
> For small bugs you can always use *console.log* to track down one
> thing or another, but for more complex situations
> there's [node-inspector](https://github.com/node-inspector/node-inspector).
> node-inspector is installable via npm. It has a lot of goodies baked
> in, but the most important are:
>
>  
>
>  

-   It's based on the Blink Developer Tools, so it should look and feel
    > familiar to frontend developers.

-   It has the ability to setup breakpoints.

-   We can step over, step in, step out, resume (continue).

-   We can inspect scopes, variables, object properties.

-   Besides inspecting, we can also edit variables and
    > object properties.

>  
>
>  
>
> \# basically \`node-debug\` instead of \`node\`
>
> \$ node-debug example.js
>
>  
>
> Express and Socket.io
>
> Express is the most popular web framework for Node, while Socket.IO is
> a realtime framework that enables bi-directional communication between
> web clients and the server.
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

 

 

Basics

Tuesday, April 26, 2016

20:31

 

To start a Node.js script from a file, simply run \$ node filename,
e.g., \$ node program.js. If all we need is a quick set of statements,
there’s a -e option that allow to run inline JavaScript/Node.js,
e.g., \$ node -e "console.log(new Date());"

 

As you know from [JS FUNdamentals](http://webapplog.com/), browser
JavaScript by default puts everything into its global scope. Node.js was
designed to behave differently with everything being local by default.
In case we need to access globals, there is a global object. Likewise,
when we need to export something, we should do so explicitly. In a
sense, window object from front-end/browser JavaScript metamorphosed
into a combination of global and process objects. Needless to say, the
document object that represent DOM of the webpage is nonexistent in
Node.js.

 

Another bad part in browser JavaScript is that there’s no way to include
modules. Scripts are supposed to be linked together using a different
language (HTML) with a lacking dependency management. CommonJS and
RequireJS solve this problem with AJAX-y approach. Node.js borrowed many
things from the CommonJS concept. However, sometime it’s more fitting to
invoke a constructor, e.g., when we attach properties to Express.js app

 

***Buffer*** is a Node.js addition to four primitives (boolean, string,
number and RegExp) and all-encompassing objects (array and functions are
also objects) in front-end JavaScript. We can think of buffers as
extremely efficient data stores. In fact, Node.js will try to use
buffers any time it can, e.g., reading from file system, receiving
packets over the network

 

***\_\_dirname vs. process.cwd***

 

\_\_dirname is an absolute path to the file in which this global
variable was called, while process.cwd is an absolute path to the
process that runs this script. The latter might not be the same as the
former if we started the program from a different folder.

 

 

 

 

 

 

Streams

Tuesday, April 26, 2016

20:38

 

In node, the built-in stream module is used by the core libraries and
can also be used by user-space modules. Similar to unix, the node stream
module's primary composition operator is called .pipe() and you get a
backpressure mechanism for free to throttle writes for slow consumers.

 

I/O in node is asynchronous, so interacting with the disk and network
involves passing callbacks to functions.RaedFile works but it's bulky
and buffers up the entire data.txt file into memory for every request
before writing the result back to clients. If data.txt is very large,
your program could start eating a lot of memory as it serves lots of
users concurrently, particularly for users on slow connections. The user
experience is poor too because users will need to wait for the whole
file to be buffered into memory on your server before they can start
receiving any contents.

 

Luckily both of the (req, res) arguments are streams, which means we can
write this in a much better way using fs.createReadStream() instead of
fs.readFile():

 

var http = require('http');\
var fs = require('fs');

var server = http.createServer(function (req, res) {\
var stream = fs.createReadStream(\_\_dirname + '/data.txt');\
stream.pipe(res);\
});\
server.listen(8000);

 

 

Here .pipe() takes care of listening for 'data' and 'end' events from
the fs.createReadStream(). This code is not only cleaner, but now the
data.txt file will be written to clients one chunk at a time immediately
as they are received from the disk. Using .pipe() has other benefits
too, like handling backpressure automatically so that node won't buffer
chunks into memory needlessly when the remote client is on a really slow
or high-latency connection.

 

There are 5 kinds of streams: readable, writable, transform, duplex, and
"classic".

 

.pipe() is just a function that takes a readable source stream src and
hooks the output to a destination writable streamdst:

src.pipe(dst)

.pipe(dst) returns dst so that you can chain together
multiple .pipe() calls together:

a.pipe(b).pipe(c).pipe(d)

which is the same as:

a.pipe(b);\
b.pipe(c);\
c.pipe(d);

 

 

Readable streams produce data that can be fed into a writable,
transform, or duplex stream by calling .pipe():

 

var Readable = require('stream').Readable;

var rs = new Readable;\
rs.push('beep ');\
rs.push('boop\\n');\
rs.push(null);

rs.pipe(process.stdout);

\$ node read0.js\
beep boop

 

it would be even better in many circumstances if we could avoid
buffering data altogether and only generate the data when the consumer
asks for it. We can push chunks on-demand by defining a .\_read
function:

 

var Readable = require('stream').Readable;\
var rs = Readable();

var c = 97;\
rs.\_read = function () {\
rs.push(String.fromCharCode(c++));\
if (c &gt; 'z'.charCodeAt(0)) rs.push(null);\
};

rs.pipe(process.stdout);

 

 

Here we push the letters 'a' through 'z', inclusive, but only when the
consumer is ready to read them. The \_read function will also get a
provisional size parameter as its first argument that specifies how many
bytes the consumer wants to read, but your readable stream can ignore
the size if it wants.

 

**consuming a readable stream**

Most of the time it's much easier to just pipe a readable stream into
another kind of stream or a stream created with a module
like [through](https://npmjs.org/package/through) or [concat-stream](https://npmjs.org/package/concat-stream),
but occasionally it might be useful to consume a readable stream
directly.

process.stdin.on('readable', function () {\
var buf = process.stdin.read();\
console.dir(buf);\
});

\$ (echo abc; sleep 1; echo def; sleep 1; echo ghi) | node consume0.js\
&lt;Buffer 61 62 63 0a&gt;\
&lt;Buffer 64 65 66 0a&gt;\
&lt;Buffer 67 68 69 0a&gt;\
null

When data is available, the 'readable' event fires and you can
call .read() to fetch some data from the buffer. When the stream is
finished, .read() returns null because there are no more bytes to fetch.

 

A writable stream is a stream you can .pipe() to but not from:

 

 

Transform streams are a certain type of duplex stream (both readable and
writable). The distinction is that in Transform streams, the output is
in some way calculated from the input.

You might also hear transform streams referred to as "through streams".
Through streams are simple readable/writable filters that transform
input and produce output.

 

Duplex streams are readable/writable and both ends of the stream engage
in a two-way interaction, sending back and forth messages like a
telephone. An rpc exchange is a good example of a duplex stream. Any
time you see something like:

a.pipe(b).pipe(a)

you're probably dealing with a duplex stream.

 

Classic streams are the old interface that first appeared in node 0.4.
You will probably encounter this style of stream for a long time so it's
good to know how they work. Whenever a stream has a "data" listener
registered, it switches into "classic" mode and behaves according to the
old API.

 

 

***built-in streams***

**process.stdin** : This readable stream contains the standard system
input stream for your program. It is paused by default but the first
time you refer to it .resume() will be called implicitly on the next
tick.

 

**process.stdout** : This writable stream contains the standard system
output stream for your program.

 

**process.stderr**: This writable stream contains the standard system
error stream for your program.

 

**net.connect()** : This function returns a \[duplex stream\] that
connects over tcp to a remote host.You can start writing to the stream
right away and the writes will be buffered until the 'connect' event
fires.

 

**Request - Simplified HTTP client: **

 

Request is designed to be the simplest way possible to make http calls.
It supports HTTPS and follows redirects by default

var request = require('request');\
request('http://www.google.com', function (error, response, body) {\
if (!error && response.statusCode == 200) {\
console.log(body) // Show the HTML for the Google homepage.\
}\
})

 

You can stream any response to a file stream.

request('http://google.com/doodle.png').pipe(fs.createWriteStream('doodle.png'))

You can also stream a file to a PUT or POST request. This method will
also check the file extension against a mapping of file extensions to
content-types (in this case application/json) and use the
proper content-type in the PUT request (if the headers don’t already
provide one).

fs.createReadStream('file.json').pipe(request.put('http://mysite.com/obj.json'))

Request can also pipe to itself. When doing
so, content-type and content-length are preserved in the PUT headers.

request.get('http://google.com/img.png').pipe(request.put('http://mysite.com/img.png'))

Request emits a "response" event when a response is received.
The response argument will be an instance
of[http.IncomingMessage](http://nodejs.org/api/http.html#http_http_incomingmessage).

 

request\
.get('http://google.com/img.png')\
.on('response', function(response) {\
console.log(response.statusCode) // 200\
console.log(response.headers\['content-type'\]) // 'image/png'\
})\
.pipe(request.put('http://mysite.com/img.png'))

 

To easily handle errors when streaming requests, listen to
the error event before piping:

request\
.get('http://mysite.com/doodle.png')\
.on('error', function(err) {\
console.log(err)\
})\
.pipe(fs.createWriteStream('doodle.png'))

 

 

request supports application/x-www-form-urlencoded and multipart/form-data form
uploads.

 

 

**Oppressor :**streaming http compression response negotiator

 

**response-stream** :Pass http server response methods through to the
next destination pipe.

 

 

 

 

 

Art of Node

Wednesday, May 04, 2016

14:19

 

Node has a small core group of modules (commonly referred to as 'node
core') that are presented as the public API that you are intended to
write programs with. For working with file systems there is the fs
module and for networks there are modules like net (TCP), http, dgram
(UDP). In addition to fs and network modules there are a number of other
base modules in node core. There is a module for asynchronously
resolving DNS queries called dns, a module for getting OS specific
information like the tmpdir location called os, a module for allocating
binary chunks of memory called buffer, some modules for parsing urls and
paths (url, querystring, path), etc. Most if not all of the modules in
node core are there to support node's main use case: writing fast
programs that talk to file systems or networks

 

**Callbacks**

Callbacks are functions that are executed asynchronously, or at a later
time. Instead of the code reading top to bottom procedurally, async
programs may execute different functions at different times based on the
order and speed that earlier functions like http requests or file system
reads happen.

 

var fs = require('fs') // require is a special function provided by
node\
var myNumber = undefined // we don't know what the number is yet since
it is stored in a file

function addOne() {\
fs.readFile('number.txt', function doneReading(err, fileContents) {\
myNumber = parseInt(fileContents)\
myNumber++\
})\
}

addOne()

console.log(myNumber) // logs out undefined -- this line gets run before
readFile is done

 

When we run this program all of the functions are immediately defined,
but they don't all execute immediately. This is a fundamental thing to
understand about async programming. When addOne is called it kicks off a
readFile and then moves on to the next thing that is ready to execute.
When readFile is done reading the file (this may take anywhere from
milliseconds to seconds to minutes depending on how fast the hard drive
is) it will run the doneReading function and give it an error (if there
was an error) and the file contents. The reason we got undefined above
is that nowhere in our code exists logic that tells the console.log
statement to wait until the readFile statement finishes before it prints
out the number.

 

The key to understanding callbacks is to realize that they are used when
you don't know when some async operation will complete, but you do know
where the operation will complete — the last line of the async function!
The top-to-bottom order that you declare callbacks does not necessarily
matter, only the logical/hierarchical nesting of them. First you split
your code up into functions, and then use callbacks to declare if one
function depends on another function finishing

 

 

var fs = require('fs')\
var myNumber = undefined

function addOne(callback) {\
fs.readFile('number.txt', function doneReading(err, fileContents) {\
myNumber = parseInt(fileContents)\
myNumber++\
callback()\
})\
}

function logMyNumber() {\
console.log(myNumber)\
}

addOne(logMyNumber)

 

From &lt;<https://github.com/maxogden/art-of-node/#the-art-of-node>&gt;

 

Now the logMyNumber function can get passed in as an argument that will
become the callback variable inside the addOne function. After readFile
is done the callback variable will be invoked (callback()). Only
functions can be invoked, so if you pass in anything other than a
function it will cause an error.

 

 

To break down this example even more, here is a timeline of events that
happen when we run this program:

-   1: The code is parsed, which means if there are any syntax errors
    > they would make the program break. During this initial
    > phase, fs and myNumber are declared as variables
    > while addOne and logMyNumber are declared as functions. Note that
    > these are just declarations. Neither function has been called nor
    > invoked yet.

-   2: When the last line of our program gets executed addOne is invoked
    > with the logMyNumber function passed as itscallback argument.
    > Invoking addOne will first run
    > the asynchronous fs.readFile function. This part of the program
    > takes a while to finish.

-   3: With nothing to do, node idles for a bit as it waits
    > for readFile to finish. If there was anything else to do during
    > this time, node would be available for work.

-   4: As soon as readFile finishes it executes its
    > callback, doneReading, which parses fileContents for an integer
    > calledmyNumber, increments myNumber and then immediately invokes
    > the function that addOne passed in (its callback),logMyNumber.

 

Node first dispatches the readFile operation and then waits for readFile
to send it an event that it has completed. While it is waiting node can
go check on other things. Inside node there is a list of things that are
dispatched but haven't reported back yet, so node loops over the list
again and again checking to see if they are finished. After they
finished they get 'processed', e.g. any callbacks that depended on them
finishing will get invoked.

 

Imagine you had 3 async functions a, b and c. Each one takes 1 minute to
run and after it finishes it calls a callback (that gets passed in the
first argument). If you wanted to tell node 'start running a, then run b
after a finishes, and then run c after b finishes' it would look like
this:

a(function() {\
b(function() {\
c()\
})\
})

 

When this code gets executed, a will immediately start running, then a
minute later it will finish and call b, then a minute later it will
finish and call c and finally 3 minutes later node will stop running
since there would be nothing more to do. There are definitely more
elegant ways to write the above example, but the point is that if you
have code that has to wait for some other async code to finish then you
express that dependency by putting your code in functions that get
passed around as callbacks.

 

If you were to turn this into pseudocode you would end up with this:

 

var file = readFile()

processFile(file)

This kind of linear (step-by-step, in order) code isn't the way that
node works. If this code were to get executed then readFile and
processFile would both get executed at the same exact time. This doesn't
make sense since readFile will take a while to complete. Instead you
need to express that processFile depends on readFile finishing. This is
exactly what callbacks are for! And because of the way that JavaScript
works you can write this dependency many different ways:

 

var fs = require('fs')

fs.readFile('movie.mp4', function finishedReading(error, movieData) {\
if (error) return console.error(error)\
// do something with the movieData\
})

 

 

**Events**

Events are a common pattern in programming, known more widely as the
'observer pattern' or 'pub/sub' (publish/subscribe). Whereas callbacks
are a one-to-one relationship between the thing waiting for the callback
and the thing calling the callback, events are the same exact pattern
except with a many-to-many API. This approach is similar to the
pure-callback approach but introduces the .on method, which subscribes a
callback to an event.

 

**Streams**

The whole point of node is to make it easy to deal with file systems and
networks so it made sense to have one pattern that was used everywhere.

 

**Modules**

Node core is made up of about two dozen modules, some lower level ones
like events and stream some higher level ones like http and crypto. This
design is intentional. Node core is supposed to be small, and the
modules in core should be focused on providing tools for working with
common I/O protocols and formats in a way that is cross-platform. For
everything else there is npm. Anyone can create a new node module that
adds some functionality and publish it to npm.

 

**Modular development workflow**

. They just split your environment up in to many virtual environments,
one for each project, but inside each environment dependencies are still
globally installed. With npm installing global modules is an
anti-pattern. Just like how you shouldn't use global variables in your
JavaScript programs you also shouldn't install global modules (unless
you need a module with an executable binary to show up in your global
PATH

 

When you call require('some\_module') in node here is what happens:

1.  if a file called some\_module.js exists in the current folder node
    > will load that, otherwise:

2.  node looks in the current folder for a node\_modules folder with
    > a some\_module folder in it

3.  if it doesn't find it, it will go up one folder and repeat step 2

This cycle repeats until node reaches the root folder of the filesystem,
at which point it will then check any global module folders
(e.g. /usr/local/node\_modules on Mac OS) and if it still doesn't
find some\_module it will throw an exception.

 

One of the benefits of npm's approach is that modules can install their
dependent modules at specific known working versions.

 

A module can list any other modules from npm or GitHub in the
dependencies field of package.json. To install the request module as a
new dependency and automatically add it to package.json run this from
your module root directory:

 

npm install --save request

This installs a copy of request into the closest node\_modules folder
and makes our package.json look something like this:

 

{

"id": "number-one",

"version": "1.0.0",

"dependencies": {

"request": "\~2.22.0"

}

}

By default npm install will grab the latest published version of a
module.

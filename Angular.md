 

Tuesday, August 04, 2015

11:25

 

AngularJS is a JavaScript framework. It can be added to an HTML page
with a &lt;script&gt; tag. AngularJS extends HTML attributes
with Directives, and binds data to HTML with Expressions.

 

The markup fetched from the server is meaningless on its own without
Angular parsing it and you need to have a client that supports
JavaScript. Thus, search engines need to work extra in order to get a
full representation of the data--**so for now it's not a good idea to
use angular if you're building a website that relies on search engines
to function. So if you're building a web application, admin website or
single-page website then you've chosen a great tool to do the job.**

 

Angular works by separating application logic from data on the
client-side and structuring a client-side web application with use of
directives, filters, bindings and binding-specific operations.
Controllers, Services and Models are used to glue all the logic and data
operations together.

 

Just like any MVC architecture, URL paths are routed to controllers and
the parameters are available within the controller method. It also
reduces the amount of code required for handling DOM bindings with data
and HTML elements.

 

**Modules** are used to fully encapsulate all the angular code of your
application into one entry point. Modules are used so that your
application (as well as discrete parts of your application) can be
separated into distinct parts which can be loaded and executed in
different order. So you could have a directives module which can be set
to run just before the ui module is run, thus ensuring that your
resulting application DOM is in proper shape for your ui code to run.

 

 

**ng-model**

ng-model or data-ng-model directive in AngularJS is one of the greatest
strength to bind the variables used in application with input
components. This works as two way data binding. If you want to
understand better about the two way bindings, you have an input
component and the value updated into that field must be reflected in
other part of the application. The better solution is to bind a variable
to that field and output that variable whereever you wish to display the
updated value throughoput the application.

**ng-bind**

ng-bind works much different than ng-model. ng-bind is one way data
binding used for displaying the value inside html component as inner
HTML. This directive can not be used for binding with the variable but
only with the HTML elements content. Infact this can be used along with
ng-model to bind the component to HTML elements. This directive is very
useful for updating the blocks like div, span, etc. with inner HTML
content

 

From
&lt;<http://stackoverflow.com/questions/12419619/whats-the-difference-between-ng-model-and-ng-bind>&gt;

 

 

 

Tuesday, August 04, 2015

11:32

 

var App = angular.module('YOUR\_APP\_NAME', \['ngResource'\]);

 

This will create a global module for your app where you can create
routes, models, filters and directives. The App variable is accessible
throughout your application and the \['ngResource'\] definition array
defines all the other modules and dependencies that must be loaded prior
to this module being activated. In this case ngResource is an additional
module that defines functionality for creating resources (models) in
angular

 

Any additional models can be defined using the same syntax, but you must
define the module name as a different name as any other module that has
been defined. If you create another module with the same name then it
may not active (or the previous module may not activate instead). If you
wish to make a new module activate after the main application module
then just define the new module and set the name of the application
module as a dependency

 

Angular comes with expressions which are apart of its general markup for
HTML and are bound to the scope variable which is where the data binding
takes place. This involves data binding, two-way data binding,
conditionals, for in and foreach loops, model binding and so on.

 

The beauty about this approach is that (as you can see) the data (the
Model) is 100% detached from the markup (the View) and the data itself
can be retrieved and cached from an external source while being handled
and tweaked by a logical controller (the Controller). Hence we have an
awesome MVC framework

 

Dependency Injection (DI) is, in angular, method of organizing how
components, modules and variables are loaded to various parts of your
angular app. All of your components within your app are to be injected
into your controllers, module configuraitons, directives, filters,
resources and routes.

 

//the controller definition

var Ctrl = function(\$scope, \$http, \$location) {

//now you can use any of the injected variables

//to change the URL after something has happened then you can use
\$location

\$location.path('/path/to/new/page');

}

//and now the injection of the variables

Ctrl.\$inject = \['\$scope','\$http','\$location'\];

 

The benefit to DI is that you can totally isolate all of your services,
controllers, resources, directives, filters into their own contained
environments with no global variables. This makes testing much easier.
It also facilitates ordering between code blocks so that once a
particular dependency has been injected then it is guaranteed to be
there for use within the next code block.

 

**Routes** are used to map which path matches are linked to which
controller. When you access a URL (by clicking on a link or putting in
the URL), angular will first check to see if its defined and, if not,
then it will delegate the event to a standard webpage view (access the
html page normally) or do nothing (if it was a hashbang URL). You should
be able to create routes anywhere in your app code-

 

App.config(\['\$routeProvider', function(\$routes) {

 

\$route.when('/',{

templateUrl : '/templates/home.html',

controller : HomeCtrl

});

\$route.when('/register',{

templateUrl : '/templates/register.html',

controller : RegisterCtrl

});

 

\$routes.otherwise({

redirectTo : '/'

});

}\]);

 

 

 

 

Tuesday, August 04, 2015

11:40

**Controllers** are where the logic of your application happens.
Plugins, Widgets and DOM-specific code shouldn't be included here since
that stuff is meant for directives. First, start by setting up the
controller (each controller function is basically the action itself).
The **\$scope** is specific to where the controller is hooked into
within your webpage. And any properties set for the \$scope variable
will then evaluate within your webpage

 

***\$rootScope***

All \$scope data is inherited off the \$rootScope variable, so if you
want to share reusable code across all your \$scope objects in all your
controllers then you can do it by setting properties of the \$rootScope
variable.

 

 

Finally, there are two ways to register a controller to the application:

 

Include the Controller within your application HTML

A controller can be set using an angular directive within a HTML tag.

 

&lt;div data-ng-controller="SomeCtrl"&gt;...&lt;/div&gt;

 

Assign a Controller to be apart of a route

You can also define a route and specify the controller that handles the
request:

 

\$routes.when('/some/path',{

controller : Ctrl,

templateUrl : '/templates/controller.html'

});

 

 

 

 

 

 

 

 

 

Tuesday, August 04, 2015

11:43

 

***Services***

 

Angular Services is an amazing approach to abstracting shared code and
functionality across your application. It ties directly into the
dependency injection feature that angular provides and can be used
directly apart of the module object.

 

<http://blog.pluralsight.com/angularjs-step-by-step-services> :
**Excellent explanation of services in angularjs**

 

In my previous post about AngularJS controllers, I spoke a bit about the
need for separation of concerns in modern-day JavaScript applications,
which are much more involved than those of a decade ago. With the amount
of JavaScript needed in a modern-day application, the architecture of
your JavaScript takes on much more importance. Two of the five SOLID
principles of object oriented design are directly related to Services:
the Single Responsibility Principle (SRP) and the Dependency Inversion
Principle (DIP).

 

The single responsibility principle teaches that every object should
have a single responsibility. If we use the example of a controller,
it’s responsibility is essentially to wire up the scope (which holds
your models) to your view; it is essentially the bridge between your
models and your views. If your controller is also responsible for making
ajax calls to fetch and update data, this is a violation of the SRP
principle. Logic like that (and other business logic) should instead be
abstracted out into a separate service, then injected into the objects
that need to use it.

 

This is where the Dependency Inversion Principle comes in. The DIP
states that objects should depend on abstractions, not concretions. In
languages like C\# and Java, this means your objects depend on
Interfaces instead of Classes. In JavaScript you could look at any
parameter of any function (constructor function or otherwise) as an
abstraction, since you can pass in any object for that parameter so long
as it has the members on it that are used within that method. But the
key here is the ability to use dependency injection — the ability to
inject into other objects. This means that all of your controllers,
directives, filters and other services should take in any external
dependencies as parameters during construction. This allows you to have
loosely coupled code and has the added benefit of making unit testing
much easier.

 

Creating a custom service

Let’s start with this fiddle which is where we ended in my last post.
Notice that in the controller we are setting \$scope.users1 to a static
array of users. Let’s change it so it’s accessed via an ajax call. But,
of course, this shouldn’t be a responsibility of our Controller, so
let’s create a service to handle it, and our controller will call the
service.

 

To create the service, we use the module’s factory method. Add this code
to the bottom of the JavaScript in the fiddle:

 

myModule.factory('userRepository', function() {

return { };

});

With this code, we are creating a new service named userRepository.
Notice that the first parameter of the factory method is the name we
want to give to our service, and also notice that the second parameter
of the factory method is a function. The object returned by that
function represents our service. In this case we are simply returning an
empty object literal, so our service does nothing. So this begs the
question: if we simply return the object that is to be our service, why
do we need all the other ceremony of myModule.factory? By using the
factory method we are registering our service with Angular. This allows
Angular’s dependency injection container to inject an instance of our
service when we request it in other places. I’ll demonstrate this
shortly when we use this service in our controller.

 

For now, let’s just let our service expose our static array of users.
Update that return statement to look like this:

 

return {

getAllUsers: function() {

return \[

{ firstName: 'Jane', lastName: 'Doe', age: 29 },

{ firstName: 'John', lastName: 'Doe', age: 32 }

\];

}

};

Notice that we are now returning an object with a getAllUsers() function
on it. This function returns our array. Your fiddle should now look
something like this. So now, we can call userRepository.getAllUsers() in
order to get our array of users. Let’s look at how we’d do that in our
controller.

 

Using your custom services

Handling dependency injection is something that AngularJS does very
well. It’s incredibly simple, yet very effective. The first thing you
have to do is register your service with Angular which we just
demonstrated above. Now all you have to do to use it is inject it. But
before we do that, let’s remove the hard-coded users array that’s in our
controller. That way you can see that the page is currently not working.
Remove the “\$scope.users = …” line from your controller, and you’ll
notice that the data disappears from the page. Now inject our new custom
service by adding it as a parameter where we’re already injecting
\$scope. Change the first line of your controller definition to look
like this:

 

myModule.controller('myController', function(\$scope, userRepository) {

That’s it. Angular will now take care of creating a userRepository for
you to use in your controller. Now let’s use our repository. Add this
line inside the controller:

 

\$scope.users = userRepository.getAllUsers();

Your fiddle should now look something like this. And now take a look at
the output, we now have our users showing up on our page again, only
this time, the data is coming from our service. Congratulations! You
just created and used your first custom service.

 

 

 

 

Tuesday, August 04, 2015

11:59

 

**Models**

 

**Excellent tutorial:**
<http://www.webdeveasy.com/angularjs-data-model/>

 

Models are used the same way that models are used just as a model is
used in Rails or any other MVC framework. They're also defined in the
same manner as angular services are as well as injected into the
application. All regular getter and setter operations for model
properties exist and all RESTful operations are defined and access the
server backend to do their storage operations. Your server-side
application needs to be coded to handle each of the REST operations for
each model (POST create, GET show, GET index, PUT/PATCH update, DELETE
destroy).

 

Here's how you define a model in angular:

 

View Code

App.factory('ModelName', \['\$resource', function(\$resource) {

\$resource.url('/path/to/model/controller/:id',{

id : '@id', //this binds the ID of the model to the URL param

},{

query : { method : 'GET', isArray : true }, //this can also be called
index or all

save : { method : 'PUT' }, //this is the update method

create : { method : 'POST' },

destroy : { method : 'DELETE' }

}

}\]);

This will create a model called ModelName with the REST actions query,
show, save, create, destroy all targeted towards the
/path/to/model/controller/:id. The :id param is only used for get, save
and destroy REST calls. When an :id value isn't present then it will not
be used in the URL and angular will strip and trailing slashes and
whitespace from the URL so effectively you'll end up having a URL such
as /path/to/model/controller for REST calls such as query and create
(which is how REST expect for them to be). All of the actions defined
can be called directly from the model, but in order to have access to
the model as a variable you must include it as a dependency injection:

 

View Code

var SomeCtrl = function(\$scope, \$http, \$location, ModelName) {

//now you can use ModelName to do your business

};

SomeCtrl.\$inject = \['\$scope','\$http','\$location','ModelName'\];

Once you have access to the model you can call all the actions that you
have defined in your resource definition as well as as a few others.
Here are some examples:

 

View Code

//list all the records on the page

var results = ModelName.query({ search : 'all' }, onSuccessFn,
onFailureFn);

 

//get a specific record

var record = ModelName.get({ id : 123 }, onSuccessFn, onFailureFn);
//onSuccessFn and onFailureFn are optional callback functions where you
can further customize the response

 

//create a new ModelName record

var record = new ModelName();

 

//update that record

record.someAttr = 'someValue';

record.\$save();

 

//or if you prefer to submit your data in a different way

ModelName.save({

id : record.id

},{

somePostObject : {

attr1 : 'value',

attr2 : 'value2'

}

});

 

//destroy the record (and include a token)

record.destroy({ token : record.token });

 

 

 

Tuesday, August 04, 2015

12:05

 

**Directives**

 

**Excellent tutorial:**
<http://www.sitepoint.com/practical-guide-angularjs-directives/>

 

Angular directives are tiny behavioral hooks that link your HTML to your
plugins and to any isolated blocks of code within your application.
They're designed not to change the logic of the controllers or models,
but to aid in the construction of the webpage. Therefore, they're
perfect for plugins, validations, dynamic text properties (such as
internationalization-related and localization-related tweaks).

 

First define the directive within your application javascript:

 

View Code

angular.directive('myDirective',function(\$compile) {

return {

templateUrl : '/path/to/some/template.html', //(optional) the contents
of this template can be downloaded and constructed into the element

replace : true, //whether or not to replace the inner data within the
element

link : function(\$scope, \$element, attributes) { //this is where your
magic happens

\$scope.title = '...';

}

};

});

Now when angular comes a HTML tag that contains data-my-directive as an
attribute (with or without a value) then it will download the template
and execute the link function. You can also define the template html
directly and you can also create your own compile function which does
all the work in one go. The \$scope variable provided within the link
function is the scope variable of the controller that contains the
directive. This is a powerful way to share data between the controller
and the directive as well as for them to communicate between each other.

 

 

 

 

 

Tuesday, August 04, 2015

12:12

**Filters**

 

Filters are reusable operations that can be embedded directly into
binding operations to tweak the data in some way. Some examples would
include pagination, language-tweaking, role and session-specific data
filtering.

 

View Code

App.filter('myUppercase', function(data) {

for(var i=0; i &lt; data.length; i++) {

data\[i\].title = data\[i\].title.toUpperCase();

}

return data;

});

This filter then can be used within an angular expression:

 

View Code

&lt;div data-ng-repeat="for record in records |
filter:myUppercase"&gt;...&lt;/div&gt;

Or it can be used directly within your JavaScript code with the \$filter
function.

 

View Code

//be sure to inject the \$filter object

var values = \['one','two','three'\];

values = \$filter('myUppercase')(values);

 

 

 

Tuesday, August 04, 2015

12:12

 

**HTML5 Mode**

 

HTML5 Mode allows for your angular app to use HTML5 history within its
routing system and then gracefully degrade its functionality to hashbang
support if the browser doesn't support HTML5 history. The following
snippet of code enables HTML5 history within your angular application
(it's disabled by default).

 

View Code

App.config(\['\$locationProvider', function(\$location) {

\$location.html5Mode(true); //now there won't be a hashbang within URLs
for browers that support HTML5 history

}\]);

 

***changes in the \$scope and digest***

 

AngularJS handles **changes in the \$scope** with a poll and watch
approach but it's not exactly what you expect polling to be whenever a
major event occurs within the application, and then, once the event
occurs, a digest operation is issued and the scope is updated. The
AngularJS \$scope variable acts as a big key/value storage hash which is
internally looped on a timeout interval and dirty checked against it's
former value(s) each time a digestion occurs. If there is a change with
the value compared to it's former value, then AngularJS fires off a
change event and renders the necessary DOM handles to make that DOM
binding render based on the value of that variable. These major events
that AngularJS pays attention to are user input events (mouse, keyboard,
etc...), any kind of important browser events (timeout, blur, etc...),
and when any data returned is returned from the server (\$http calls,
template downloads, etc...). This is why whenever something happens
outside of the AngularJS code (a third party plugin does something, or
when the URL is manually changed) a direct call to the \$scope.\$apply()
must be made to inform AngularJS to recognize that change (all of this
is explained in more detail later on).

 

The nice thing about all this is that AngularJS isn't greedy and only
runs when it has to, so if your webpage is idling as a background tab
then, unless you have implemented something to loop in the background,
then AngularJS should not fire off any digest calls.

 

<http://stackoverflow.com/questions/9682092/databinding-in-angularjs/9693933#9693933>

 

 

 

 

 

 

Tuesday, August 04, 2015

12:34

***Root Scope and Extending Scope Members***

 

The \$rootScope acts as the parent scope object of all other \$scope
objects. This means that when a controller is is executed then the
\$scope variable that is provided to it will have it's contents
linked/cloned from the \$rootScope object. It's best just to think the
\$scope variable as a child class of the \$rootScope (\$scope extends
\$rootScope). Undestanding this is useful for when you want to have
special methods attached to your scope variable for use across your
entire application (such as session information, flags, states, etc...).

 

The following example below is an example of how you can attach
different libraries or code objects to your \$scope instance.

 

App.run(\['\$rootScope',function(\$rootScope) {

//this will be available to all scope variables

\$rootScope.includeLibraries = true;

//this method will be available to all scope variables as well

\$rootScope.include = function(libraries) {

var scope = this;

//attach each of the libraries directly to the scope variable

for(var i=0;i&lt;libraries.length;i++) {

var key = libraries\[i\];

scope\[key\] = getLibrary(key);

}

return scope;

};

}\]);

And then inside of your controller or directive you can do the
following.

 

StackOverflow View Codevar Ctrl = function(\$scope) {

if(\$scope.includeLibraries) { //the flag was set in the \$rootScope
object

\$scope = \$scope.include(\['plugin1', 'library1'\]);

}

};

Ctrl.\$inject = \['\$scope'\];

 

Try not to set too much data into the \$scope and \$rootScope variables.
Afterall, AngularJS deals with \$scope data very very often and you
wouldn't want to overwhelm it ;)

 

 

 

Tuesday, August 04, 2015

13:44

The **data-ng-init** attribute is useful for pre-setting values. The
syntax works like you would be setting values in JavaScript directly
(since it uses eval to evaluate the text within the attribute value).

 

**Catching Errors**

 

Catching errors is something that is important for a production
application. Below are various approaches do doing so:

 

Catchall Route (otherwise)

Despite this being a useful method as a default page for a route, it's
best to reserve this route as your 404 page handler in the event that a
route is not recognized within your application.

 

\$routeProvider.when('/404',{

controller : ErrorCtrl

});

\$routeProvider.otherwise({

redirectTo : '/404'

});

When your routes fail

In the event that a route change fails (due to a missing templateUrl or
something) then you can capture the event within your scope by doing the
following:

 

App.run(\['\$rootScope','\$location',function(\$rootScope, \$location) {

\$rootScope.\$on("\$routeChangeError", function (event, current,
previous, rejection) {

//change this code to handle the error somehow

\$location.path('/404').replace();

});

}\]);

Wrap Services Around your HTTP Requests

Earlier in the article I explained the importance of custom services for
code reuse. When you set a custom service to wrap all your AJAX calls
then you can catch errors before they're passed onto other parts of your
application.

 

App.factory('myHttp',\['\$http','\$location',function(\$http,
\$location) {

 

var onEmpty = function() {

window.location = '/404';

};

return function() {

get : function(url, success, fail) {

\$http.get(url).success(function(response) {

var data = response.data;

if(!data) {

onEmpty();

return;

}

success();

}).error(onEmpty);

}

};

}\]);

 

Be sure to only use this method when you access resources and data that
is required within your application (like JSON data for a specific
view).

 

 

 

Tuesday, August 04, 2015

12:37

 

Each time a major event occurs in a web application that is angular is
running (when a webpage is first loaded, when new AJAX request is
recieved, URL changes, etc...) Angular picks up the change and then
prepares a digestion (which is the internal loop which is run on the
\$scope memeber). This only takes a few milliseconds, but angular only
runs this process once at a time. You can manually kickstart this
process by running the \$scope.\$apply() method (this is useful for
triggering updaets when 3rd party applications do something with your
webpage that angular needs to know about). Also if you set your own
bindings and run the \$scope.\$apply() method then an exception may be
thrown which may cause your code to stop (this happens when an existing
digestion is going on in the background). So you will need to aware when
a digestion is going on by checking the \$\$phase variable (this is
explained below). The \$apply method runs the \$diest() method which is
an internal method which triggers angular to poll all it's \$watch
methods. To get around the \$apply exception you will need to pay
attention to the \$scope.\$\$phase flag to see if a digestion phase is
going on in the background. If a phase is going on then you can just set
the \$scope values directly and they should get picked up by the current
digestion. In the event that you wish to change the URL of the webpage,
then you will have to also pay attention to the \$\$phase variable to
see if you're "allowed" to change the URL. If a digestion phase is going
on then you can just fallback to changing the URL the old fashion way
using window.location.

 

**Communication Between Services and Controllers**

 

Whenever you have an event take place in your application which affects
all controllers and directives it's best to use the \$emit, \$on and
\$broadcast methods provided by AngularJS. Examples of this include
permissions and session changes (like when a user logs out or when a
flag is raised).

When you need to have a parent controller or scope instruct all child
controllers about a change then you can use the \$broadcast method.

 

 

**You should be using Custom Services**

 

Custom services are what make angular very manageable and easily
testable. By using angular's dependency injection feature you can create
a custom service anywhere within your application and include it
elsewhere very easily. A common example of where a shared service makes
sense is to use it as a special \$http service which is tailored to fit
your application.

 

 

 

Tuesday, August 04, 2015

13:48

**How Promises Work**

 

Promises are basically vertical callbacks without the need for nested
functions. This is useful for when one part of the program needs to run
after something else but is situated in a different area of your
application. Examples would include running a permissions HTTP GET
operation after checking to see that the user's session is still active
(this could be another HTTP call). To get this to work without the use
of promises would be a coding nightmare (lots of callbacks and useless
coding fluff).

 

AngularJS promises work effectively to get around this by use of the \$q
service. They're inspired by Kris Kowall's Q and work similarly.
Basically, anything that does something that requires a callback is
wrapped into a defer and promise loop and then once that particular
promise is resolved (whether by reject() or resolve()) then the next
defered promise in the queue is dealt with. So long as the promises are
linked with each other (much like the nodes in a queue are linked to
each other) then everything will be loaded one after the other

 

**Includes and Custom HTML Views**

 

Includes (using ngInclude)

If you have an area of your HTML page where you would like to include
another snippet of text then you can do this by using the
data-ng-include attribute.

 

&lt;div data-ng-include
src="/some/path/to/a/template.html"&gt;...&lt;/div&gt;

You can also define it without the custom src attribute and use the
include attribute directly.

 

&lt;!-- this is same as above --&gt;

&lt;div
data-ng-include="/some/path/to/a/template.html"&gt;...&lt;/div&gt;

The above line will get loaded right away when angular parses the HTML.
So to get this to load when you have data available then do this:

 

&lt;div data-ng-show="someVariable"
data-ng-include="someVariable"&gt;...&lt;/div&gt;

And setup the \$scope.someVariable variable to a value when you're ready
to display the include.

 

Once the include has been downloaded and is ready then the
\$scope.\$on('\$includeContentLoaded'); will be emitted. Also if you
include an onload attribute within the same element then that attribute
will also be evaluated once the include is ready.

 

 

 

 

 

Concepts

Wednesday, August 12, 2015

14:59

 

-   Angular use plain old JavaScript Objects for synchronising Model and
    > View data-bindings, which makes updating both a breeze. Angular
    > parses back to JSON and communicates best with a REST endpoint

>  

-   Dependency injection: In AngularJS, we cleverly use the arguments of
    > a function to declare the dependencies we want, and Angular gives
    > them to us. 

>  

-   AngularJS (as well as other JavaScript frameworks) manage state
    > entirely in the browser and communicate changes when we want them
    > to via Ajax (HTTP) using GET, POST, PUT and DELETE methods,
    > typically talking to a REST endpoint backend. 

>  

-   In "older" applications where the server typically managed state,
    > there were disconnections between data the user was seeing and
    > data synchronized on the server.

>  

-   Think of \$scope as an automated bridge between JavaScript and the
    > DOM itself which holds our synchronised data

>  

-    Once Angular starts rendering your application, it creates
    > a \$rootScope Object, and all further bindings and logic in your
    > application create new \$scope Objects which then all become
    > children of the \$rootScope.

>  

-   An Angular Controller allows us to interact with a View and Model,
    > it's the place where presentational logic can take place to keep
    > the UI bindings in sync with the Model. A Controller's purpose is
    > to drive Model and View changes, in Angular it's a meeting place
    > between our business logic and our presentational logic.

>  

-   A Controller accepts two arguments, the first the Controller's name,
    > to be referenced elsewhere such as the DOM, and the second a
    > callback function. This callback shouldn't be treated as a
    > callback, however, it's more a declaration of the Controller's
    > body

 

-   All the Controller does is talk to a Service, and pass the data in
    > either the same or a different format across to our View,
    > using the \$scope Object. Once a View is updated, the Controller
    > logic is also updated and can be passed back to the server using
    > a Service.

 

-   The Angular team introduced this as part of the
    > new controllerAs syntax, of which a Controller becomes
    > instantiated as an instance under a variable - much like you could
    > using the new keyword against a variable to create a new Object.

 

-   It's important to remember that all Services are application
    > singletons, there is only one instance of a Service per injector.
    > By convention all custom Services should follow Pascal Case like
    > our Controllers, for example "my service" would be "MyService"

 

-   Angular gives us a service method for creating a new Object with,
    > this could talk to a backend or provide utilities to handle
    > business logic. A service is just a constructorObject that gets
    > called with the new keyword, which means we'll be using
    > the thiskeyword to bind our logic to the Service.
    > The service creates a singleton Object created by a service
    > factory

 

-   A Service means we can't run any code before it as all methods are
    > the Object instantiated. Things are different when it comes to
    > a Factory.

 

-   Factory methods return an Object or a Function, which means we can
    > make usage of closures as well as returning a host Object to bind
    > methods to

 

-   Instead of manipulating the DOM “directly,” you annotate your DOM
    > with metadata (directives), and Angular manipulates the DOM
    > for you.

 

-   A \$scope is an object that ties a view (a DOM element) to
    > the controller. In the Model-View-Controller structure, this
    > \$scope object becomes the model. Although it sounds complex, the
    > \$scope is just a JavaScript object. Both the controller and the
    > view have access to the \$scope so it can be used for
    > communication between the two.

 

-   All scopes are created with prototypal inheritance, meaning that
    > they have access to their parent scopes. By default, for any
    > property that AngularJS cannot find on a local scope, AngularJS
    > will crawl up to the containing (parent) scope and look for the
    > property or method there. If AngularJS can’t find the property
    > there, it will walk to that scope’s parent and so on and so forth
    > until it reaches the \$rootScope

>  

-   Some directives can optionally create an isolate scope and do not
    > inherit from their parents.

 

-   \$watch functions run (if necessary) in the AngularJS event loop
    > (the \$digest loop), and the Angular updates the DOM accordingly

>  

-   The double-curly expression directive registers a listener for the
    > expression inside the {{ expression }} using the \$watch()
    > function. This function enables Angular to update the view.

>  

-   The ng-init directive is a function that runs at bootstrap time
    > (before runtime). It allows us to set default variables prior to
    > running any other functions during runtime

>  

-   The ng-click directive registers a listener with the DOM element.
    > When the DOM listener fires (when a button or link is clicked),
    > Angular executes the expression and updates the view as normal:

>  

-   Directives, in AngularJS are, at their core functions that get run
    > when the DOM is compiled by the compiler.

>  

-   Services are singletons, which are objects that are instantiated
    > only once per app (by the \$injector)

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

 

 

Angular JS

Monday, February 08, 2016

14:13

 

> **Controller prototype**
>
> Scope-based vs object-oriented controllers in Angular
>
> It used to be that the AngularJS controllers shared state with the DOM
> (the view layer) via \$scope object. The view could access any
> property and call any method on the \$scope

  ----------------------------------------------
  1   &lt;div ng-controller="MyController"&gt;
      
  2   Hello {{ name }}! or {{ greeting() }}
      
  3   &lt;/div&gt;
  --- ------------------------------------------
  ----------------------------------------------

> The application code to initialize the controller (separate function
> for clarity)

  ------------------------------------------------
  1   function myController(\$scope) {
      
  2   \$scope.name = 'World';
      
  3   \$scope.greeting = function greeting() {
      
  4   return 'Hello ' + \$scope.name + '!';
      
  5   };
      
  6   }
      
  7   angular.module('Example', \[\])
      
  8   .controller('MyController', myController);
  --- --------------------------------------------
  ------------------------------------------------

> Each instance of the \$scope object was created behind the scenes by
> the AngularJS. Each scope instance had its own copy of the
> property name (good) and its own copy of function greeting (bad, waste
> of space).
>
> Fortunately, we can easily refactor this code to still keep separate
> data (the name property), but reuse single method greetingamong all
> instances. We do this by binding a common function greeting to
> the \$scope object inside the controller.

  ------------------------------------------------
  1   function greeting() {
      
  2   return 'Hello ' + this.name + '!';
      
  3   }
      
  4   function myController(\$scope) {
      
  5   \$scope.name = 'World';
      
  6   \$scope.greeting = greeting.bind(\$scope);
      
  7   }
      
  8   angular.module('Example', \[\])
      
  9   .controller('MyController', myController);
  --- --------------------------------------------
  ------------------------------------------------

> I prefer [not using .bind in
> Angular](https://glebbahmutov.com/blog/why-function-bind-matters-little-in-angular/),
> but in this case I don't mind it too much. Yet, there is a second
> problem with using \$scopeobjects to tie the data from the model to
> the view. The \$scope is too heavy! If you print a \$scope to the
> console inside the controller it has lots of stuff
>
> \$\$ChildScope: null\
> \$\$childHead: null\
> \$\$childTail: null\
> \$\$listenerCount: Object\
> \$\$listeners: Object\
> \$\$nextSibling: null\
> \$\$prevSibling: ChildScope\
> \$\$watchers: Array\[2\]\
> \$\$watchersCount: 2\
> \$id: 4\
> \$parent: Scope\
> greeting: ()\
> name: "Func"\
> \_\_proto\_\_: Scope
>
> If we inspect its prototype object, we will find even more properties
>
> \$\$ChildScope: ChildScope()\
> \$\$applyAsyncQueue: Array\[0\]\
> \$\$asyncQueue: Array\[0\]\
> \$\$childHead: ChildScope\
> \$\$childTail: ChildScope\
> \$\$destroyed: false\
> \$\$isolateBindings: null\
> \$\$listenerCount: Object\
> \$\$listeners: Object\
> \$\$nextSibling: null\
> \$\$phase: null\
> \$\$postDigestQueue: Array\[0\]\
> \$\$prevSibling: null\
> \$\$watchers: null\
> \$\$watchersCount: 6\
> \$id: 1\
> \$parent: null\
> \$root: Scope\
> \_\_proto\_\_: Scope
>
> Oh my! It makes no sense to expose *all* scope properties to the view
> (DOM). Why should we allow the view to print the number of watchers?

  1   &lt;div ng-controller="MyController"&gt;{{ \$\$watchersCount }}&lt;/div&gt;
  --- -----------------------------------------------------------------------------

> In AngularJS 1.3 a [new syntax was
> introduced](https://glebbahmutov.com/blog/after-upgrading-to-angular-1.3/) to [separate
> controllers from
> scopes](https://glebbahmutov.com/blog/separate-model-from-view-in-angular/).
>
> Now we can create a controller with a few properties that should be
> accessible from the DOM

  ----------------------------------------------------------------------------------
  1   &lt;div ng-controller="MyController as ctrl" ng-init="ctrl.name = 'App'"&gt;
      
  2   Hello {{ ctrl.name }}!
      
  3   &lt;/div&gt;
  --- ------------------------------------------------------------------------------
  ----------------------------------------------------------------------------------

> Major benefit: we must use ctrl.name in order to access the property,
> minimizing the clashes. We can set the properties that should be
> accessible from the DOM directly on the controller's this instance.

  ----------------------------------------------------------------------------------
  1   &lt;div ng-controller="OOController as ctrl" ng-init="ctrl.name = 'App'"&gt;
      
  2   Hello {{ ctrl.name }}!
      
  3   &lt;/div&gt;
  --- ------------------------------------------------------------------------------
  ----------------------------------------------------------------------------------

>  

  ------------------------------------------------
  1   function OOController() {
      
  2   this.name = 'Object';
      
  3   this.greeting = function greeting() {
      
  4   return 'Hello ' + this.name + '!';
      
  5   };
      
  6   }
      
  7   angular.module('Example', \[\])
      
  8   .controller('OOController', OOController);
  --- --------------------------------------------
  ------------------------------------------------

> Even better, under the hood the AngularJS framework runs the
> controller function as a constructor for the new object.

  -----------------------------------
  1   var ctrl = Object.create({});
      
  2   OOController.call(ctrl);
  --- -------------------------------
  -----------------------------------

> This gives us a perfect opportunity to move all common functions into
> a single place that is already familiar to anyone who programs
> JavaScript - the prototype object

  -------------------------------------------------------------
  1   function OOController() {
      
  2   this.name = 'Object';
      
  3   }
      
  4   OOController.prototype.greeting = function greeting() {
      
  5   return 'Hello ' + this.name + '!';
      
  6   };
      
  7   angular.module('Example', \[\])
      
  8   .controller('OOController', OOController);
  --- ---------------------------------------------------------
  -------------------------------------------------------------

> Notice how cool this code becomes - the OOController is plain
> JavaScript code that can be tested easily!
>
> If you still need \$scope, you can inject it into the controller
> function.

  ------------------------------------------------
  1   function OOController(\$scope) {
      
  2   this.name = 'Object';
      
  3   console.log(\$scope);
      
  4   }
      
  5   angular.module('Example', \[\])
      
  6   .controller('OOController', OOController);
  --- --------------------------------------------
  ------------------------------------------------

> The \$scope object will have lots of properties, linking it to the
> entire scope tree. It will also have \$scope.ctrl property pointing at
> the controller object (which is now a separate object). I personally
> do not like this property, since the MVC model should not have access
> to the View or controller properties directly in my opinion.
>
> We can react to the user events easily. For example we can add a
> button to change the name property on click

  ------------------------------------------------------------------------------------------------------
  1   &lt;div ng-controller="OOController as ctrl" ng-init="ctrl.name = 'App'"&gt;
      
  2   Hello {{ ctrl.name }}! &lt;button ng-click="ctrl.setName('clicked');"&gt;Click me&lt;/button&gt;
      
  3   &lt;/div&gt;
  --- --------------------------------------------------------------------------------------------------
  ------------------------------------------------------------------------------------------------------

>  

  ---------------------------------------------------------------
  1    function OOController() {
       
  2    this.name = 'Object';
       
  3    }
       
  4    OOController.prototype.greeting = function greeting() {
       
  5    return 'Hello ' + this.name + '!';
       
  6    };
       
  7    OOController.prototype.setName = function setName(str) {
       
  8    this.name = str;
       
  9    };
       
  10   angular.module('Example', \[\])
       
  11   .controller('OOController', OOController);
  ---- ----------------------------------------------------------
  ---------------------------------------------------------------

> Whenever the user clicks the button, the controller's name property is
> set, and the digest cycle runs.
>
> I am still thinking how to better compose controllers
> like OOController with \$scope objects (for emitting events on change
> for example, or watching \$scope properties).
>
>  
>
>  
>
> ***Debugging***
>
>  
>
> You've been given an Angular code base. How do you figure out where
> everything is? Where scope variables are coming from? What controller
> does what?
>
> Angular doesn't make it easy, but there are few tips and tricks that
> can make your life easier. Tools like Angular Batarang can help, but
> they're not always installed when you need them. Take some time to
> understand the underlying concepts, and your life will be easier in
> the long run.
>
> Angular Batarang is not a great way to do this kind of work. I would
> not recommend trying it out until you've attempted these techniques...
>
> Here are a few tips that will save you a couple of hours next time you
> are thrown in the deep end of an Angular code base.
>
> Most of these tips require that [debugging
> info](https://docs.angularjs.org/guide/production) be available. If
> they don't work for you, open up the console and
> typeangular.reloadWithDebugInfo();
>
> **What is the scope for this element?**
>
> Almost everything in Angular revolves around
> the [scope](https://docs.angularjs.org/guide/scope). Angular creates a
> scope hierarchy with controllers and directives . Directives can
> sometimes have their own *isolate* scope. Being able to know the value
> of the scope at a given place in our page is valuable to debugging,
> and easy to do. Angular lets you access the scope available to an
> element via the .scopemethod.
>
> An isolate scope is one that is unique to the directive and is not
> affected by anything outside of it (aside from bindings)

-   In Chrome, right click an element in the page you're interested

-   Select inspect element

-   The element is now highlighted in the inspector

-   In the console, enter \$(\$0) to get the element. If not using
    > jQuery, you can use angular.element(\$0)

-   \$(\$0).scope() will return the scope associated with the element.
    > You can see its properties right away.

-   Properties inherited from parent scopes won't show up, but you can
    > still type their name. So even if you don't see a property foo on
    > your scope, you can run \$(\$0).scope().foo and see its value if
    > it is available from a parent.

-   You can look at the properties of the parent
    > scope with\$(\$0).scope().\$parent. You can chain this
    > too:\$(\$0).scope().\$parent.\$parent

-   You can look at the root scope: \$(\$0).scope().\$root

-   If you highlighted a directive with isolate scope, you can look at
    > it with\$(\$0).isolateScope()

-   If you highlighted an element inside of a directive with isolate
    > scope,\$(\$0).scope() will show what is available to it (ie: the
    > isolate scope)

> ![](media/image1.jpg){width="6.0in" height="2.3333333333333335in"}
>
> It can be a bit confusing, but try it out! It can be a lot faster than
> setting breakpoints and inspecting variables. If you're not sure which
> of the above commands to run, just try them all. They're perfectly
> safe, and you'll eventually find the data you're looking for.
>
> For more information on the angular scope, refer to [the angular
> documentation](https://docs.angularjs.org/guide/scope)
>
> **Where does this variable come from?**
>
> Once your Angular application grows in size it can become challenging
> to figure out where variables used in our templates come from. For a
> single directive with isolate scope, it's easy. In a hierarchy of
> controllers and directives, try some of these methods for tracking
> them down:

-   Using the method in the previous section, find the element using the
    > variable and look at its scope.

-   Try to inspect the value: \$(\$0).scope().foo if the property is
    > called foo.

-   If the value is defined, you have your answer, the property came
    > from the controller or directive at that level.

-   Otherwise, go up one level in the DOM, and try again.

-   Repeat until you find it.

> There is one small details that make things more complicated however:
> scope inheritance. A controller up in the hierarchy could be providing
> values available on the child scopes. There's a few ways you can go
> about figuring it out:
>
> You may have noticed elements with a class "ng-scope" when looking
> through the inspector. They represent the elements where new scopes
> got created

-   You can use \$(\$0).scope() directly: the inspector will only show
    > the direct scope's properties, not the ones defined on parents. So
    > you can go up the hierarchy until you see your property listed.

-   Use \$(\$0).scope().hasOwnProperty('foo') to see if the property is
    > set directly on the scope you're looking at, and go up the
    > hierarchy until it returns true.

-   Keep going up until you no longer see your property. Just
    > add .parent() to the element to do it from
    > the console:\$(\$0).parent().scope().hasOwnProperty('foo')

-   Look on the last element where you saw it: your property was defined
    > in a controller or directive defined on that element, or a
    > close parent. It could also be defined in the markup (like in the
    > case of an ng-repeat). You can do this by outputting the element
    > directly in the console.

> ![](media/image2.jpg){width="6.0in" height="1.5833333333333333in"}
>
> Using the above techniques, you'll be able to find at what point in
> the document the property is being set. It's definitely a lot of work,
> but is usually faster than trying to guess, unless you wrote the code
> yourself!
>
> **Why does Prototypal Inheritance matter here?**
>
> Inheritance in JavaScript is different from inheritance in languages
> like Java or C\#. JavaScript uses prototypal inheritance. Accessing a
> value that doesn't exist on a given object gets delegated to one
> higher up in the chain, if available.
>
> Prototypal inheritance is amazingly useful when debugging Angular
> applications (see link below). The techniques above use it to analyze
> scopes to find where values come from. If you've ever had issues
> getting your two-way data bindings to behave the way you expect, the
> culprit may be prototypal inheritance.
>
> There are many tutorials on how inheritance work in JavaScript on the
> net. You may want to
> start [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain).
> A good understanding of these concepts will make your Angular
> experience a lot smoother. It's a good foundation for any JavaScript
> developer.
>
> **What controller handles this section of the page?**
>
> This may seem obvious, but we often forget about it. If you need to
> figure out which controller is responsible for a section of the page,
> just look for the ng-controller attribute in the DOM. If you don't see
> one, go up one level and look again.
>
> If you're like me, you may have trouble finding an attribute in a ton
> of HTML. To find find it, click on an element,
> run \$(\$0).attr('ng-controller'), and if nothing comes up, click on
> its parent (using the bread crumbs).epeat until you get a controller
> name back.
>
> With a big of jQuery magic, we can also find the controller that is
> nearest to our selection in one
> step: \$(\$0).closest('\[ng-controller\]').attr('ng-controller')
>
> ![](media/image3.jpg){width="4.177083333333333in"
> height="1.0104166666666667in"}
>
> **Why don't some elements show up?**
>
> If you use ng-if, ng-switch, or ng-views, you may have wondered why
> your elements didn't show up when searching for them in the inspector.
> Unlike ng-show which shows and hide elements by changing their
> visibility, these directives add and remove their content from the DOM
> completely based on conditions or routes.
>
> Angular leaves a comment, such as &lt;!-- ngIf: isFoo --&gt; where the
> element would have been if isFoo had been true.
>
> If the condition is more complicated, you can use the techniques we
> described earlier to understand why an element isn't being shown. In
> For this example, you would run \$(\$0).scope().isFoo, and you would
> get a falsy value. That's why the element didn't get added to the DOM,
> and was replaced by a comment instead.
>
> The comment will be in the DOM when the element has been added, not
> just when it is absent. Look right below it for an element with the
> same condition. If there isn't one, then you can assume the condition
> was not met.
>
> **How do I see the effects of a value changing?**
>
> What if we want to force the element from the previous section to show
> without going through the scenario that would set isFoo to true? We
> can do it from the console!

-   Select the element in the inspector.

-   run \$(\$0).scope().isFoo = true to set isFoo

-   run \$(\$0).scope().\$digest() to force Angular to reevaluate the
    > value

-   The DOM should change to reflect the new value

> ![](media/image4.gif){width="6.0in" height="2.3333333333333335in"}
>
> The first step, selecting the element, is very important. If you don't
> select the right element, you may or may not get the results you
> expect because of how prototypal inheritance delegation work. Your
> value may not always get propagated up or down the chain.
>
> **What is the digest cycle?**
>
> In the previous section, we used the \$digest method to trigger
> changes. You may wonder why we had to do that. Why didn't the DOM
> change the moment we set isFoo to true?
>
> Objects can't notify Angular that their properties have changed
> without proxies or custom setters. One Angular's goals is to let us
> use plain old JavaScript objects. Angular solves this using the digest
> cycle to inspect expressions and watchers for changes. Digest is run
> by Angular when an event it is aware of happens. This could be a
> an \$http request or an ng-click event.
>
> Proxies are a new feature of
> ES2015 <http://babeljs.io/docs/learn-es2015/#proxies>
>
> When something happens outside of Angular's known world about (maybe a
> jquery plugin, or a console command), it doesn't automatically
> run\$digest and nothing happens. In this case we'll need to
> execute\$digest ourselves. As soon as the digest executes, things will
> get updated.
>
> ES2015 is the next version of JavaScript, also known as ES6. It
> contains features that can be used by Angular in the future to improve
> performance by simplifying how object changes are detected, such as
> proxies. While it is possible to use most of ES2015's features
> using[Babel](http://babeljs.io/), a javascript compiler, fast
> proxies [must be implemented
> natively](https://babeljs.io/docs/learn-es2015/#proxies), so the
> current version of Angular uses dirty checking instead.
>
> **How does Angular DI work?**
>
> Angular is built on top of the concept of [dependency
> injection](https://docs.angularjs.org/guide/di). It can feel a little
> bit magical. While a full explanation of Angular's DI is out of the
> scope of this blog post, here's a few things to keep in mind as you
> wrap your head around it.
>
> Note that the following is a big oversimplification!

-   There's no magic behind Angular's DI. Under the hood, Angular keeps
    > a cache/map of keys to objects. When a key is in your component's
    > dependency (such as \$scope, \$http, or one of your own services),
    > Angular looks it up in the cache and passes the value to your
    > method when creating your component.

-   Angular services, factories and providers, values and constants are
    > almost all the same thing. They just differ in what kind of
    > control they give you when they are created, and if they can be
    > used in config blocks or not.

-   Under the hood, directives append "Directive" to their name. That is
    > why they don't conflict with other services of the same name.

-   A provider will have the suffix "Provider" when injected in a config
    > block, but won't when injected elsewhere (where the result of
    > its\$get method is injected instead)

-   All of those objects
    > are [singletons](https://docs.angularjs.org/guide/services), so
    > you're using the same instance everywhere (within one page load).
    > That is even true of factories and providers. The function they
    > provide gets called once per page load and the result is reused
    > everywhere it is injected.

> I strongly recommend learning the different types of angular services.
> They are a significant source of confusion when trying to wrap your
> head around an AngularJS code base.
>
> **Breakpoints are your friends.**
>
> You don't have to debug through your JavaScript code by
> addingconsole.log or debugger statements everywhere, though it can be
> useful. Consider familiarizing yourself
> with [breakpoints](https://developer.chrome.com/devtools/docs/javascript-debugging#breakpoints),
> available in the inspector of all major browsers.
>
> Chrome even supports conditional breakpoints, where the breakpoint
> will only stop execution if a certain JavaScript expression returns
> true. This is useful when debugging repetitive code where only a
> specific iteration is interesting (such as nested loops). You don't
> have to go through the entire loop to get where you want.
>
> ![](media/image5.jpg){width="6.0in" height="1.7395833333333333in"}
>
> **It's all JavaScript.**
>
> At the end of the day, the most important thing to understand about
> AngularJS, is that **It's just JavaScript**. There's no magic, and it
> is bound by the same rules as any other JavaScript applications.
> Dependency injection is just a big list of key value pairs from which
> objects are pulled from and passed to your components. The way scopes
> work is based on prototypal inheritance. The \$digest loop is just a
> task that iterates over expressions and watchers when Angular-related
> events occur. You can force it to happen.
>
> By understanding the good old JavaScript under Angular's hood, you can
> reduce the time it takes to debug your code base. It is worth the time
> to take a look at how Angular implements its own methods, including
> the directives for basic form elements from the Angular repository. It
> takes a bit of time, but gives a lot of background on how things end
> up working.
>
> [CC](https://creativecommons.org/licenses/by-sa/2.0/) background photo
> by flickr user [Jon
> Candy](https://www.flickr.com/photos/joncandy/3755718285), "Longleat
> Maze"
>
>  
>
> From
> &lt;<http://eng.localytics.com/tips-and-tricks-for-debugging-unfamiliar-angularjs-code/?ref=slicedham>&gt;
>
>  
>
>  

 

 

Tutorial

Wednesday, August 31, 2016

17:53

 

>  
>
>  
>
>  
>
> **ngApp**
>
> The **ng-app** attribute represents an Angular directive,
> named ngApp (Angular uses kebab-case for its custom attributes
> andcamelCase for the corresponding directives which implement them).
> This directive is used to flag the HTML element that Angular should
> consider to be the root element of our application. This gives
> application developers the freedom to tell Angular if the entire HTML
> page or only a portion of it should be treated as the AngularJS
> application.
>
>  

-   only one AngularJS application can be auto-bootstrapped per
    > HTML document. The first ngApp found in the document will be used
    > to define the root element to auto-bootstrap as an application. To
    > run multiple applications in an HTML document you must manually
    > bootstrap them
    > using [angular.bootstrap](https://docs.angularjs.org/api/ng/function/angular.bootstrap) instead.

-   AngularJS applications cannot be nested within each other.

-   Do not use a directive that
    > uses [transclusion](https://docs.angularjs.org/api/ng/service/$compile#transclusion) on
    > the same element as ngApp. This includes directives such
    > as [ngIf](https://docs.angularjs.org/api/ng/directive/ngIf), [ngInclude](https://docs.angularjs.org/api/ng/directive/ngInclude)and [ngView](https://docs.angularjs.org/api/ngRoute/directive/ngView).
    > Doing this misplaces the
    > app [\$rootElement](https://docs.angularjs.org/api/ng/service/$rootElement) and
    > the
    > app's [injector](https://docs.angularjs.org/api/auto/service/$injector),
    > causing animations to stop working and making the injector
    > inaccessible from outside the app.

>  
>
> Angular looks for
> the [ngApp](https://docs.angularjs.org/api/ng/directive/ngApp) directive.
> If Angular finds the directive, it will bootstrap the application with
> the root of the application DOM being the element on which
> the ngApp directive was defined. If
> the [ngApp](https://docs.angularjs.org/api/ng/directive/ngApp) directive
> is found then Angular will:

-   load
    > the [module](https://docs.angularjs.org/guide/module) associated
    > with the directive.

-   create the
    > application [injector](https://docs.angularjs.org/api/auto/service/$injector)

-   compile the DOM treating
    > the [ngApp](https://docs.angularjs.org/api/ng/directive/ngApp) directive
    > as the root of the compilation. This allows you to tell it to
    > treat only a portion of the DOM as an Angular application.

>  
>
>  
>
> As a best practice, consider adding an ng-strict-di directive on the
> same element as ng-app. This will ensure that all services in your
> application are properly annotated.
>
> Strict mode throws an error whenever a service tries to use implicit
> annotations
>
>  
>
> **Module**
>
>  
>
> You can think of a module as a container for the different parts of
> your app – controllers, services, filters, directives, etc.Most
> applications have a main method that instantiates and wires together
> the different parts of the application.Angular apps don't have a main
> method. Instead modules declaratively specify how an application
> should be bootstrapped. There are several advantages to this approach:
>
>  

-   The declarative process is easier to understand.

-   You can package code as reusable modules.

-   The modules can be loaded in any order (or even in parallel) because
    > modules delay execution.

-   Unit tests only have to load relevant modules, which keeps
    > them fast.

-   End-to-end tests can use modules to override configuration.

>  
>
>  
>
> In order for the injector to know how to create and wire together all
> of these objects, it needs a registry of "recipes". Each recipe has an
> identifier of the object and the description of how to create this
> object.
>
> Each recipe belongs to an Angular module. An Angular module is a bag
> that holds one or more recipes. And since manually keeping track of
> module dependencies is no fun, a module can contain information about
> dependencies on other modules as well. When an Angular application
> starts with a given application module, Angular creates a new instance
> of injector, which in turn creates a registry of recipes as a union of
> all recipes defined in the core "ng" module, application module and
> its dependencies. The injector then consults the recipe registry when
> it needs to create an object for your application.
>
>  
>
>  
>
> **Recommended Setup**
>
>  
>
> Instead we recommend that you break your application to multiple
> modules like this.
>
>  

-   A module for each feature

-   A module for each reusable component (especially directives
    > and filters)

-   And an application level module which depends on the above modules
    > and contains any initialization code.

>  
>
> A module is a collection of configuration and run blocks which get
> applied to the application during the bootstrap process. In its
> simplest form the module consists of a collection of two kinds of
> blocks:

-   **Configuration blocks** - get executed during the provider
    > registrations and configuration phase. Only providers and
    > constants can be injected into configuration blocks. This is to
    > prevent accidental instantiation of services before they have been
    > fully configured.

-   **Run blocks** - get executed after the injector is created and are
    > used to kickstart the application. Only instances and constants
    > can be injected into run blocks. This is to prevent further system
    > configuration during application run time.

>  
>
> angular.module('myModule', \[\]).\
> config(function(injectables) { // provider-injector\
> // This is an example of config block.\
> // You can have as many of these as you want.\
> // You can only inject Providers (not instances)\
> // into config blocks.\
> }).\
> run(function(injectables) { // instance-injector\
> // This is an example of a run block.\
> // You can have as many of these as you want.\
> // You can only inject instances (not Providers)\
> // into run blocks\
> });
>
>  
>
>  
>
> When bootstrapping, first Angular applies all constant definitions.
> Then Angular applies configuration blocks in the same order they were
> registered.
>
>  
>
> Run blocks are the closest thing in Angular to the main method. A run
> block is the code which needs to run to kickstart the application. It
> is executed after all of the services have been configured and the
> injector has been created. Run blocks typically contain code which is
> hard to unit-test, and for this reason should be declared in isolated
> modules, so that they can be ignored in the unit-tests.
>
>  
>
> Modules can list other modules as their dependencies. Depending on a
> module implies that the required module needs to be loaded before the
> requiring module is loaded. In other words the configuration blocks of
> the required modules execute before the configuration blocks of the
> requiring module. The same is true for the run blocks. Each module can
> only be loaded once, even if multiple other modules require it.
>
>  
>
> Beware that using angular.module('myModule', \[\]) will create the
> module myModule and overwrite any existing module namedmyModule.
> Use angular.module('myModule') to retrieve an existing module.
>
> var myModule = angular.module('myModule', \[\]);
>
> // add some directives and services\
> myModule.service('myService', ...);\
> myModule.directive('myDirective', ...);
>
> // overwrites both myService and myDirective by creating a new module\
> var myModule = angular.module('myModule', \[\]);
>
> // throws an error because myOtherModule has yet to be defined\
> var myModule = angular.module('myOtherModule');
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
> **Dependency Injection**
>
>  
>
> Refer :
> <https://github.com/angular/angular.js/wiki/Understanding-Dependency-Injection>
>
>  
>
> There are only three ways a component (object or function) can get a
> hold of its dependencies:

-   The component can create the dependency, typically
    > using the new operator.

-   The component can look up the dependency, by referring to a
    > global variable.

-   The component can have the dependency passed to it where it
    > is needed.

> The first two options of creating or looking up dependencies are not
> optimal because they hard code the dependency to the component. This
> makes it difficult, if not impossible, to modify the dependencies.
> This is especially problematic in tests, where it is often desirable
> to provide mock dependencies for test isolation.
>
> The third option is the most viable, since it removes the
> responsibility of locating the dependency from the component. The
> dependency is simply handed to the component.
>
> To manage the responsibility of dependency creation, each Angular
> application has
> an [injector](https://docs.angularjs.org/api/ng/function/angular.injector).
> The injector is a [service
> locator](http://en.wikipedia.org/wiki/Service_locator_pattern) that is
> responsible for construction and lookup of dependencies.
>
> Asking for dependencies solves the issue of hard coding, but it also
> means that the injector needs to be passed throughout the application.
> Passing the injector breaks the [Law of
> Demeter](http://en.wikipedia.org/wiki/Law_of_Demeter). To remedy this,
> we use a declarative notation in our HTML templates, to hand the
> responsibility of creating components over to the injector,
>
>  
>
> When Angular compiles the HTML, it processes
> the ng-controller directive, which in turn asks the injector to create
> an instance of the controller and its dependencies. This is all done
> behind the scenes. Notice that by having the ng-controller ask the
> injector to instantiate the class, it can satisfy all of the
> dependencies of MyController without the controller ever knowing about
> the injector.
>
>  
>
> Dependency injection helps to make your web applications both
> well-structured (e.g. separate entities for presentation, data, and
> control) and loosely coupled (dependencies between entities are not
> resolved by the entities themselves, but by the DI subsystem). As a
> result, applications are easier to test as well.
>
>  
>
> **BootStrapping**
>
>  
>
> A binding, denoted by double-curlies: {{ }}
>
> The binding tells Angular that it should evaluate an expression and
> insert the result into the DOM in place of the binding. Rather than a
> one-time insert, a binding will result in efficient continuous updates
> whenever the result of the expression evaluation changes. Angular
> expressions are JavaScript-like code snippets that are evaluated by
> Angular in the context of the current model scope, rather than within
> the scope of the global context (window).
>
>  
>
> There are 3 important things that happen during the bootstrap phase:

-   The [injector](https://docs.angularjs.org/api/auto/service/$injector) that
    > will be used for dependency injection is created.

-   The injector will then create the [root
    > scope](https://docs.angularjs.org/api/ng/service/$rootScope) that
    > will become the context for the model of our application.

-   Angular will then "compile" the DOM starting at the ngApp root
    > element, processing any directives and bindings found along
    > the way.

> Once an application is bootstrapped, it will then wait for incoming
> browser events (such as mouse clicks, key presses or incoming HTTP
> responses) that might change the model. Once such an event occurs,
> Angular detects if it caused any model changes and if changes are
> found, Angular will reflect them in the view by updating all of the
> affected bindings.
>
>  
>
>  
>
> **View and Template**
>
>  
>
> In Angular, the view is a projection of the model through the HTML
> template. This means that whenever the model changes, Angular
> refreshes the appropriate binding points, which updates the view.
>
>  
>
> We have also added a new directive, called ngController, which
> attaches a PhoneListController controller to the &lt;body&gt; tag. At
> this point:
>
>  
>
> PhoneListController is in charge of the DOM sub-tree under (and
> including) the &lt;body&gt; element.
>
> The expressions in curly braces ({{phone.name}} and {{phone.snippet}})
> denote bindings, which are referring to our application model, which
> is set up in our PhoneListController controller.
>
>  
>
> Here we declared a controller called PhoneListController and
> registered it in an Angular module, phonecatApp. Notice that
> our ngAppdirective (on the &lt;html&gt; tag) now specifies
> the phonecatApp module name as the module to load when bootstrapping
> the application.
>
>  
>
> // Define the \`phonecatApp\` module\
> var phonecatApp = angular.module('phonecatApp', \[\]);
>
> // Define the \`PhoneListController\` controller on the
> \`phonecatApp\` module\
> phonecatApp.controller('PhoneListController', function
> PhoneListController(\$scope) {
>
>  
>
> Although the controller is not yet doing very much, it plays a crucial
> role. By providing context for our data model, the controller allows
> us to establish data-binding between the model and the view. We
> connected the dots between the presentation, data, and logic
> components as follows:

-   The [ngController](https://docs.angularjs.org/api/ng/directive/ngController) directive,
    > located on the &lt;body&gt; tag, references the name of our
    > controller, PhoneListController (located in the
    > JavaScript file app.js).

-   The PhoneListController controller attaches the phone data to
    > the \$scope that was injected into our controller function.
    > This*scope* is a prototypal descendant of the *root scope* that
    > was created when the application was defined. This controller
    > scope is available to all bindings located
    > within the &lt;body ng-controller="PhoneListController"&gt; tag.

>  
>
> **Template**
>
>  
>
> In Angular, templates are written with HTML that contains
> Angular-specific elements and attributes. Angular combines the
> template with information from the model and controller to render the
> dynamic view that a user sees in the browser.
>
>  
>
> These are the types of Angular elements and attributes you can use:

-   [Directive](https://docs.angularjs.org/guide/directive) — An
    > attribute or element that augments an existing DOM element or
    > represents a reusable DOM component.

-   [Markup](https://docs.angularjs.org/api/ng/service/$interpolate) —
    > The double curly brace notation {{ }} to bind expressions to
    > elements is built-in Angular markup.

-   [Filter](https://docs.angularjs.org/guide/filter) — Formats data
    > for display.

-   [Form controls](https://docs.angularjs.org/guide/forms) — Validates
    > user input.

>  
>
>  
>
>  
>
> **Testing**
>
> The "Angular way" of separating controller from the view, makes it
> easy to test code as it is being developed. If our controller were
> available on the global namespace, we could simply instantiate it with
> a mock scope object:
>
>  
>
>  
>
>  
>
> describe('PhoneListController', function() {
>
>  
>
> it('should create a \`phones\` model with 3 phones', function() {
>
> var scope = {};
>
> var ctrl = new PhoneListController(scope);
>
>  
>
> expect(scope.phones.length).toBe(3);
>
> });
>
>  
>
> });
>
> The test instantiates PhoneListController and verifies that the phones
> array property on the scope contains three records. This example
> demonstrates how easy it is to create a unit test for code in Angular.
> Since testing is such a critical part of software development, we make
> it easy to create tests in Angular so that developers are encouraged
> to write them.
>
>  
>
> In practice, you will not want to have your controller functions in
> the global namespace. Instead, you can see that we have registered it
> via a constructor function on the phonecatApp module.
>
>  
>
> In this case Angular provides a service, \$controller, which will
> retrieve your controller by name. Here is the same test using
> \$controller:
>
> describe('PhoneListController', function() {
>
> beforeEach(module('phonecatApp'));
>
> it('should create a \`phones\` model with 3 phones',
> inject(function(\$controller) {\
> var scope = {};\
> var ctrl = \$controller('PhoneListController', {\$scope: scope});
>
> expect(scope.phones.length).toBe(3);\
> }));
>
> });

-   Before each test we tell Angular to load the phonecatApp module.

-   We ask Angular to inject the \$controller service into our
    > test function.

-   We use \$controller to create an instance
    > of the PhoneListController.

-   With this instance, we verify that the phones array property on the
    > scope contains three records.

>  
>
>  
>
>  
>
> **Scope**
>
> The concept of a scope in Angular is crucial. A scope can be seen as
> the glue which allows the template, model, and controller to work
> together. Angular uses scopes, along with the information contained in
> the template, data model, and controller, to keep models and views
> separate, but in sync. Any changes made to the model are reflected in
> the view; any changes that occur in the view are reflected in the
> model.
>
> Scope is an object that refers to the application model. It is an
> execution context for expressions. Scopes are arranged in hierarchical
> structure which mimic the DOM structure of the application. Scopes can
> watch expressions and propagate events.

-   Scopes provide APIs
    > ([\$watch](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$watch))
    > to observe model mutations.

-   Scopes provide APIs
    > ([\$apply](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$apply))
    > to propagate any model changes through the system into the view
    > from outside of the "Angular realm" (controllers, services,
    > Angular event handlers).

-   Scopes can be nested to limit access to the properties of
    > application components while providing access to shared
    > model properties. Nested scopes are either "child scopes" or
    > "isolate scopes". A "child scope" (prototypically) inherits
    > properties from its parent scope. An "isolate scope" does not.
    > See [isolated
    > scopes](https://docs.angularjs.org/guide/directive#isolating-the-scope-of-a-directive) for
    > more information.

-   Scopes provide context against
    > which [expressions](https://docs.angularjs.org/guide/expression) are evaluated.
    > For example {{username}} expression is meaningless, unless it is
    > evaluated against a specific scope which
    > defines the username property.

>  
>
> Scope is the glue between application controller and the view. During
> the template linking phase the directives set up \$watch expressions
> on the scope. The \$watch allows the directives to be notified of
> property changes, which allows the directive to render the updated
> value to the DOM.
>
> Both controllers and directives have reference to the scope, but not
> to each other. This arrangement isolates the controller from the
> directive as well as from the DOM. This is an important point since it
> makes the controllers view agnostic, which greatly improves the
> testing story of the applications.
>
>  
>
> Logically the rendering of {{greeting}} involves:

-   retrieval of the scope associated with DOM node
    > where {{greeting}} is defined in template. In this example this is
    > the same scope as the scope which was passed into MyController.
    > (We will discuss scope hierarchies later.)

-   Evaluate
    > the greeting [expression](https://docs.angularjs.org/guide/expression) against
    > the scope retrieved above, and assign the result to the text of
    > the enclosing DOM element.

>  
>
> Scopes are attached to the DOM as \$scope data property, and can be
> retrieved for debugging purposes. (It is unlikely that one would need
> to retrieve scopes in this way inside the application.) The location
> where the root scope is attached to the DOM is defined by the location
> of ng-app directive. Typically ng-app is placed on the &lt;html&gt;
> element, but it can be placed on other elements as well, if, for
> example, only a portion of the view needs to be controlled by Angular.
>
>  
>
> **Scope Hierarchies**
>
>  
>
> Each Angular application has exactly one root scope, but may have
> several child scopes.
>
> The application can have multiple scopes, because some directives
> create new child scopes (refer to directive documentation to see which
> directives create new scopes). When new scopes are created, they are
> added as children of their parent scope. This creates a tree structure
> which parallels the DOM where they're attached.
>
> When Angular evaluates {{name}}, it first looks at the scope
> associated with the given element for the name property. If no such
> property is found, it searches the parent scope and so on until the
> root scope is reached. In JavaScript this behavior is known as
> prototypical inheritance, and child scopes prototypically inherit from
> their parents.
>
>  
>
> **Scope Life Cycle**
>
>  
>
> The normal flow of a browser receiving an event is that it executes a
> corresponding JavaScript callback. Once the callback completes the
> browser re-renders the DOM and returns to waiting for more events.
>
> When the browser calls into JavaScript the code executes outside the
> Angular execution context, which means that Angular is unaware of
> model modifications. To properly process model modifications the
> execution has to enter the Angular execution context using the \$apply
> method. Only model modifications which execute inside the \$apply
> method will be properly accounted for by Angular. For example if a
> directive listens on DOM events, such as ng-click it must evaluate the
> expression inside the \$apply method.
>
>  
>
> After evaluating the expression, the \$apply method performs a
> \$digest. In the \$digest phase the scope examines all of the \$watch
> expressions and compares them with the previous value. This dirty
> checking is done asynchronously. This means that assignment such as
> \$scope.username="angular" will not immediately cause a \$watch to be
> notified, instead the \$watch notification is delayed until the
> \$digest phase. This delay is desirable, since it coalesces multiple
> model updates into one \$watch notification as well as guarantees that
> during
>
> the \$watch notification no other \$watches are running. If a \$watch
> changes the value of the model, it will force additional \$digest
> cycle.
>
>  

-   **Creation\
    > **The [**root
    > scope**](https://docs.angularjs.org/api/ng/service/$rootScope) is
    > created during the application bootstrap by
    > the [**\$injector**](https://docs.angularjs.org/api/auto/service/$injector).
    > During template linking, some directives create new child scopes.

-   **Watcher registration\
    > **During template linking, directives
    > register [**watches**](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$watch) on
    > the scope. These watches will be used to propagate model values to
    > the DOM.

-   **Model mutation\
    > **For mutations to be properly observed, you should make them only
    > within
    > the [**scope.\$apply()**](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$apply).
    > Angular APIs do this implicitly, so no extra \$apply call is
    > needed when doing synchronous work in controllers, or asynchronous
    > work
    > with [**\$http**](https://docs.angularjs.org/api/ng/service/$http), [**\$timeout**](https://docs.angularjs.org/api/ng/service/$timeout) or [**\$interval**](https://docs.angularjs.org/api/ng/service/$interval)services.

-   **Mutation observation\
    > **At the end of \$apply, Angular performs
    > a [**\$digest**](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$digest) cycle
    > on the root scope, which then propagates throughout all
    > child scopes. During the \$digest cycle, all \$watched expressions
    > or functions are checked for model mutation and if a mutation is
    > detected, the \$watch listener is called.

-   **Scope destruction\
    > **When child scopes are no longer needed, it is the responsibility
    > of the child scope creator to destroy them
    > via [**scope.\$destroy()**](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$destroy) API.
    > This will stop propagation of \$digest calls into the child scope
    > and allow for memory used by the child scope models to be
    > reclaimed by the garbage collector.

>  
>
> During the compilation phase, the compiler matches directives against
> the DOM template. The directives usually fall into one of two
> categories:
>
> Observing directives, such as double-curly expressions {{expression}},
> register listeners using the \$watch() method. This type of directive
> needs to be notified whenever the expression changes so that it can
> update the view.
>
> Listener directives, such as ng-click, register a listener with the
> DOM. When the DOM listener fires, the directive executes the
> associated expression and updates the view using the \$apply()
> method.When an external event (such as a user action, timer or XHR) is
> received, the associated expression must be applied to the scope
> through the \$apply() method so that all listeners are updated
> correctly.
>
>  
>
> In most cases, directives and scopes interact but do not create new
> instances of scope. However, some directives, such as ng-controller
> and ng-repeat, create new child scopes and attach the child scope to
> the corresponding DOM element. You can retrieve a scope for any DOM
> element by using an angular.element(aDomElement).scope() method call.
>
>  
>
> Scopes and controllers interact with each other in the following
> situations:

-   Controllers use scopes to expose controller methods to templates
    > (see [ng-controller](https://docs.angularjs.org/api/ng/directive/ngController)).

-   Controllers define methods (behavior) that can mutate the model
    > (properties on the scope).

-   Controllers may
    > register [watches](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$watch) on
    > the model. These watches execute immediately after the controller
    > behavior executes.

>  
>
> Here is the explanation of how the Hello world example achieves the
> data-binding effect when the user enters text into the text field.

-   During the compilation phase:

    1.  the [ng-model](https://docs.angularjs.org/api/ng/directive/ngModel) and [input](https://docs.angularjs.org/api/ng/directive/input) [directive](https://docs.angularjs.org/guide/directive) set
        > up a keydown listener on the &lt;input&gt; control.

    2.  the [interpolation](https://docs.angularjs.org/api/ng/service/$interpolate) sets
        > up
        > a [\$watch](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$watch) to
        > be notified of name changes.

<!-- -->

-   During the runtime phase:

    1.  Pressing an 'X' key causes the browser to emit a keydown event
        > on the input control.

    2.  The [input](https://docs.angularjs.org/api/ng/directive/input) directive
        > captures the change to the input's value and
        > calls [\$apply](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$apply)("name
        > = 'X';") to update the application model inside the Angular
        > execution context.

    3.  Angular applies the name = 'X'; to the model.

    4.  The [\$digest](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$digest) loop
        > begins

    5.  The [\$watch](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$watch) list
        > detects a change on the name property and notifies
        > the [interpolation](https://docs.angularjs.org/api/ng/service/$interpolate),
        > which in turn updates the DOM.

    6.  Angular exits the execution context, which in turn exits
        > the keydown event and with it the JavaScript
        > execution context.

    7.  The browser re-renders the view with the updated text.

>  
>
>  
>
> **ngController**
>
>  
>
> MVC components in angular:

-   Model — Models are the properties of a scope; scopes are attached to
    > the DOM where scope properties are accessed through bindings.

-   View — The template (HTML with data bindings) that is rendered into
    > the View.

-   Controller — The ngController directive specifies a Controller
    > class; the class contains business logic behind the application to
    > decorate the scope with functions and values

>  
>
> Note that you can also attach controllers to the DOM by declaring it
> in a route definition via the \$route service. A common mistake is to
> declare the controller again using ng-controller in the template
> itself. This will cause the controller to be attached and executed
> twice.
>
>  

-   This directive creates new scope.

-   This directive executes at priority level 500.

>  
>
> Two different declaration styles are included below:

-   one binds methods and properties directly onto the controller
    > using this: ng-controller="SettingsController1 as settings"

-   one injects \$scope into the
    > controller: ng-controller="SettingsController2"

>  
>
> The second option is more common in the Angular community, and is
> generally used in boilerplates and in this guide. However, there are
> advantages to binding properties directly to the controller and
> avoiding scope.

-   Using controller as makes it obvious which controller you are
    > accessing in the template when multiple controllers apply to
    > an element.

-   If you are writing your controllers as classes you have easier
    > access to the properties and methods, which will appear on the
    > scope, from inside the controller code.

-   Since there is always a . in the bindings, you don't have to worry
    > about prototypal inheritance masking primitives.

>  
>
> **Controller**
>
>  
>
> In Angular, a Controller is defined by a JavaScript constructor
> function that is used to augment the Angular Scope. When a Controller
> is attached to the DOM via the ng-controller directive, Angular will
> instantiate a new Controller object, using the specified Controller's
> constructor function. A new child scope will be created and made
> available as an injectable parameter to the Controller's constructor
> function as \$scope. If the controller has been attached using the
> controller as syntax then the controller instance will be assigned to
> a property on the new scope.
>
>  
>
> Use controllers to:

-   Set up the initial state of the \$scope object.

-   Add behavior to the \$scope object.

> Do not use controllers to:

-   Manipulate DOM — Controllers should contain only business logic.
    > Putting any presentation logic into Controllers significantly
    > affects its testability. Angular
    > has [databinding](https://docs.angularjs.org/guide/databinding) for
    > most cases
    > and [directives](https://docs.angularjs.org/guide/directive) to
    > encapsulate manual DOM manipulation.

-   Format input — Use [angular form
    > controls](https://docs.angularjs.org/guide/forms) instead.

-   Filter output — Use [angular
    > filters](https://docs.angularjs.org/guide/filter) instead.

-   Share code or state across controllers — Use [angular
    > services](https://docs.angularjs.org/guide/services) instead.

-   Manage the life-cycle of other components (for example, to create
    > service instances).

>  
>
>  
>
> It is common to attach Controllers at different levels of the DOM
> hierarchy. Since the ng-controller directive creates a new child
> scope, we get a hierarchy of scopes that inherit from each other. The
> \$scope that each Controller receives will have access to properties
> and methods defined by Controllers higher up the hierarchy.
>
>  
>
>  
>
> **Angular expressions**
>
> Angular expressions are like JavaScript expressions with the following
> differences:

-   **Context:** JavaScript expressions are evaluated against
    > the global window. In Angular, expressions are evaluated against
    > a [scope](https://docs.angularjs.org/api/ng/type/$rootScope.Scope)object.

> Angular does not use JavaScript's eval() to evaluate expressions.
> Instead Angular's \$parse service processes these expressions.
>
> Angular expressions do not have access to global variables like
> window, document or location. This restriction is intentional. It
> prevents accidental access to the global state – a common source of
> subtle bugs.
>
> Instead use services like \$window and \$location in functions called
> from expressions. Such services provide mockable access to globals.
>
> It is possible to access the context object using the identifier this
> and the locals object using the identifier \$locals.
>
>  

-   **Forgiving:** In JavaScript, trying to evaluate undefined
    > properties generates ReferenceError or TypeError. In Angular,
    > expression evaluation is forgiving to undefined and null.

> Expression evaluation is forgiving to undefined and null. In
> JavaScript, evaluating a.b.c throws an exception if a is not an
> object. While this makes sense for a general purpose language, the
> expression evaluations are primarily used for data binding, which
> often look like this:
>
>  
>
> {{a.b.c}}
>
> It makes more sense to show nothing than to throw an exception if a is
> undefined (perhaps we are waiting for the server response, and it will
> become defined soon). If expression evaluation wasn't forgiving we'd
> have to write bindings that clutter the code, for example:
> {{((a||{}).b||{}).c}}
>
>  
>
> Similarly, invoking a function a.b.c() on undefined or null simply
> returns undefined.
>
>  

-   **Filters:** You can
    > use [filters](https://docs.angularjs.org/guide/filter) within
    > expressions to format data before displaying it.

-   **No Control Flow Statements:** You cannot use the following in an
    > Angular expression: conditionals, loops, or exceptions.

> Apart from the ternary operator (a ? b : c), you cannot write a
> control flow statement in an expression. The reason behind this is
> core to the Angular philosophy that application logic should be in
> controllers, not the views. If you need a real conditional, loop, or
> to throw from a view expression, delegate to a JavaScript method
> instead.

-   **No Function Declarations:** You cannot declare functions in an
    > Angular expression, even inside ng-init directive.

> You can't declare functions or create regular expressions from within
> AngularJS expressions. This is to avoid complex model transformation
> logic inside templates. Such logic is better placed in a controller or
> in a dedicated filter where it can be tested properly.

-   **No RegExp Creation With Literal Notation:** You cannot create
    > regular expressions in an Angular expression.

-   **No Object Creation With New Operator:** You cannot
    > use new operator in an Angular expression.

-   **No Bitwise, Comma, And Void Operators:** You cannot
    > use [Bitwise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators), , or void operators
    > in an Angular expression.

> If you want to run more complex JavaScript code, you should make it a
> controller method and call the method from your view. If you want
> to eval() an Angular expression yourself, use
> the [\$eval()](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$eval) method
>
>  
>
> **One-time binding**
>
> An expression that starts with :: is considered a one-time expression.
> One-time expressions will stop recalculating once they are stable,
> which happens after the first digest if the expression result is a
> non-undefined value
>
> The main purpose of one-time binding expression is to provide a way to
> create a binding that gets deregistered and frees up resources once
> the binding is stabilized. Reducing the number of expressions being
> watched makes the digest loop faster and allows more information to be
> displayed at the same time
>
>  
>
>  
>
> **Interpolation and data-binding**
>
>  
>
> Interpolation markup with
> embedded [expressions](https://docs.angularjs.org/guide/expression) is
> used by Angular to provide data-binding to text nodes and attribute
> values.
>
> An example of interpolation is shown below:
>
> &lt;a ng-href="img/{{username}}.jpg"&gt;Hello {{username}}!&lt;/a&gt;
>
>  
>
> During the compilation process the compiler uses the \$interpolate
> service to see if text nodes and element attributes contain
> interpolation markup with embedded expressions.
>
> If that is the case, the compiler adds an interpolateDirective to the
> node and registers watches on the computed interpolation function,
> which will update the corresponding text nodes or attribute values as
> part of the normal digest cycle.
>
>  
>
> If the interpolated value is not a String, it is computed as follows:

-   undefined and null are converted to ''

-   if the value is an object that is not a Number, Date or Array,
    > \$interpolate looks for a custom toString() function on the
    > object, and uses that. Custom
    > means that myObject.toString !==Object.prototype.toString\`.

-   if the above doesn't apply, JSON.stringify is used.

>  
>
> Attributes such as disabled are called boolean attributes, because
> their presence means true and their absence means false. We cannot use
> normal attribute bindings with them, because the HTML specification
> does not require browsers to preserve the values of boolean
> attributes. This means that if we put an Angular interpolation
> expression into such an attribute then the binding information would
> be lost, because the browser ignores the attribute value.
>
>  
>
> In the following example, the interpolation information would be
> ignored and the browser would simply interpret the attribute as
> present, meaning that the button would always be disabled.
>
> Disabled: &lt;input type="checkbox" ng-model="isDisabled" /&gt;\
> &lt;button disabled="{{isDisabled}}"&gt;Disabled&lt;/button&gt;
>
>  
>
> For this reason, Angular provides special ng-prefixed directives for
> the following boolean attributes: disabled, required, selected,
> checked, readOnly , and open. These directives take an expression
> inside the attribute, and set the corresponding boolean attribute to
> true when the expression evaluates to truthy.
>
>  
>
> Disabled: &lt;input type="checkbox" ng-model="isDisabled" /&gt;\
> &lt;button ng-disabled="isDisabled"&gt;Disabled&lt;/button&gt;
>
>  
>
> Web browsers are sometimes picky about what values they consider valid
> for attributes.For example, considering this template:
>
> &lt;svg&gt;\
> &lt;circle cx="{{cx}}"&gt;&lt;/circle&gt;\
> &lt;/svg&gt;
>
> We would expect Angular to be able to bind to this, but when we check
> the console we see something likeError: Invalid value for attribute
> cx="{{cx}}". Because of the SVG DOM API's restrictions, you cannot
> simply write cx="{{cx}}".With ng-attr-cx you can work around this
> problem.
>
>  
>
> If an attribute with a binding is prefixed with the ngAttr prefix
> (denormalized as ng-attr-) then during the binding it will be applied
> to the corresponding unprefixed attribute. This allows you to bind to
> attributes that would otherwise be eagerly processed by browsers (e.g.
> an SVG element's circle\[cx\] attributes). When using ngAttr, the
> allOrNothing flag of \$interpolate is used, so if any expression in
> the interpolated string results in undefined, the attribute is removed
> and not added to the element.
>
>  
>
> For example, we could fix the example above by instead writing:
>
> &lt;svg&gt;\
> &lt;circle ng-attr-cx="{{cx}}"&gt;&lt;/circle&gt;\
> &lt;/svg&gt;
>
>  
>
> If one wants to modify a camelcased attribute (SVG elements have valid
> camelcased attributes), such as viewBox on the svg element, one can
> use underscores to denote that the attribute to bind to is naturally
> camelcased.
>
> For example, to bind to viewBox, we can write:
>
> &lt;svg ng-attr-view\_box="{{viewBox}}"&gt;\
> &lt;/svg&gt;
>
>  
>
> You should avoid dynamically changing the content of an interpolated
> string (e.g. attribute value or text node). Your changes are likely to
> be overwriten, when the original string gets evaluated. This
> restriction applies to both directly changing the content via
> JavaScript or indirectly using a directive.
>
> For example, you should not use interpolation in the value of the
> style attribute (e.g. style="color: {{ 'orange' }}; font-weight: {{
> 'bold' }};") and at the same time use a directive that changes the
> content of that attributte, such as ngStyle.
>
>  
>
> **Embedding interpolation markup inside expressions**
>
>  
>
> &lt;div ng-show="form{{\$index}}.\$invalid"&gt;&lt;/div&gt;
>
> You should instead delegate the computation of complex expressions to
> the scope, like this:
>
> &lt;div ng-show="getForm(\$index).\$invalid"&gt;&lt;/div&gt;
>
> function getForm(index) {\
> return \$scope\['form' + index\];\
> }
>
>  
>
> Why mixing interpolation and expressions is bad practice:

-   It increases the complexity of the markup

-   There is no guarantee that it works for every directive, because
    > interpolation itself is a directive. If another directive accesses
    > attribute data before interpolation has run, it will get the raw
    > interpolation markup and not data.

-   It impacts performance, as interpolation adds another watcher to
    > the scope.

-   Since this is not recommended usage, we do not test for this, and
    > changes to Angular core may break your code.

>  
>
>  
>
> **Components**
>
>  
>
> The template (the part of the view containing the bindings and
> presentation logic) acts as a blueprint for how our data should be
> organized and presented to the user. The controller provides the
> context in which the bindings are evaluated and applies behavior and
> logic to our template.
>
>  
>
> There are still a couple of areas we can do better:

-   What if we want to reuse the same functionality in a different part
    > of our application ?\
    > We would need to duplicate the whole template (including
    > the controller). This is error-prone and hurts maintainability.

-   The scope, that glues our controller and template together into a
    > dynamic view, is not isolated from other parts of the page. What
    > this means is that a random, unrelated change in a different part
    > of the page (e.g. a property-name conflict) could have unexpected
    > and hard-to-debug side effects on our view.

> Since this combination (template + controller) is such a common and
> recurring pattern, Angular provides an easy and concise way to combine
> them together into reusable and isolated entities, known as
> components. Additionally, Angular will create a so called isolate
> scope for each instance of our component, which means no prototypal
> inheritance and no risk of our component affecting other parts of the
> application or vice versa.
>
>  
>
> To create a component, we use the .component() method of an Angular
> module. We must provide the name of the component and the Component
> Definition Object (CDO for short).
>
> Remember that (since components are also directives) the name of the
> component is in camelCase (e.g. myAwesomeComponent), but we will use
> kebab-case (e.g. my-awesome-component) when referring to it in our
> HTML
>
>  
>
> In its simplest form, the CDO will just contain a template and a
> controller. (We can actually omit the controller and Angular will
> create a dummy controller for us. This is useful for simple
> "presentational" components, that don't attach any behavior to the
> template.)
>
>  
>
> angular.\
> module('myApp').\
> component('greetUser', {\
> template: 'Hello, {{\$ctrl.user}}!',\
> controller: function GreetUserController() {\
> this.user = 'world';\
> }\
> });
>
>  
>
> Now, every time we include &lt;greet-user&gt;&lt;/greet-user&gt; in
> our view, Angular will expand it into a DOM sub-tree constructed using
> the provided template and managed by an instance of the specified
> controller
>
> For reasons already mentioned (and for other reasons that are out of
> the scope of this tutorial), it is considered a good practice to avoid
> using the scope directly. We can (and should) use our controller
> instance; i.e. assign our data and methods on properties of our
> controller (the "this" inside the controller constructor), instead of
> directly to the scope.
>
> From the template, we can refer to our controller instance using an
> alias. This way, the context of evaluation for our expressions is even
> more clear. By default, components use \$ctrl as the controller alias,
> but we can override it, should the need arise
>
>  

-   Our phone list is reusable. Just
    > drop &lt;phone-list&gt;&lt;/phone-list&gt; anywhere in the page to
    > get a list of phones.

-   Our main view (index.html) is cleaner and more declarative. Just by
    > looking at it, we know there is a list of phones. We are not
    > bothered with implementation details.

-   Our component is isolated and safe from "external influences".
    > Likewise, we don't have to worry, that we might accidentally break
    > something in some other part of the application. What happens
    > inside our component, stays inside our component.

-   It's easier to test our component in isolation.

>  
>
> Advantages of Components:

-   simpler configuration than plain directives

-   promote sane defaults and best practices

-   optimized for component-based architecture

-   writing component directives will make it easier to upgrade to
    > Angular 2

> When not to use Components:

-   for directives that rely on DOM manipulation, adding event listeners
    > etc, because the compile and link functions are unavailable

-   when you need advanced directive definition options like priority,
    > terminal, multi-element

-   when you want a directive that is triggered by an attribute or CSS
    > class, rather than an element

>  

-   **Components only control their own View and Data:** Components
    > should never modify any data or DOM that is out of their
    > own scope. Normally, in Angular it is possible to modify data
    > anywhere in the application through scope inheritance and watches.
    > This is practical, but can also lead to problems when it is not
    > clear which part of the application is responsible for modifying
    > the data. That is why component directives use an isolate scope,
    > so a whole class of scope manipulation is not possible.

-   **Components have a well-defined public API - Inputs and
    > Outputs:** However, scope isolation only goes so far, because
    > Angular uses two-way binding. So if you pass an object to a
    > component like this - bindings: {item: '='}, and modify one of its
    > properties, the change will be reflected in the parent component.
    > For components however, only the component that owns the data
    > should modify it, to make it easy to reason about what data is
    > changed, and when. For that reason, components should follow a few
    > simple conventions:

    1.  Inputs should be using &lt; and @ bindings. The &lt; symbol
        > denotes [one-way
        > bindings](https://docs.angularjs.org/api/ng/service/$compile#-scope-) which
        > are available since 1.5. The difference to = is that the bound
        > properties in the component scope are not watched, which means
        > if you assign a new value to the property in the component
        > scope, it will not update the parent scope. Note however, that
        > both parent and component scope reference the same object, so
        > if you are changing object properties or array elements in the
        > component, the parent will still reflect that change. The
        > general rule should therefore be to never change an object or
        > array property in the component scope. @ bindings can be used
        > when the input is a string, especially when the value of the
        > binding doesn't change.\
        > bindings: {\
        > hero: '&lt;',\
        > comment: '@'\
        > }

    2.  Outputs are realized with & bindings, which function as
        > callbacks to component events.\
        > bindings: {\
        > onDelete: '&',\
        > onUpdate: '&'\
        > }

    3.  Instead of manipulating Input Data, the component calls the
        > correct Output Event with the changed data. For a deletion,
        > that means the component doesn't delete the hero itself, but
        > sends it back to the owner component via the correct event.\
        > &lt;!-- note that we use kebab-case for bindings in the
        > template as usual --&gt;\
        > &lt;editable-field on-update="\$ctrl.update('location',
        > value)"&gt;&lt;/editable-field&gt;&lt;br&gt;\
        > &lt;button ng-click="\$ctrl.onDelete({hero:
        > \$ctrl.hero})"&gt;Delete&lt;/button&gt;

    4.  That way, the parent component can decide what to do with the
        > event (e.g. delete an item or update the properties)\
        > ctrl.deleteHero(hero) {\
        > \$http.delete(...).then(function() {\
        > var idx = ctrl.list.indexOf(hero);\
        > if (idx &gt;= 0) {\
        > ctrl.list.splice(idx, 1);\
        > }\
        > });\
        > }

<!-- -->

-   **Components have a well-defined lifecycle** Each component can
    > implement "lifecycle hooks". These are methods that will be called
    > at certain points in the life of the component. The following hook
    > methods can be implemented:

    1.  \$onInit() - Called on each controller after all the controllers
        > on an element have been constructed and had their bindings
        > initialized (and before the pre & post linking functions for
        > the directives on this element). This is a good place to put
        > initialization code for your controller.

    2.  \$onChanges(changesObj) - Called whenever one-way bindings
        > are updated. The changesObj is a hash whose keys are the names
        > of the bound properties that have changed, and the values are
        > an object of
        > the form{ currentValue, previousValue, isFirstChange() }. Use
        > this hook to trigger updates within a component such as
        > cloning the bound value to prevent accidental mutation of the
        > outer value.

    3.  \$doCheck() - Called on each turn of the digest cycle. Provides
        > an opportunity to detect and act on changes. Any actions that
        > you wish to take in response to the changes that you detect
        > must be invoked from this hook; implementing this has no
        > effect on when \$onChanges is called. For example, this hook
        > could be useful if you wish to perform a deep equality check,
        > or to check a Date object, changes to which would not be
        > detected by Angular's change detector and thus
        > not trigger \$onChanges. This hook is invoked with no
        > arguments; if detecting changes, you must store the
        > previous value(s) for comparison to the current values.

    4.  \$onDestroy() - Called on a controller when its containing scope
        > is destroyed. Use this hook for releasing external resources,
        > watches and event handlers.

    5.  \$postLink() - Called after this controller's element and its
        > children have been linked. Similar to the post-link function
        > this hook can be used to set up DOM event handlers and do
        > direct DOM manipulation. Note that child elements that
        > containtemplateUrl directives will not have been compiled and
        > linked since they are waiting for their template to load
        > asynchronously and their own compilation and linking has been
        > suspended until that occurs. This hook can be considered
        > analogous to the ngAfterViewInit and ngAfterContentInit hooks
        > in Angular 2. Since the compilation process is rather
        > different in Angular 1 there is no direct mapping and care
        > should be taken when upgrading.

> By implementing these methods, your component can hook into its
> lifecycle.

-   **An application is a tree of components:** Ideally, the whole
    > application should be a tree of components that implement clearly
    > defined inputs and outputs, and minimize two-way data binding.
    > That way, it's easier to predict when data changes and what the
    > state of a component is.

>  
>
> Components are also useful as route templates (e.g. when
> using [ngRoute](https://docs.angularjs.org/api/ngRoute)). In a
> component-based application, every view is a component:
>
> var myMod = angular.module('myMod', \['ngRoute'\]);\
> myMod.component('home', {\
> template: '&lt;h1&gt;Home&lt;/h1&gt;&lt;p&gt;Hello, {{
> \$ctrl.user.name }} !&lt;/p&gt;',\
> controller: function() {\
> this.user = {name: 'world'};\
> }\
> });\
> myMod.config(function(\$routeProvider) {\
> \$routeProvider.when('/', {\
> template: '&lt;home&gt;&lt;/home&gt;'\
> });\
> });
>
>  
>
>  
>
> **File Organization (Also refer angular style guide**
>
>  
>
> <https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md>
>
> One Feature per File
>
>  
>
> Organizing by Feature: Well, we are going to group our files into
> directories by feature. For example, since we have a section in our
> application that lists phones, we will put all related files into a
> phone-list/ directory under app/. We are soon to find out that certain
> features are used across different parts of the application. We will
> put those inside app/core/.
>
> Other typical names for our core directory are shared, common and
> components. The last one is kind of misleading though, as it will
> contain other things than components as well.
>
>  
>
> Using Modules: Each feature/section should declare its own module and
> all related entities should register themselves on that module. Each
> feature/section, will declare its own module and have all related
> entities registered there. The main module (phonecatApp) will declare
> a dependency on each feature/section module. Now, all it takes to
> reuse the same code on a new project is copying the feature directory
> over and adding the feature module as a dependency in the new
> project's main module.
>
>  
>
> External Templates: we use the templateUrl property and specify the
> URL that our template will be loaded from.
>
> Using an external template like this, will result in more HTTP
> requests to the server (one for each external template). Although
> Angular takes care not to make extraneous requests (e.g. fetching the
> templates lazily, caching the results, etc), additional requests do
> have a cost (especially on mobile devices and data-plan connections).
>
> Luckily, there are ways to avoid the extra costs (while still keeping
> your templates external). A detailed discussion of the subject is
> outside the scope of this tutorial, but you can take a look at the
> \$templateRequest and \$templateCache services for more info on how
> Angular manages external templates.
>
>  
>
>  
>
> **Filters**
>
>  
>
>  
>
> Filters format the value of an expression for display to the user.
> They can be used in view templates, controllers or services. Angular
> comes with a collection of built-in filters, but it is easy to define
> your own as well. The underlying API is the \$filterProvider.
>
>  
>
>  
>
> Selects a subset of items from array and returns it as a new array.
>
>  
>
> Data-binding: This is one of the core features in Angular. When the
> page loads, Angular binds the value of the input box to the data model
> variable specified with ngModel and keeps the two in sync.
>
>  
>
> orderBy is a filter that takes an input array, copies it and reorders
> the copy which is then returned. You can change the sorting order by
> setting reverse to true. By default, items are sorted in ascending
> order. The comparison is done using the comparator function. If none
> is specified, a default, built-in comparator is used
>
>  
>
> Filters can be applied to expressions in view templates using the
> following syntax:
>
> {{ expression | filter }}
>
> E.g. the markup {{ 12 | currency }} formats the number 12 as a
> currency using
> the [currency](https://docs.angularjs.org/api/ng/filter/currency) filter.
> The resulting value is \$12.00.
>
> Filters can be applied to the result of another filter. This is called
> "chaining" and uses the following syntax:
>
> {{ expression | filter1 | filter2 | ... }}
>
> Filters may have arguments. The syntax for this is
>
> {{ expression | filter:argument1:argument2:... }}
>
>  
>
> In templates, filters are only executed when their inputs have
> changed. This is more performant than executing a filter on
> each [\$digest](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$digest)as
> is the case
> with [expressions](https://docs.angularjs.org/guide/expression).
>
> There are two exceptions to this rule:

-   In general, this applies only to filters that take [primitive
    > values](https://developer.mozilla.org/docs/Glossary/Primitive) as inputs.
    > Filters that
    > receive [Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Objects) as
    > input are executed on each\$digest, as it would be too costly to
    > track if the inputs have changed.

-   Filters that are marked as \$stateful are also executed on
    > each \$digest. See [Stateful
    > filters](https://docs.angularjs.org/guide/filter#stateful-filters) for
    > more information. Note that no Angular core filters
    > are \$stateful.

>  
>
> **You can also use filters in controllers, services, and directives.**
>
>  
>
> For this, inject a dependency with the name &lt;filterName&gt;Filter
> into your controller/service/directive. E.g. a filter called number is
> injected by using the dependency numberFilter. The injected argument
> is a function that takes the value to format as first argument, and
> filter parameters starting with the second argument.
>
>  
>
> The example below uses the filter called filter. This filter reduces
> arrays into sub arrays based on conditions. The filter can be applied
> in the view template with markup like {{ctrl.array | filter:'a'}},
> which would do a fulltext search for "a". However, using a filter in a
> view template will reevaluate the filter on every digest, which can be
> costly if the array is big.
>
> The example below therefore calls the filter directly in the
> controller. By this, the controller is able to call the filter only
> when needed (e.g. when the data is loaded from the backend or the
> filter expression is changed).
>
>  
>
> **Creating custom filters**
>
>  
>
> Writing your own filter is very easy: just register a new filter
> factory function with your module. Internally, this uses the
> filterProvider. This factory function should return a new filter
> function which takes the input value as the first argument. Any filter
> arguments are passed in as additional arguments to the filter
> function.
>
>  
>
> The filter function should be a pure function, which means that it
> should be stateless and idempotent, and not rely for example on other
> Angular services. Angular relies on this contract and will by default
> execute a filter only when the inputs to the function change. Stateful
> filters are possible, but less performant.
>
>  
>
> It is strongly discouraged to write filters that are stateful, because
> the execution of those can't be optimized by Angular, which often
> leads to performance issues. Many stateful filters can be converted
> into stateless filters just by exposing the hidden state as a model
> and turning it into an argument for the filter. If you however do need
> to write a stateful filter, you have to mark the filter as \$stateful,
> which means that it will be executed one or more times during the each
> \$digest cycle.
>
>  
>
>  
>
> **Custom Filer**
>
>  
>
> angular.\
> module('core').\
> filter('checkmark', function() {\
> return function(input) {\
> return input ? '\\u2713' : '\\u2718';\
> };\
> });
>
>  
>
> The name of our filter is "checkmark". The input evaluates to either
> true or false, and we return one of the two unicode characters we have
> chosen to represent true (\\u2713 -&gt; ✓) and false (\\u2718 -&gt;
> ✘).
>
>  
>
> Now that our filter is ready, we need to register the core module as a
> dependency of our main phonecatApp module.
>
>  
>
> angular.module('phonecatApp', \[\
> ...\
> 'core',\
> ...\
> \]);
>
>  
>
>  
>
> **Forms**
>
>  
>
> Controls (input, select, textarea) are ways for a user to enter data.
> A Form is a collection of controls for the purpose of grouping related
> controls together.
>
>  
>
> Form and controls provide validation services, so that the user can be
> notified of invalid input before submitting a form. This provides a
> better user experience than server-side validation alone because the
> user gets instant feedback on how to correct the error. Keep in mind
> that while client-side validation plays an important role in providing
> good user experience, it can easily be circumvented and thus can not
> be trusted. Server-side validation is still necessary for a secure
> application.
>
>  
>
>  
>
> The key directive in understanding two-way data-binding is ngModel.
> The ngModel directive provides the two-way data-binding by
> synchronizing the model to the view, as well as view to the model. In
> addition it provides an API for other directives to augment its
> behavior.
>
> Note that novalidate is used to disable browser's native form
> validation.
>
> To allow styling of form as well as controls, ngModel adds these CSS
> classes:

-   ng-valid: the model is valid

-   ng-invalid: the model is invalid

-   ng-valid-\[key\]: for each valid key added by \$setValidity

-   ng-invalid-\[key\]: for each invalid key added by \$setValidity

-   ng-pristine: the control hasn't been interacted with yet

-   ng-dirty: the control has been interacted with

-   ng-touched: the control has been blurred

-   ng-untouched: the control hasn't been blurred

-   ng-pending: any \$asyncValidators are unfulfilled

>  
>
>  
>
> ***Binding to form and control state***
>
>  
>
> A form is an instance
> of [FormController](https://docs.angularjs.org/api/ng/type/form.FormController).
> The form instance can optionally be published into the scope using
> the name attribute.
>
> Similarly, an input control that has
> the [ngModel](https://docs.angularjs.org/api/ng/directive/ngModel) directive
> holds an instance
> of [NgModelController](https://docs.angularjs.org/api/ng/type/ngModel.NgModelController).
> Such a control instance can be published as a property of the form
> instance using the name attribute on the input control. The name
> attribute specifies the name of the property on the form instance.
>
> This implies that the internal state of both the form and the control
> is available for binding in the view using the standard binding
> primitives.
>
> This allows us to extend the above example with these features:

-   Custom error message displayed after the user interacted with a
    > control (i.e. when \$touched is set)

-   Custom error message displayed upon submitting the form
    > (\$submitted is set), even if the user didn't interact with a
    > control

>  
>
> By default, any change to the content will trigger a model update and
> form validation. You can override this behavior using the
> ngModelOptions directive to bind only to specified list of events.
> I.e. ng-model-options="{ updateOn: 'blur' }" will update and validate
> only after the control loses focus. You can set several events using a
> space delimited list. I.e. ng-model-options="{ updateOn: 'mousedown
> blur' }"
>
>  
>
> If you want to keep the default behavior and just add new events that
> may trigger the model update and validation, add "default" as one of
> the specified events.
>
>  
>
> You can delay the model update/validation by using the debounce key
> with the ngModelOptions directive. This delay will also apply to
> parsers, validators and model flags like \$dirty or \$pristine.
>
>  
>
> I.e. ng-model-options="{ debounce: 500 }" will wait for half a second
> since the last content change before triggering the model update and
> form validation.
>
> If custom triggers are used, custom debouncing timeouts can be set for
> each event using an object in debounce. This can be useful to force
> immediate updates on some specific circumstances (like blur events).
>
> I.e. ng-model-options="{ updateOn: 'default blur', debounce: {
> default: 500, blur: 0 } }"
>
> If those attributes are added to an element, they will be applied to
> all the child elements and controls that inherit from it unless they
> are overridden.
>
>  
>
> ***Custom Validation***
>
>  
>
> With a custom directive, you can add your own validation functions to
> the \$validators object on the ngModelController. To get a hold of the
> controller, you require it in the directive as shown in the example
> below.
>
>  
>
> Each function in the \$validators object receives the modelValue and
> the viewValue as parameters. Angular will then call \$setValidity
> internally with the function's return value (true: valid, false:
> invalid). The validation functions are executed every time an input is
> changed (\$setViewValue is called) or whenever the bound model
> changes. Validation happens after successfully running \$parsers and
> \$formatters, respectively. Failed validators are stored by key in
> ngModelController.\$error.
>
>  
>
> Additionally, there is the \$asyncValidators object which handles
> asynchronous validation, such as making an \$http request to the
> backend. Functions added to the object must return a promise that must
> be resolved when valid or rejected when invalid. In-progress async
> validations are stored by key in ngModelController.\$pending.
>
>  
>
>  
>
>  
>
> **Event Handler**
>
>  
>
> We also registered an ngClick handler with thumbnail images. When a
> user clicks on one of the thumbnail images, the handler will use the
> \$ctrl.setImage() method callback to change the value of the
> \$ctrl.mainImageUrl property to the URL of the clicked thumbnail
> image.
>
>  
>
> **Animations**
>
>  
>
> The animation functionality is provided by Angular in the ngAnimate
> module, which is distributed separately from the core Angular
> framework. In addition we can use jQuery
>
>  
>
> AngularJS provides animation hooks for common directives such as
> ngRepeat, ngSwitch, and ngView, as well as custom directives via the
> \$animate service. These animation hooks are set in place to trigger
> animations during the life cycle of various directives and when
> triggered, will attempt to perform a CSS Transition, CSS Keyframe
> Animation or a JavaScript callback Animation (depending on if an
> animation is placed on the given directive). Animations can be placed
> using vanilla CSS by following the naming conventions set in place by
> AngularJS or with JavaScript code when it's defined as a factory.
>
>  
>
> Animations in AngularJS are completely based on CSS classes. As long
> as you have a CSS class attached to a HTML element within your
> website, you can apply animations to it. Lets say for example that we
> have an HTML template with a repeater in it like so:
>
>  
>
> &lt;div ng-repeat="item in items" class="repeated-item"&gt;
>
> {{ item.id }}
>
> &lt;/div&gt;
>
> As you can see, the .repeated-item class is present on the element
> that will be repeated and this class will be used as a reference
> within our application's CSS and/or JavaScript animation code to tell
> AngularJS to perform an animation.
>
> As ngRepeat does its thing, each time a new item is added into the
> list, ngRepeat will add a ng-enter class name to the element that is
> being added. When removed it will apply a ng-leave class name and when
> moved around it will apply a ng-move class name.
>
>  
>
> AngularJS also pays attention to CSS class changes on elements by
> triggering the add and remove hooks. This means that if a CSS class is
> added to or removed from an element then an animation can be executed
> in between, before the CSS class addition or removal is finalized.
> (Keep in mind that AngularJS will only be able to capture class
> changes if an expression or the ng-class directive is used on the
> element.)
>
>  
>
> A handful of common AngularJS directives support and trigger animation
> hooks whenever any major event occurs during its life cycle. The table
> below explains in detail which animation events are triggered
>
>  

  **Directive        **     **Supported Animations**
  ------------------------- ------------------------------------------
  ngRepeat                  enter, leave, and move
  ngView                            enter and leave
  ngInclude                 enter and leave
  ngSwitch                  enter and leave
  ngIf                      enter and leave
  ngClass or                add and remove
  ngShow & ngHide           add and remove (the ng-hide class value)

>  
>
> Animations within custom directives can also be established by
> injecting \$animate directly into your directive and making calls to
> it when needed.
>
> myModule.directive('my-directive', \['\$animate', function(\$animate)
> {\
> return function(scope, element, attrs) {\
> element.on('click', function() {\
> if(element.hasClass('clicked')) {\
> \$animate.removeClass(element, 'clicked');\
> } else {\
> \$animate.addClass(element, 'clicked');\
> }\
> });\
> };\
> }\]);
>
>  
>
>  
>
> By default, animations are disabled when the Angular app bootstraps.
> If you are using the ngApp directive, this happens in the
> DOMContentLoaded event, so immediately after the page has been loaded.
> Animations are disabled, so that UI and content are instantly visible.
> Otherwise, with many animations on the page, the loading process may
> become too visually overwhelming, and the performance may suffer.
>
>  
>
> Internally, ngAnimate waits until all template downloads that are
> started right after bootstrap have finished. Then, it waits for the
> currently running \$rootScope.Scope and the one after that to finish.
> This ensures that the whole app has been compiled fully before
> animations are attempted.
>
>  
>
>  
>
>  
>
> **Two way Data Binding**
>
>  
>
> Notice that when the application is loaded in the browser, "Newest" is
> selected in the drop-down menu. This is because we set orderProp to
> 'age' in the controller. So the binding works in the direction from
> our model to the UI. Now if you select "Alphabetically" in the
> drop-down menu, the model will be updated as well and the phones will
> be reordered. That is the data-binding doing its job in the opposite
> direction — from the UI to the model.
>
>  
>
> Data-binding in Angular apps is the automatic synchronization of data
> between the model and view components. The way that Angular implements
> data-binding lets you treat the model as the single-source-of-truth in
> your application. The view is a projection of the model at all times.
> When the model changes, the view reflects the change, and vice versa.
>
>  
>
> Angular templates work differently. First the template (which is the
> uncompiled HTML along with any additional markup or directives) is
> compiled on the browser. The compilation step produces a live view.
> Any changes to the view are immediately reflected in the model, and
> any changes in the model are propagated to the view. The model is the
> single-source-of-truth for the application state, greatly simplifying
> the programming model for the developer. You can think of the view as
> simply an instant projection of your model.
>
> Because the view is just a projection of the model, the controller is
> completely separated from the view and unaware of it. This makes
> testing a snap because it is easy to test your controller in isolation
> without the view and the related DOM/browser dependency.
>
>  
>
>  
>
> **Services**
>
> Angular services are substitutable objects that are wired together
> using dependency injection (DI). You can use services to organize and
> share code across your app.
>
>  
>
> Angular services are:
>
>  

-   Lazily instantiated – Angular only instantiates a service when an
    > application component depends on it.

-   Singletons – Each component dependent on a service gets a reference
    > to the single instance generated by the service factory.

>  
>
> To use an Angular service, you add it as a dependency for the
> component (controller, service, filter or directive) that depends on
> the service. Angular's dependency injection subsystem takes care of
> the rest.
>
>  
>
> Application developers are free to define their own services by
> registering the service's name and service factory function, with an
> Angular module. The service factory function generates the single
> object or function that represents the service to the rest of the
> application. The object or function returned by the service is
> injected into any component (controller, service, filter or directive)
> that specifies a dependency on the service.
>
>  
>
> Services are registered to modules via the Module API. Typically you
> use the Module factory API to register a service:
>
>  
>
> Services can have their own dependencies. Just like declaring
> dependencies in a controller, you declare dependencies by specifying
> them in the service's factory function signature.
>
>  
>
> The \$ prefix is there to namespace Angular-provided services. To
> prevent collisions it's best to avoid naming your services and models
> anything that begins with a \$. If you inspect a Scope, you may also
> notice some properties that begin with \$\$. These properties are
> considered private, and should not be accessed or modified.
>
>  
>
> ***Minimification ***
>
>  
>
> Since Angular infers the controller's dependencies from the names of
> arguments to the controller's constructor function, if you were
> to[minify](https://en.wikipedia.org/wiki/Minification_(programming)) the
> JavaScript code for the PhoneListController controller, all of its
> function arguments would be minified as well, and the dependency
> injector would not be able to identify services correctly.
>
> We can overcome this problem by annotating the function with the names
> of the dependencies, provided as strings, which will not get minified.
> There are two ways to provide these injection annotations:

-   Create an \$inject property on the controller function which holds
    > an array of strings. Each string in the array is the name of the
    > service to inject for the corresponding parameter

-   Use an inline annotation where, instead of just providing the
    > function, you provide an array. This array contains a list of the
    > service names, followed by the function itself as the last item of
    > the array.

>  
>
>  
>
>  
>
>  
>
> **Routing**
>
>  
>
> The routing functionality added in this step is provided by Angular in
> the ngRoute module, which is distributed separately from the core
> Angular framework.
>
>  
>
> To add the detailed view, we are going to turn index.html into what we
> call a "layout template". This is a template that is common for all
> views in our application. Other "partial templates" are then included
> into this layout template depending on the current "route" — the view
> that is currently displayed to the user. Application routes in Angular
> are declared via the \$routeProvider, which is the provider of the
> \$route service. This service makes it easy to wire together
> controllers, view templates, and the current URL location in the
> browser. Using this feature, we can implement deep linking, which lets
> us utilize the browser's history (back and forward navigation) and
> bookmarks.
>
>  
>
>  
>
> A
> module's [.config()](https://docs.angularjs.org/api/ng/type/angular.Module#config) method
> gives us access to the available providers for configuration. To make
> the providers, services and directives defined in ngRoute available to
> our application, we need to add ngRoute as a dependency of
> our phonecatApp module.
>
>  
>
> **app/app.module.js:**
>
> angular.module('phonecatApp', \[\
> 'ngRoute',\
> ...\
> \]);
>
>  
>
> angular.\
> module('phonecatApp').\
> config(\['\$locationProvider', '\$routeProvider',\
> function config(\$locationProvider, \$routeProvider) {\
> \$locationProvider.hashPrefix('!');
>
> \$routeProvider.\
> when('/phones', {\
> template: '&lt;phone-list&gt;&lt;/phone-list&gt;'\
> }).
>
>  
>
> when('/phones'): Determines the view that will be shown, when the URL
> hash fragment is /phones. According to the specified template, Angular
> will create an instance of the phoneList component to manage the view.
> Note that this is the same markup that we used to have in the
> index.html file.
>
>  
>
> when('/phones/:phoneId'): Determines the view that will be shown, when
> the URL hash fragment matches /phones/&lt;phoneId&gt;, where
> &lt;phoneId&gt; is a variable part of the URL. In charge of the view
> will be the phoneDetail component.
>
>  
>
> otherwise('/phones'): Defines a fallback route to redirect to, when no
> route definition matches the current URL.(Here it will redirect to
> /phones.)
>
>  
>
> *Always be explicit about the dependecies of a sub-module. Do not rely
> on dependencies inherited from a parent module (because that parent
> module might not be there some day). Declaring the same dependency in
> multiple modules does not incur extra "cost", because Angular will
> still load each dependency once*
>
>  
>
>  
>
>  
>
>  
>
> **Directives**
>
>  
>
> At a high level, directives are markers on a DOM element (such as an
> attribute, element name, comment or CSS class) that tell AngularJS's
> HTML compiler (\$compile) to attach a specified behavior to that DOM
> element (e.g. via event listeners), or even to transform the DOM
> element and its children. Angular comes with a set of these directives
> built-in, like ngBind, ngModel, and ngClass. Much like you create
> controllers and services, you can create your own directives for
> Angular to use. When Angular bootstraps your application, the HTML
> compiler traverses the DOM matching directives against the DOM
> elements.
>
>  
>
> **What does it mean to "compile" an HTML template?** For AngularJS,
> "compilation" means attaching directives to the HTML to make it
> interactive. The reason we use the term "compile" is that the
> recursive process of attaching directives mirrors the process of
> compiling source code in [compiled programming
> languages](http://en.wikipedia.org/wiki/Compiled_languages).
>
>  
>
>  
>
>  
>
>  

-   **Ngsrc** : That directive prevents the browser from treating the
    > Angular {{ expression }} markup literally, and initiating a
    > request to an invalid URL
    > ([http://localhost:8000/{{phone.imageUrl}}](http://localhost:8000/%7b%7bphone.imageUrl%7d%7d)),
    > which it would have done if we had only specified an attribute
    > binding in a regular src attribute
    > (&lt;img src="{{phone.imageUrl}}"&gt;). Using the ngSrc directive,
    > prevents the browser from making an HTTP request to an
    > invalid location.

>  

-   **ngView** is a directive that complements the \$route service by
    > including the rendered template of the current route into the main
    > layout (index.html) file. Every time the current route changes,
    > the included view changes with it according to the configuration
    > of the \$route service.

>  
>
> Requires the ngRoute module to be installed.
>
>  
>
> **Matching Directives**
>
>  
>
> we need to know how Angular's [HTML
> compiler](https://docs.angularjs.org/guide/compiler) determines when
> to use a given directive. Similar to the terminology used when
> an [element **matches** a
> selector](https://developer.mozilla.org/en-US/docs/Web/API/Element.matches),
> we say an element **matches** a directive when the directive is part
> of its declaration.
>
> In the following example, we say that
> the &lt;input&gt; element **matches** the ngModel directive
>
> &lt;input ng-model="foo"&gt;
>
> The following &lt;input&gt; element also **matches** ngModel:
>
> &lt;input data-ng-model="foo"&gt;
>
> And the following element **matches** the person directive:
>
> &lt;person&gt;{{name}}&lt;/person&gt;
>
>  
>
> **Normalization**
>
>  
>
> Angular **normalizes** an element's tag and attribute name to
> determine which elements match which directives. We typically refer to
> directives by their
> case-sensitive [camelCase](http://en.wikipedia.org/wiki/CamelCase) **normalized** name
> (e.g. ngModel). However, since HTML is case-insensitive, we refer to
> directives in the DOM by lower-case forms, typically
> using [dash-delimited](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles) attributes
> on DOM elements (e.g. ng-model).
>
> The **normalization** process is as follows:

1.  Strip x- and data- from the front of the element/attributes.

2.  Convert the :, -, or \_-delimited name to camelCase.

>  
>
> **Directive types**
>
>  
>
> \$compile can match directives based on element names, attributes,
> class names, as well as comments. All of the Angular-provided
> directives match attribute name, tag name, comments, or class name.
>
>  
>
> **Best Practice:** Prefer using directives via tag name and attributes
> over comment and class names. Doing so generally makes it easier to
> determine what directives a given element matches.
>
>  
>
> **Creating Directives**
>
>  
>
> Much like controllers, directives are registered on modules. To
> register a directive, you use the module.directive API.
> module.directive takes the normalized directive name followed by a
> factory function. This factory function should return an object with
> the different options to tell \$compile how the directive should
> behave when matched.
>
> The factory function is invoked only once when the compiler matches
> the directive for the first time. You can perform any initialization
> work here. The function is invoked using \$injector.invoke which makes
> it injectable just like a controller.
>
>  
>
> Best Practice: In order to avoid collisions with some future standard,
> it's best to prefix your own directive names. For instance, if you
> created a &lt;carousel&gt; directive, it would be problematic if HTML7
> introduced the same element. A two or three letter prefix (e.g.
> btfCarousel) works well. Similarly, do not prefix your own directives
> with ng or they might conflict with directives included in a future
> version of Angular.
>
>  
>
> Check below link for examples on creating directives
>
>  
>
> **HTML Compiler**
>
>  
>
> Angular's HTML compiler allows the developer to teach the browser new
> HTML syntax. The compiler allows you to attach behavior to any HTML
> element or attribute and even create new HTML elements or attributes
> with custom behavior. Angular calls these behavior extensions
> directives.
>
> Angular comes pre-bundled with common directives which are useful for
> building any app. We also expect that you will create directives that
> are specific to your app. These extensions become a Domain Specific
> Language for building your application.
>
> All of this compilation takes place in the web browser; no server side
> or pre-compilation step is involved.
>
> **Compiler**
>
> Compiler is an Angular service which traverses the DOM looking for
> attributes. The compilation process happens in two phases.

1.  **Compile:** traverse the DOM and collect all of the directives. The
    > result is a linking function.

2.  **Link:** combine the directives with a scope and produce a
    > live view. Any changes in the scope model are reflected in the
    > view, and any user interactions with the view are reflected in the
    > scope model. This makes the scope model the single source
    > of truth.

> Some directives such
> as [ng-repeat](https://docs.angularjs.org/api/ng/directive/ngRepeat) clone
> DOM elements once for each item in a collection. Having a compile and
> link phase improves performance since the cloned template only needs
> to be compiled once, and then linked once for each clone instance.
>
>  
>
> **Directive**
>
>  
>
> A directive is a behavior which should be triggered when specific HTML
> constructs are encountered during the compilation process. The
> directives can be placed in element names, attributes, class names, as
> well as comments. A directive is just a function which executes when
> the compiler encounters it in the DOM
>
>  
>
> Angular is different. The Angular compiler consumes the DOM, not
> string templates. The result is a linking function, which when
> combined with a scope model results in a live view. The view and scope
> model bindings are transparent. The developer does not need to make
> any special calls to update the view. And because innerHTML is not
> used, you won't accidentally clobber user input. Furthermore, Angular
> directives can contain not just text bindings, but behavioral
> constructs as well.
>
>  
>
> ![](media/image6.png){width="4.510416666666667in" height="3.125in"}
>
>  
>
> The Angular approach produces a stable DOM. The DOM element instance
> bound to a model item instance does not change for the lifetime of the
> binding. This means that the code can get hold of the elements and
> register event handlers and know that the reference will not be
> destroyed by template data merge.
>
>  
>
> **How directives are compiled**
>
>  
>
> It's important to note that Angular operates on DOM nodes rather than
> strings. Usually, you don't notice this restriction because when a
> page loads, the web browser parses HTML into the DOM automatically.
>
> HTML compilation happens in three phases:

1.  [\$compile](https://docs.angularjs.org/api/ng/service/$compile) traverses
    > the DOM and matches directives.\
    > If the compiler finds that an element matches a directive, then
    > the directive is added to the list of directives that match the
    > DOM element. A single element may match multiple directives.

<!-- -->

1.  Once all directives matching a DOM element have been identified, the
    > compiler sorts the directives by their priority.\
    > Each directive's compile functions are executed.
    > Each compile function has a chance to modify the DOM.
    > Each compilefunction returns a link function. These functions are
    > composed into a "combined" link function, which invokes each
    > directive's returned link function.

<!-- -->

1.  \$compile links the template with the scope by calling the combined
    > linking function from the previous step. This in turn will call
    > the linking function of the individual directives, registering
    > listeners on the elements and setting
    > up [\$watchs](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$watch) with
    > the [scope](https://docs.angularjs.org/api/ng/type/$rootScope.Scope) as
    > each directive is configured to do.

> The result of this is a live binding between the scope and the DOM. So
> at this point, a change in a model on the compiled scope will be
> reflected in the DOM.
>
> *"Compile" Versus "Link"*
>
> To understand, let's look at a real-world example with ngRepeat:
>
> Hello {{user.name}}, you have these actions:\
> &lt;ul&gt;\
> &lt;li ng-repeat="action in user.actions"&gt;\
> {{action.description}}\
> &lt;/li&gt;\
> &lt;/ul&gt;
>
> When the above example is compiled, the compiler visits every node and
> looks for directives.{{user.name}} matches the [interpolation
> directive](https://docs.angularjs.org/api/ng/service/$interpolate) and ng-repeat matches
> the [ngRepeat directive](https://docs.angularjs.org/api/ng/directive/ngRepeat).
>
> But [ngRepeat](https://docs.angularjs.org/api/ng/directive/ngRepeat) has
> a dilemma.It needs to be able to clone new &lt;li&gt; elements for
> every action in user.actions. This initially seems trivial, but it
> becomes more complicated when you consider that user.actions might
> have items added to it later. This means that it needs to save a clean
> copy of the &lt;li&gt; element for cloning purposes.
>
> As new actions are inserted, the template &lt;li&gt; element needs to
> be cloned and inserted into ul. But cloning the &lt;li&gt; element is
> not enough. It also needs to compile the &lt;li&gt; so that its
> directives, like {{action.description}}, evaluate against the
> right [scope](https://docs.angularjs.org/api/ng/type/$rootScope.Scope).
>
>  
>
> A naive approach to solving this problem would be to simply insert a
> copy of the &lt;li&gt; element and then compile it. The problem with
> this approach is that compiling on every &lt;li&gt; element that we
> clone would duplicate a lot of the work. Specifically, we'd be
> traversing &lt;li&gt;each time before cloning it to find the
> directives. This would cause the compilation process to be slower, in
> turn making applications less responsive when inserting new nodes.
>
>  
>
> The solution is to break the compilation process into two phases:
>
> the compile phase where all of the directives are identified and
> sorted by priority, and a linking phase where any work which "links" a
> specific instance of
> the [scope](https://docs.angularjs.org/api/ng/type/$rootScope.Scope) and
> the specific instance of an &lt;li&gt; is performed.
>
> **Note:** *Link* means setting up listeners on the DOM and setting
> up \$watch on the Scope to keep the two in sync.
>
> [ngRepeat](https://docs.angularjs.org/api/ng/directive/ngRepeat) works
> by preventing the compilation process from descending into
> the &lt;li&gt; element so it can make a clone of the original and
> handle inserting and removing DOM nodes itself. Instead
> the [ngRepeat](https://docs.angularjs.org/api/ng/directive/ngRepeat) directive
> compiles &lt;li&gt; separately. The result of the &lt;li&gt; element
> compilation is a linking function which contains all of the directives
> contained in the &lt;li&gt; element, ready to be attached to a
> specific clone of the &lt;li&gt; element.
>
> At runtime
> the [ngRepeat](https://docs.angularjs.org/api/ng/directive/ngRepeat) watches
> the expression and as items are added to the array it clones
> the &lt;li&gt; element, creates a
> new [scope](https://docs.angularjs.org/api/ng/type/$rootScope.Scope)for
> the cloned &lt;li&gt; element and calls the link function on the
> cloned &lt;li&gt;.
>
>  
>
> **Providers**
>
>  
>
> Each web application you build is composed of objects that collaborate
> to get stuff done. These objects need to be instantiated and wired
> together for the app to work. In Angular apps most of these objects
> are instantiated and wired together automatically by the injector
> service.
>
> The injector creates two types of objects, services and specialized
> objects.
>
> Services are objects whose API is defined by the developer writing the
> service. Specialized objects conform to a specific Angular framework
> API. These objects are one of controllers, directives, filters or
> animations.The injector needs to know how to create these objects. You
> tell it by registering a "recipe" for creating your object with the
> injector. There are five recipe types.
>
>  
>
> The most verbose, but also the most comprehensive one is a Provider
> recipe. The remaining four recipe types — Value, Factory, Service and
> Constant — are just syntactic sugar on top of a provider recipe.
>
>  

1.  **Value Recipe**

>  
>
> Let's say that we want to have a very simple service called "clientId"
> that provides a string representing an authentication id used for some
> remote API. You would define it like this:
>
> var myApp = angular.module('myApp', \[\]);\
> myApp.value('clientId', 'a12345654321x');
>
>  
>
> And this is how you would display it via Angular's data-binding:
>
> myApp.controller('DemoController', \['clientId', function
> DemoController(clientId) {\
> this.clientId = clientId;\
> }\]);
>
> &lt;html ng-app="myApp"&gt;\
> &lt;body ng-controller="DemoController as demo"&gt;\
> Client ID: {{demo.clientId}}\
> &lt;/body&gt;\
> &lt;/html&gt;
>
> In this example, we've used the Value recipe to define the value to
> provide when DemoController asks for the service with id "clientId".
>
>  
>
>  

1.  **Factory Recipe**

>  
>
>  The Factory recipe adds the following abilities:

-   ability to use other services (have dependencies)

-   service initialization

-   delayed/lazy initialization

> The Factory recipe constructs a new service using a function with zero
> or more arguments (these are dependencies on other services). The
> return value of this function is the service instance created by this
> recipe.
>
> **Note: All services in Angular are singletons. That means that the
> injector uses each recipe at most once to create the object. The
> injector then caches the reference for all future needs.**
>
> Since a Factory is a more powerful version of the Value recipe, the
> same service can be constructed with it. Using our
> previous clientIdValue recipe example, we can rewrite it as a Factory
> recipe like this:
>
>  
>
> myApp.factory('clientId', function clientIdFactory() {\
> return 'a12345654321x';\
> });
>
>  
>
>  
>
> Let's say, however, that we would also like to create a service that
> computes a token used for authentication against a remote API. This
> token will be called apiToken and will be computed based on
> the clientId value and a secret stored in the browser's local storage:
>
> myApp.factory('apiToken', \['clientId', function
> apiTokenFactory(clientId) {\
> var encrypt = function(data1, data2) {\
> // NSA-proof encryption algorithm:\
> return (data1 + ':' + data2).toUpperCase();\
> };
>
> var secret = window.localStorage.getItem('myApp.secret');\
> var apiToken = encrypt(clientId, secret);
>
> return apiToken;\
> }\]);
>
> In the code above, we see how the apiToken service is defined via the
> Factory recipe that depends on the clientId service. The factory
> service then uses NSA-proof encryption to produce an authentication
> token.
>
>  

-   **Service Recipe**

>  
>
> The Service recipe produces a service just like the Value or Factory
> recipes, but it does so by invoking a constructor with the new
> operator. The constructor can take zero or more arguments, which
> represent dependencies needed by the instance of this type.
>
>  
>
> Note: Service recipes follow a design pattern called constructor
> injection.
>
>  
>
> function UnicornLauncher(apiToken) {
>
> this.launchedCount = 0;\
> this.launch = function() {\
> // Make a request to the remote API and include the apiToken\
> ...\
> this.launchedCount++;\
> }\
> }
>
>  
>
> Since we already have a constructor for our UnicornLauncher type, we
> can replace the Factory recipe above with a Service recipe like this:
>
> myApp.service('unicornLauncher', \["apiToken", UnicornLauncher\]);
>
> Much simpler!
>
>  

1.  **Provider Recipe**

>  
>
> the Provider recipe is the core recipe type and all the other recipe
> types are just syntactic sugar on top of it. It is the most verbose
> recipe with the most abilities, but for most services it's overkill.
> The Provider recipe is syntactically defined as a custom type that
> implements a \$get method. This method is a factory function just like
> the one we use in the Factory recipe. In fact, if you define a Factory
> recipe, an empty Provider type with the \$get method set to your
> factory function is automatically created under the hood.
>
> You should use the Provider recipe only when you want to expose an API
> for application-wide configuration that must be made before the
> application starts. This is usually interesting only for reusable
> services whose behavior might need to vary slightly between
> applications.
>
>  

1.  **Constant Recipe**

>  
>
> Since the config function runs in the configuration phase when no
> services are available, it doesn't have access even to simple value
> objects created via the Value recipe. Since simple values, like URL
> prefixes, don't have dependencies or configuration, it's often handy
> to make them available in both the configuration and run phases. This
> is what the Constant recipe is for.
>
>  
>
> myApp.constant('planetName', 'Greasy Giant');
>
>  
>
> myApp.config(\['unicornLauncherProvider', 'planetName',
> function(unicornLauncherProvider, planetName) {\
> unicornLauncherProvider.useTinfoilShielding(true);\
> unicornLauncherProvider.stampText(planetName);\
> }\]);
>
>  
>
> And since Constant recipe makes the value also available at runtime
> just like the Value recipe, we can also use it in our controller and
> template:
>
> myApp.controller('DemoController', \["clientId", "planetName",
> function DemoController(clientId, planetName) {\
> this.clientId = clientId;\
> this.planetName = planetName;\
> }\]);
>
> &lt;html ng-app="myApp"&gt;\
> &lt;body ng-controller="DemoController as demo"&gt;\
> Client ID: {{demo.clientId}}\
> &lt;br&gt;\
> Planet Name: {{demo.planetName}}\
> &lt;/body&gt;\
> &lt;/html&gt;
>
>  
>
> **Special Purpose Objects**
>
>  
>
> Earlier we mentioned that we also have special purpose objects that
> are different from services. These objects extend the framework as
> plugins and therefore must implement interfaces specified by Angular.
> These interfaces are Controller, Directive, Filter and Animation.
>
> The instructions for the injector to create these special objects
> (with the exception of the Controller objects) use the Factory recipe
> behind the scenes.
>
>  
>
> To wrap it up, let's summarize the most important points:

-   The injector uses recipes to create two types of objects: services
    > and special purpose objects

-   There are five recipe types that define how to create objects:
    > Value, Factory, Service, Provider and Constant.

-   Factory and Service are the most commonly used recipes. The only
    > difference between them is that the Service recipe works better
    > for objects of a custom type, while the Factory can produce
    > JavaScript primitives and functions.

-   The Provider recipe is the core recipe type and all the other ones
    > are just syntactic sugar on it.

-   Provider is the most complex recipe type. You don't need it unless
    > you are building a reusable piece of code that needs
    > global configuration.

-   All special purpose objects except for the Controller are defined
    > via Factory recipes.

>  
>
> ![](media/image7.png){width="9.770833333333334in"
> height="2.3854166666666665in"}
>
>  
>
> **Bootstrap**
>
>  
>
> **Angular &lt;script&gt; Tag**
>
>  

-   Place the script tag at the bottom of the page. Placing script tags
    > at the end of the page improves app load time because the HTML
    > loading is not blocked by loading of the angular.js script. You
    > can get the latest bits
    > from [http://code.angularjs.org](http://code.angularjs.org/).
    > Please don't link your production code to this URL, as it will
    > expose a security hole on your site. For experimental development
    > linking to our site is fine.

    -   Choose: angular-\[version\].js for a human-readable file,
        > suitable for development and debugging.

    -   Choose: angular-\[version\].min.js for a compressed and
        > obfuscated file, suitable for use in production.

-   Place ng-app to the root of your application, typically on
    > the &lt;html&gt; tag if you want angular to auto-bootstrap
    > your application.

-   If you choose to use the old style directive syntax ng: then include
    > xml-namespace in html to make IE happy. (This is here for
    > historical reasons, and we no longer recommend use of ng:.)

>  
>
> Angular initializes automatically upon DOMContentLoaded event or when
> theangular.js script is evaluated if at that
> time document.readyState is set to'complete'. At this point Angular
> looks for
> the [ngApp](https://docs.angularjs.org/api/ng/directive/ngApp) directive
> which designates your application root. If
> the [ngApp](https://docs.angularjs.org/api/ng/directive/ngApp) directive
> is found then Angular will:

-   load
    > the [module](https://docs.angularjs.org/guide/module) associated
    > with the directive.

-   create the
    > application [injector](https://docs.angularjs.org/api/auto/service/$injector)

-   compile the DOM treating
    > the [ngApp](https://docs.angularjs.org/api/ng/directive/ngApp) directive
    > as the root of the compilation. This allows you to tell it to
    > treat only a portion of the DOM as an Angular application.

>  
>
>  
>
> As a best practice, consider adding an ng-strict-di directive on the
> same element as ng-app: This will ensure that all services in your
> application are properly annotated
>
>  
>
> **Unit Testing**
>
>  
>
> Unit testing, as the name implies, is about testing individual units
> of code. Unit tests try to answer questions such as "Did I think about
> the logic correctly?" or "Does the sort function order the list in the
> right order?"
>
> In order to answer such a question it is very important that we can
> isolate the unit of code under test. That is because when we are
> testing the sort function we don't want to be forced into creating
> related pieces such as the DOM elements, or making any XHR calls to
> fetch the data to sort.
>
>  
>
> While this may seem obvious it can be very difficult to call an
> individual function on a typical project. The reason is that the
> developers often mix concerns resulting in a piece of code which does
> everything. It makes an XHR request, it sorts the response data, and
> then it manipulates the DOM.
>
> With Angular, we try to make it easy for you to do the right thing.
> For your XHR requests, we provide dependency injection, so your
> requests can be simulated. For the DOM, we abstract it, so you can
> test your model without having to manipulate the DOM directly. Your
> tests can then assert that the data has been sorted without having to
> create or look at the state of the DOM or to wait for any XHR requests
> to return data. The individual sort function can be tested in
> isolation.
>
>  
>
> Angular comes with dependency injection built-in, which makes testing
> components much easier, because you can pass in a component's
> dependencies and stub or mock them as you wish.
>
> Components that have their dependencies injected allow them to be
> easily mocked on a test by test basis, without having to mess with any
> global variables that could inadvertently affect another test.
>
>  
>
> **Karma** : Karma is a JavaScript command line tool that can be used
> to spawn a web server which loads your application's source code and
> executes your tests. You can configure Karma to run against a number
> of browsers, which is useful for being confident that your application
> works on all browsers you need to support. Karma is executed on the
> command line and will display the results of your tests on the command
> line once they have run in the browser. Karma is a NodeJS application,
> and should be installed through npm
>
>  
>
> **Jasmine**: Jasmine is a behavior driven development framework for
> JavaScript that has become the most popular choice for testing Angular
> applications. Jasmine provides functions to help with structuring your
> tests and also making assertions. As your tests grow, keeping them
> well structured and documented is vital, and Jasmine helps achieve
> this
>
>  
>
> **angular**-**mocks** :Angular also provides the ngMock module, which
> provides mocking for your tests. This is used to inject and mock
> Angular services within unit tests. In addition, it is able to extend
> other modules so they are synchronous. Having tests synchronous keeps
> them much cleaner and easier to work with. One of the most useful
> parts of ngMock is \$httpBackend, which lets us mock XHR requests in
> tests, and return sample data instead.
>
>  
>
>  
>
> See
> the [angular-seed](https://github.com/angular/angular-seed) project
> for an example.
>
>  
>
> From &lt;<https://docs.angularjs.org/guide/unit-testing>&gt;
>
>  
>
>  
>
> **E2E Testing**
>
>  
>
> As applications grow in size and complexity, it becomes unrealistic to
> rely on manual testing to verify the correctness of new features,
> catch bugs and notice regressions. Unit tests are the first line of
> defense for catching bugs, but sometimes issues come up with
> integration between components which can't be captured in a unit test.
> End-to-end tests are made to find these problems.
>
>  
>
> **Protractor** is a Node.js program, and runs end-to-end tests that
> are also written in JavaScript and run with node. Protractor uses
> WebDriver to control browsers and simulate user actions.
>
>  
>
> Protractor uses Jasmine for its test syntax. As in unit testing, a
> test file is comprised of one or more it blocks that describe the
> requirements of your application. it blocks are made of commands and
> expectations. Commands tell Protractor to do something with the
> application such as navigate to a page or click on a button.
> Expectations tell Protractor to assert something about the
> application's state, such as the value of a field or the current URL.
>
> If any expectation within an it block fails, the runner marks the it
> as "failed" and continues on to the next block.
>
> Test files may also have beforeEach and afterEach blocks, which will
> be run before or after each it block regardless of whether the block
> passes or fails.
>
>  
>
> Protractor does not work out-of-the-box with apps that bootstrap
> manually using angular.bootstrap. You must use the ng-app directive.
>
>  
>
>  
>
> **\$location**
>
>  
>
> The \$location service parses the URL in the browser address bar
> (based
> on [window.location](https://developer.mozilla.org/en/window.location))
> and makes the URL available to your application. Changes to the URL in
> the address bar are reflected into the \$location service and changes
> to \$location are reflected into the browser address bar.
>
> **The \$location service:**

-   Exposes the current URL in the browser address bar, so you can

    -   Watch and observe the URL.

    -   Change the URL.

-   Maintains synchronization between itself and the browser's URL when
    > the user

    -   Changes the address in the browser's address bar.

    -   Clicks the back or forward button in the browser (or clicks a
        > History link).

    -   Clicks on a link in the page.

-   Represents the URL object as a set of methods (protocol, host, port,
    > path, search, hash).

>  
>
> ![](media/image8.png){width="6.8125in" height="2.5in"}
>
>  
>
>  
>
> It does not cause a full page reload when the browser URL is changed.
> To reload the page after changing the URL, use the lower-level API,
> \$window.location.href.
>
>  
>
> **\$location service configuration**
>
>  
>
> To configure the \$location service, retrieve the \$locationProvider
> and set the parameters. \$location service provides getter methods for
> read-only parts of the URL (absUrl, protocol, host, port) and getter /
> setter methods for url, path, search, hash:
>
>  
>
> There is a special replace method which can be used to tell the
> \$location service that the next time the \$location service is synced
> with the browser, the last history record should be replaced instead
> of creating a new one. This is useful when you want to implement
> redirection, which would otherwise break the back button (navigating
> back would retrigger the redirection). To change the current URL
> without creating a new browser history record you can call:
>
> \$location.path('/someNewPath');\
> \$location.replace();\
> // or you can chain these as:
> \$location.path('/someNewPath').replace();
>
>  
>
> Note that the setters don't update window.location immediately.
> Instead, the \$location service is aware of the scope life-cycle and
> coalesces multiple \$location mutations into one "commit" to the
> window.location object during the scope \$digest phase. Since multiple
> changes to the \$location's state will be pushed to the browser as a
> single change, it's enough to call the replace() method just once to
> make the entire "commit" a replace operation rather than an addition
> to the browser history. Once the browser is updated, the \$location
> service resets the flag set by replace() method and future mutations
> will create new history records, unless replace() is called again.
>
>  
>
> **Setters and character encoding**
>
> You can pass special characters to \$location service and it will
> encode them according to rules specified in [RFC
> 3986](http://www.ietf.org/rfc/rfc3986.txt). When you access the
> methods:

-   All values that are passed to \$location setter
    > methods, path(), search(), hash(), are encoded.

-   Getters (calls to methods without parameters) return decoded values
    > for the following methods path(), search(), hash().

-   When you call the absUrl() method, the returned value is a full url
    > with its segments encoded.

-   When you call the url() method, the returned value is path, search
    > and hash, in the form /path?search=a&b=c\#hash. The segments are
    > encoded as well.

>  
>
>  
>
> \$location service has two configuration modes which control the
> format of the URL in the browser address bar: **Hashbang** mode (the
> default) and the **HTML5** mode which is based on using the HTML5
> History API.
>
>  
>
> ![](media/image9.png){width="7.5625in" height="1.9166666666666667in"}
>
>  
>
> In **HTML5** mode, the \$location service getters and setters interact
> with the browser URL address through the HTML5 history API. This
> allows for use of regular URL path and search segments, instead of
> their hashbang equivalents. If the HTML5 History API is not supported
> by a browser, the \$location service will fall back to using the
> hashbang URLs automatically. This frees you from having to worry about
> whether the browser displaying your app supports the history API or
> not; the \$location service transparently uses the best available
> option.
>
>  
>
> Opening a regular URL in a legacy browser -&gt; redirects to a
> hashbang URL
>
> Opening hashbang URL in a modern browser -&gt; rewrites to a regular
> URL
>
>  
>
> **Relative links**
>
> Be sure to check all relative links, images, scripts etc. Angular
> requires you to specify the url base in the head of your main html
> file (&lt;base href="/my-base/index.html"&gt;)
> unless html5Mode.requireBase is set to false in the html5Mode
> definition object passed to\$locationProvider.html5Mode(). With that,
> relative urls will always be resolved to this base url, even if the
> initial url of the document was different.
>
> There is one exception: Links that only contain a hash fragment
> (e.g. &lt;a href="\#target"&gt;) will only
> change \$location.hash() and not modify the url otherwise. This is
> useful for scrolling to anchors on the same page without needing to
> know on which page the user currently is.
>
>  
>
> Check <https://docs.angularjs.org/guide/$location> for more location
> tutorial and caveats
>
>  
>
> **CSS classes used by angular**
>
>  

-   ng-scope

    -   **Usage:** angular applies this class to any element for which a
        > new [scope](https://docs.angularjs.org/api/ng/service/$rootScope) is defined.
        > (see [scope](https://docs.angularjs.org/guide/scope) guide for
        > more information about scopes)

-   ng-isolate-scope

    -   **Usage:** angular applies this class to any element for which a
        > new [isolate
        > scope](https://docs.angularjs.org/guide/directive#isolating-the-scope-of-a-directive) is defined.

-   ng-binding

    -   **Usage:** angular applies this class to any element that is
        > attached to a data binding, via ng-bind or {{}} curly braces,
        > for example.
        > (see [databinding](https://docs.angularjs.org/guide/databinding) guide)

-   ng-invalid, ng-valid

    -   **Usage:** angular applies this class to a form control widget
        > element if that element's input does not pass validation.
        > (see [input](https://docs.angularjs.org/api/ng/directive/input)directive)

-   ng-pristine, ng-dirty

    -   **Usage:** angular [ngModel](https://docs.angularjs.org/api/ng/directive/ngModel) directive
        > applies ng-pristine class to a new form control widget which
        > did not have user interaction. Once the user interacts with
        > the form control, the class is changed to ng-dirty.

-   ng-touched, ng-untouched

    -   **Usage:** angular [ngModel](https://docs.angularjs.org/api/ng/directive/ngModel) directive
        > applies ng-untouched class to a new form control widget which
        > has not been blurred. Once the user blurs the form control,
        > the class is changed to ng-touched.

>  
>
> **i18n and l10n**
>
>  
>
> Internationalization (i18n) is the process of developing products in
> such a way that they can be localized for languages and cultures
> easily. Localization (l10n), is the process of adapting applications
> and text to enable their usability in a particular cultural or
> linguistic market. For application developers, internationalizing an
> application means abstracting all of the strings and other
> locale-specific bits (such as date or currency formats) out of the
> application. Localizing an application means providing translations
> and localized formats for the abstracted bits.
>
>  
>
> Angular supports i18n/l10n for date, number and currency filters.
>
> Localizable pluralization is supported via the ngPluralize directive.
> Additionally, you can use MessageFormat extensions to \$interpolate
> for localizable pluralization and gender support in all interpolations
> via the ngMessageFormat module.
>
> All localizable Angular components depend on locale-specific rule sets
> managed by the \$locale service.
>
>  
>
> Check <https://docs.angularjs.org/guide/i18n>
>
>  
>
>  
>
> **Security**
>
>  
>
> <https://docs.angularjs.org/guide/security>
>
>  
>
>  
>
> **Accessibility **
>
>  
>
> The goal of ngAria is to improve Angular's default accessibility by
> enabling common ARIA attributes that convey state or semantic
> information for assistive technologies used by persons with
> disabilities.
>
>  
>
> **Decorators**
>
>  
>
> Decorators are a design pattern that is used to separate modification
> or decoration of a class without modifying the original source code.
> In Angular, decorators are functions that allow a service, directive
> or filter to be modified prior to its usage.
>
>  
>
> **Running an AngularJS App in Production**
>
>  

-   **Disabling Debug Data: **

>  
>
> **Concepts**
>
>  
>
> In Angular, a file like this is called a template. When Angular starts
> your application, it parses and processes this new markup from the
> template using the compiler. The loaded, transformed and rendered DOM
> is then called the view. The first kind of new markup are the
> directives. They apply special behavior to attributes or elements in
> the HTML. In the example above we use the ng-app attribute, which is
> linked to a directive that automatically initializes our application.
> Angular also defines a directive for the input element that adds extra
> behavior to the element. The ng-model directive stores/updates the
> value of the input field into/from a variable.
>
>  
>
> In Angular, the only place where an application should access the DOM
> is within directives. This is important because artifacts that access
> the DOM are hard to test. If you need to access the DOM directly you
> should write a custom directive for this
>
>  
>
> The second kind of new markup are the double curly braces {{
> expression | filter }}: When the compiler encounters this markup, it
> will replace it with the evaluated value of the markup. An expression
> in a template is a JavaScript-like code snippet that allows Angular to
> read and write variables. Note that those variables are not global
> variables. Just like variables in a JavaScript function live in a
> scope, Angular provides a scope for the variables accessible to
> expressions. The values that are stored in variables on the scope are
> referred to as the model in the rest of the documentation. The example
> above also contains a filter. A filter formats the value of an
> expression for display to the user. The important thing in the example
> is that Angular provides live bindings: Whenever the input values
> change, the value of the expressions are automatically recalculated
> and the DOM is updated with their values. The concept behind this is
> two-way data binding.
>
>  
>
> Controller More accurately, the file specifies a constructor function
> that will be used to create the actual controller instance. The
> purpose of controllers is to expose variables and functionality to
> expressions and directives. ng-controller directive to the HTML. This
> directive tells Angular that the new InvoiceController is responsible
> for the element with the directive and all of the element's children.
> The syntax InvoiceController as invoice tells Angular to instantiate
> the controller and save it in the variable invoice in the current
> scope.
>
>  
>
> We moved the convertCurrency function and the definition of the
> existing currencies into the new file finance2.js. But how does the
> controller get a hold of the now separated function?
>
> This is where Dependency Injection comes into play. Dependency
> Injection (DI) is a software design pattern that deals with how
> objects and functions get created and how they get a hold of their
> dependencies. Everything within Angular (directives, filters,
> controllers, services, ...) is created and wired using dependency
> injection. Within Angular, the DI container is called the injector.
>
> To use DI, there needs to be a place where all the things that should
> work together are registered. In Angular, this is the purpose of the
> modules. When Angular starts, it will use the configuration of the
> module with the name defined by the ng-app directive, including the
> configuration of all modules that this module depends on.
>
>  
>
> In the example above: The template contains the directive
> ng-app="invoice2". This tells Angular to use the invoice2 module as
> the main module for the application. The code snippet
> angular.module('invoice2', \['finance2'\]) specifies that the invoice2
> module depends on the finance2 module. By this, Angular uses the
> InvoiceController as well as the currencyConverter service.
>
>  
>
> How does the InvoiceController get a reference to the
> currencyConverter function? In Angular, this is done by simply
> defining arguments on the constructor function. With this, the
> injector is able to create the objects in the right order and pass the
> previously created objects into the factories of the objects that
> depend on them. In our example, the InvoiceController has an argument
> named currencyConverter. By this, Angular knows about the dependency
> between the controller and the service and calls the controller with
> the service instance as argument.
>
>  
>
> ![](media/image10.png){width="4.666666666666667in" height="4.46875in"}
>
>  
>
>  
>
>  
>
> **The difference between services and factories**
>
>  
>
> Okay, so what is the difference between a service and a factory in
> AngularJS? As we all know, we can define a service like this:
>
> app.service('MyService', function () {\
> this.sayHello = function () {\
> console.log('hello');\
> };\
> });
>
> .service() is a method on our module that takes a name and a function
> that defines the service. Pretty straight forward. Once defined, we
> can inject and use that particular service in other components, like
> controllers, directives and filters, like this:
>
> app.controller('AppController', function (MyService) {\
> MyService.sayHello(); // logs 'hello'\
> });
>
> Okay, clear. Now the same thing as a factory:
>
> app.factory('MyService', function () {\
> return {\
> sayHello: function () {\
> console.log('hello');\
> }\
> }\
> });
>
> Again, .factory() is a method on our module and it also takes a name
> and a function, that defines the factory. We can inject and use that
> thing exactly the same way we did with the service. Now what is the
> difference here?
>
> Well, you might see that instead of working with this in the factory,
> we’re returning an object literal. Why is that? It turns out, **a
> service is a constructor function** whereas a factory is not.
> Somewhere deep inside of this Angular world, there’s this code that
> calls Object.create()with the service constructor function, when it
> gets instantiated. However, a factory function is really just a
> function that gets called, which is why we have to return an object
> explicitly.
>
>  
>
> if we inject MyService somewhere, what happens behind the scenes is:
>
> MyServiceProvider.\$get(); // return the instance of the service
>
> Alright, factory functions just get called, what about the service
> code? Here’s another snippet:
>
> function service(name, constructor) {\
> return factory(name, \['\$injector', function(\$injector) {\
> return \$injector.instantiate(constructor);\
> }\]);\
> }
>
> Oh look, it turns out that when we call service() it actually
> calls factory(). But it doesn’t just pass our service constructor
> function to the factory as it is. It passes a function that asks the
> injector to instantiate and object by the given constructor. In other
> words: a service calls a predefined factory, which ends up
> as \$get() method on the corresponding
> provider.\$injector.instantiate() is the method that ultimately
> calls Object.create() with the constructor function. That’s why we
> use this in services.
>
> Okay, so it turns out that, no matter what we
> use, service() or factory(), it’s always a factory that is called
> which creates a provider for our service
>
>  
>
>  
>
> Both service and factory allow as to define code before methods..
>
>  
>
> ![](media/image11.png){width="2.9583333333333335in"
> height="3.1145833333333335in"}
>
>  
>
> It says we can run code before we return our object literal. That
> basically allows us to do some configuration stuff or conditionally
> create an object or not, which doesn’t seem to be possible when
> creating a service directly, which is why most resources recommend to
> use factories over services, but the reasoning is inappreciable.
>
> What if I told you, we can do the exact same thing with services too?
>
> Yeap, correct. A service is a constructor function, however, that
> doesn’t prevent us from doing additional work and return object
> literals. ***In fact, constructor functions in JavaScript can return
> whatever they want. So we can take our service code and write it in a
> way that it basically does the exact same thing as our factory:***
>
>  
>
> ![](media/image12.png){width="3.3020833333333335in"
> height="2.53125in"}
>
>  
>
> **Services allow us to use ES6 classes**
>
>  
>
> Of course, writing services in that way is kind of contra productive,
> since it’s called as a constructor function, so it should also be used
> like one. Is there any advantage over the other at all then? Yes,
> there is. It turns out that it’s actually better to use services where
> possible, when it comes to migrating to ES6. The reason for that is
> simply that a service is a constructor function and a factory is not.
> Working with constructor functions in ES5 allows us to easily use ES6
> classes when we migrate to ES6.
>
>  
>
> With factories, this is not possible because they are simply called as
> functions.
>
>  
>
> From
> &lt;<http://blog.thoughtram.io/angular/2015/07/07/service-vs-factory-once-and-for-all.html>&gt;
>
>  
>
>

 

Wednesday, April 06, 2016

21:46

 

Classes and objects

Inheritance

Iterators

Generators

proxy

 

 

Objects

Thursday, April 07, 2016

10:09

From one side, an object is an associative array (called hash in some
languages). It stores key-value pairs. From the other side, objects are
used for object-oriented programming, and that’s a different story.

An empty object (you may also read as empty associative array) is
created with one of two syntaxes:

 

1\. o = new Object()

2\. o = { } // the same

 

There’s a significant difference between dot and square brackets.

-   **obj.prop** returns the key named ‘prop’

-   **obj\[prop\] returns the key named by value of prop:**

>  

We can try to get any property from an object. There will be no error.
But if the property does not exist, then undefined is returned:

 

There is a special for..in syntax to list object properties:

 

**for**(key **in** obj) {

  ... obj\[key\] ...

}

 

 

In theory, the order of iteration over object properties is not
guaranteed. In practice, there is a de-facto standard about it.

-   IE&lt;9, Firefox, Safari always iterate in the order of definition.

-   Opera, IE9, Chrome iterate in the order of definition for string
    > keys.\
    > Numeric keys become sorted and go before string keys.

 

A variable which is assigned to object actually keeps reference to it.
That is, a variable stores kind-of pointer to real data. You can use the
variable to change this data, this will affect all other references.
Same happens when you pass an object to function. **The variable is a
reference, not a value.**

 

You can store anything in object. Not just simple values, but also
functions. When you put a function into an object, you can call it as
method:

 

 

An object can be created literally, using obj = { ... } syntax. Another
way of creating an object in JavaScript is to construct it by calling a
function with new directive.

 

 

 

 

 

 

YDKJS - 1

Thursday, April 07, 2016

14:25

There are differences! Where JavaScript differs from traditionally
"compiled" languages such as C\# and Java is that JavaScript
is **JIT(Just-In-Time) compiled**. What that means is that JavaScript
isn't compiled well into advance into object code(or another language)
that can be ported and thrown around from one environment to the nex

There are three major components that are involved with JavaScript
Compilation:

-   **The Compiler:** Handles all standard compiler tasks: parsing,
    > generation and lexing. Slightly different from the traditional
    > compiler, see below.

-   **The Scope:** Constant looks up all declared variables and passes
    > them along to the engine for execution. Keeps track of declared
    > variables!

-   **The Engine:** Handles all of the execution and fires all the
    > events that are necessary in the flow(Compilation/Scope lookup)

>  

Communication is key in all long lasting relationships, JavaScript
compilation is no exception! As portions of JavaScript code is traversed
throughout the program, the compiler will lex(tokenize) followed by
throwing it into a AST tree. Sounds about similar? Well things get
interesting when we get to the code generation step, the compiler
actually starts to communicate with the scope to verify if the piece of
code already exists for the current scope. If this code does not exist,
scope is informed to declare the variables, otherwise the compiler takes
no action. Once the compiler is done going through the scope, it will
generate the code for the engine to execute. Here is where the engine
starts to execute...NOT SO FAST! The engine doesn't execute anything
just yet! The engine needs to communicate with the scope to verify that
the variables being passed to it are accessible in the current scope, if
they are, then the value is assigned and we move on. The engine compiles
the code before it executes it. In part to this process it registers the
variable declarations with the scope. Variable declarations are
processed by the engine prior to any other code execution via the
engine-scope communication stream. Hoisting is nothing more than
understanding that variable declarations are moved up in the execution
tree.

 

JavaScript JIT compilers:

-   Google Chrome V80 - NodeJS & Chrome

-   JaegerMonkey - Mozilla

-   SpiderMonkey - Mozilla

-   IonMonkey - Mozilla

-   Chakra - IE

 

Prompt() to get values from user.

 

If you have a number but need to print it on the screen, you need to
convert the value to a string , and in JavaScript this conversion is
called "coercion." Similarly, if someone enters a series of numeric
characters into a form on an ecommerce page, that's a string , but if
you need to then use that value to do math operations, you need to
coerce it to a number .

var b = Number( a );

 

But a controversial topic is what happens when you try to compare two
values that are not already of the same type, which would require
implicit coercion. To help you out in these common situations,
JavaScript will sometimes kick in and implicitly coerce values to the
matching types.

So if you use the == loose equals operator to make the comparison
"99.99" == 99.99 , JavaScript will convert the lefthand side "99.99" to
its number equivalent 99.99 .

 

In some programming languages, you declare a variable (container) to
hold a specific type of value, such as number or string . Static typing,
otherwise known as type enforcement, is typically cited as a benefit for
program correctness by preventing unintended value conversions. Other
languages emphasize types for values instead of variables. Weak typing,
otherwise known as dynamic typing, allows a variable to hold any type of
value at any time. It's typically cited as a benefit for program
flexibility by allowing a single variable

to represent a value no matter what type form that value may take at any
given moment in the program's logic flow. JavaScript uses the latter
approach, dynamic typing, meaning variables can hold values of any type
without any type enforcement.

 

The newest version of JavaScript at the time of this writing (commonly
called "ES6") includes a new way to declare constants, by using const
instead of var. If you tried to assign any different value to TAX\_RATE
after that first declaration, your program would reject the change (and
in strict mode, fail with an error).

 

The if statement expects a boolean , but if you pass it something that's
not already boolean , coercion will occur. JavaScript defines a list of
specific values that are considered "falsy" because when coerced to a
boolean they become false these include values like 0 and "" . Any other
value not on the "falsy" list is automatically "truthy" when coerced to
a boolean they become true . Truthy values include things like 99.99 and
"free".

 

In JavaScript each function gets its own scope. Scope is basically a
collection of variables as well as the rules for how those variables are
accessed by name. Only code inside that function can access that
function's scoped variables. A variable name has to be unique within the
same scope there can't be two different a variables sitting right next
to each other. But the same variable name a could appear in different
scopes.

Lexical scope rules say that code in one scope can access variables of
either that scope or any scope outside of it.

 

JavaScript has typed values, not typed variables. The following builtin
types are available:

**string**

**number**

**boolean**

**null and undefined**

**object**

**symbol (new to ES6)**

 

JavaScript provides a typeof operator that can examine a value and tell
you what type it is

 

***Objects***

The object type refers to a compound value where you can set properties
(named locations) that each hold their own values of any type.

 

var obj = {

a: "hello world",

b: 42,

c: true

};

 

obj.a; // "hello world"

obj\["a"\]; // "hello world"

 

Properties can either be accessed with dot notation (i.e., obj.a ) or
bracket notation (i.e., obj\["a"\] ). Dot notation is shorter and
generally easier to read, and is thus preferred when possible

 

var obj = {

a: "hello world",

b: 42

};

var b = "a";

obj\[b\]; // "hello world"

obj\["b"\]; // 42

 

***Arrays***

An array is an object that holds values (of any type) not particularly
in named properties/keys, but rather in numerically indexed positions

 

var arr = \[

"hello world",

42,

true

\];

arr\[0\]; // "hello world"

 

Because arrays are special objects (as typeof implies), they can also
have properties, including the automatically updated length property

 

***Functions***

 

functions are a subtype of objects typeof returns "function" , which
implies that a function is a main type and can thus have properties, but
you typically will only use function object properties (like foo.bar )
in limited cases

 

***BuiltIn Type Methods***

 

The "how" behind being able to call a.toUpperCase() is more complicated
than just that method existing on the value. Briefly there is a String
(capital S ) object wrapper form typically called a "native " that pairs
with the primitive string type; it's this object wrapper that defines
the toUpperCase() method on its prototype. When you use a primitive
value like "hello world" as an object by referencing a property or
method (e.g., a.toUpperCase() in the previous snippet), JS automatically
"boxes" the value to its object wrapper counterpart

 

***Coercion***

 

Coercion comes in two forms in JavaScript: explicit and implicit.
Explicit coercion is simply that you can see obviously from the code
that a conversion from one type to another will occur whereas implicit
coercion is when the type conversion can happen as more of a nonobvious
side effect of some other operation

 

***Equality***

There are four equality operators: == , === , != , and !==.

 

The difference between == and === is usually characterized that ==
checks for value equality and === checks for both value and type
equality. However this is inaccurate. The proper way to characterize
them is that == checks for value equality with coercion allowed and ===
checks for value equality without allowing coercion; === is often called
"strict equality" for this reason

 

In the a == b comparison, JS notices that the types do not match, so it
goes through an ordered series of steps to coerce one or both values to
a different type until the types match, where then a simple value
equality can be checked. The a === b produces false , because the
coercion is not allowed, so the simple value comparison obviously fails.

 

You should take special note of the == and === comparison rules if
you're comparing two nonprimitive values like object s (including
function and array ). Because those values are actually held by
reference both == and === comparisons will simply check whether the
references match not anything about the underlying values

 

JavaScript string values can also be compared for inequality, using
typical alphabetic rules ( "bar" &lt; "foo" ). Similar rules as ==
comparison (though not exactly identical!) apply to the inequality
operators. Notably, there are no "strict inequality" operators that
would disallow coercion the same way === "strict equality" does

 

***Function Scopes***

 

You use the var keyword to declare a variable that will belong to the
current function scope, or the global scope if at the top level outside
of any function.

 

*Hoisting*

Wherever a var appears inside a scope, that declaration is taken to
belong to the entire scope and accessible everywhere throughout.
Metaphorically, this behavior is called hoisting, when a var declaration
is conceptually "moved" to the top of its enclosing scope.

 

In addition to creating declarations for variables at the function
level, ES6 lets you declare variables to belong to individual blocks
(pairs of { .. } ), using the let keyword

 

 

***Strict Mode***

 

ES5 added a "strict mode" to the language, which tightens the rules for
certain behaviors. Generally, these restrictions are seen as keeping the
code to a safer and more appropriate set of guidelines. Also, adhering
to strict mode makes your code generally more optimizable by the engine.

You can opt in to strict mode for an individual function, or an entire
file, depending on where you put the strict mode pragma

function foo() {

"use strict";

}

 

***Functions As Values***

 

Not only can you pass a value (argument) to a function, but a function
itself can be a value that's assigned to variables, or passed to or
returned from other functions. As such, a function value should be
thought of as an expression, much like any other value or expression.

 

var foo = function() {

// ..

};

 

var x = function bar(){

// ..

};

 

The first function expression assigned to the foo variable is called
anonymous because it has no name . The second function expression is
named ( bar ), even as a reference to it is also assigned to the x
variable. Named function expressions are generally more preferable,
though anonymous function expressions are still extremely common

 

***Immediately Invoked Function Expressions (IIFEs)***

 

There's another way to execute a function expression, which is typically
referred to as an immediately invoked function

expression (IIFE):

(function IIFE(){

console.log( "Hello!" );

})();

// "Hello!"

 

The outer ( .. ) that surrounds the (function IIFE(){ .. }) function
expression is just a nuance of JS grammar needed to prevent it from
being treated as a normal function declaration. The final () on the end
of the expression the })(); line is what actually executes the function
expression referenced immediately before it.

 

Because an IIFE is just a function, and functions create variable scope,
using an IIFE in this fashion is often used to declare variables that
won't affect the surrounding code outside the IIFE:

 

var a = 42;

(function IIFE(){

var a = 10;

console.log( a ); // 10

})();

console.log( a ); // 42

 

IIFEs can also have return values:

var x = (function IIFE(){

return 42;

})();

x; // 42

 

***Closure***

 

You can think of closure as a way to "remember" and continue to access a
function's scope (its variables) even once the function has finished
running.

 

function makeAdder(x) {

// parameter \`x\` is an inner variable

// inner function \`add()\` uses \`x\`, so

// it has a "closure" over it

function add(y) {

return y + x;

};

return add;

}

 

The reference to the inner add(..) function that gets returned with each
call to the outer makeAdder(..) is able to remember whatever x value was
passed in to makeAdder(..) .

 

// \`plusOne\` gets a reference to the inner \`add(..)\`

// function with closure over the \`x\` parameter of

// the outer \`makeAdder(..)\`

var plusOne = makeAdder( 1 );

// \`plusTen\` gets a reference to the inner \`add(..)\`

// function with closure over the \`x\` parameter of

// the outer \`makeAdder(..)\`

var plusTen = makeAdder( 10 );

plusOne( 3 ); // 4 &lt;‐‐ 1 + 3

plusOne( 41 ); // 42 &lt;‐‐ 1 + 41

plusTen( 13 ); // 23 &lt;‐‐ 10 + 13

 

***Modules***

The most common usage of closure in JavaScript is the module pattern.
Modules let you define private implementation details (variables,
functions) that are hidden from the outside world, as well as a public
API that is accessible from the outside.

 

function User(){

var username, password;

function doLogin(user,pw) {

username = user;

password = pw;

// do the rest of the login work

}

var publicAPI = {

login: doLogin

};

return publicAPI;

}

// create a \`User\` module instance

var fred = User();

fred.login( "fred", "12Battery34!" );

 

 

The User() function serves as an outer scope that holds the variables
username and password as well as the inner doLogin() function; these are
all private inner details of this User module that cannot be accessed
from the outside world. Executing User() creates an instance of the User
module a whole new scope is created and thus a whole new copy of each of
these inner variables/functions. We assign this instance to fred . If we
run User() again we'd get a new instance entirely separate from fred .
The inner doLogin() function has a closure over username and password
meaning it will retain its access to them even after the User() function
finishes running. publicAPI is an object with one property/method on it
login which is a reference to the inner doLogin() function. When we
return publicAPI from User() it becomes the instance we call fred . At
this point the outer User() function has finished executing. Normally
you'd think the inner variables like username and password have gone
away. But here they have not because there's a closure in the login()
function keeping them alive. That's why we can call fred.login(..) the
same as calling the inner doLogin(..) and it can still access username
and password inner variables.

 

***this Identifier***

 

If a function has a this reference inside it, that this reference
usually points to an object . But which object it points to depends on
how the function was called. It's important to realize that this does
not refer to the function itself, as is the most common misconception.

 

function foo() {

console.log( this.bar );

}

var bar = "global";

var obj1 = {

bar: "obj1",

foo: foo

};

var obj2 = {

bar: "obj2"

};

// ‐‐‐‐‐‐‐‐

foo(); // "global"

obj1.foo(); // "obj1"

foo.call( obj2 ); // "obj2"

new foo(); // undefined

 

There are four rules for how this gets set, and they're shown in those
last four lines of that snippet.

1\. foo() ends up setting this to the global object in nonstrict mode in
strict mode, this would be undefined and you'd get an error in accessing
the bar property so "global" is the value found for this.bar .

2\. obj1.foo() sets this to the obj1 object.

3\. foo.call(obj2) sets this to the obj2 object.

4\. new foo() sets this to a brand new empty object.

 

***Prototypes***

When you reference a property on an object, if that property doesn't
exist, JavaScript will automatically use that object's internal
prototype reference to find another object to look for the property on.
You could think of this almost as a fallback if the property is missing.
The internal prototype reference linkage from one object to its fallback
happens at the time the object is created

 

var foo = {

a: 42

};

// create \`bar\` and link it to \`foo\`

var bar = Object.create( foo );

bar.b = "hello world";

bar.b; // "hello world"

bar.a; // 42 &lt;‐‐ delegated to \`foo\`

 

The a property doesn't actually exist on the bar object, but because bar
is prototypelinked to foo , JavaScript automatically falls back to
looking for a on the foo object, where it's found.

 

***Polyfilling***

 

The word "polyfill" is an invented term (by Remy Sharp)
(<https://remysharp.com/2010/10/08/whatisapolyfill>) used to refer to
taking the definition of a newer feature and producing a piece of code
that's equivalent to the behavior, but is able to run in older JS
environments.

For example, ES6 defines a utility called Number.isNaN(..) to provide an
accurate nonbuggy check for NaN values, deprecating the original
isNaN(..) utility. But it's easy to polyfill that utility so that you
can start using it in your code regardless of whether the end user is in
an ES6 browser or not.

Consider:

if (!Number.isNaN) {

Number.isNaN = function isNaN(x) {

return x !== x;

};

}

The if statement guards against applying the polyfill definition in ES6
browsers where it will already exist. If it's not already present, we
define Number.isNaN(..)

 

***Transpiling***

There's no way to polyfill new syntax that has been added to the
language. The new syntax would throw an error in the old JS engine as
unrecognized/invalid. So the better option is to use a tool that
converts your newer code into older code equivalents. This process is
commonly called "transpiling," a term for transforming + compiling.

Essentially, your source code is authored in the new syntax form, but
what you deploy to the browser is the transpiled code in old syntax
form. You typically insert the transpiler into your build process,
similar to your code linter or your minifier

 

***NonJavaScript***

 

The most common nonJavaScript JavaScript you'll encounter is the DOM
API. For example:

var el = document.getElementById( "foo" );

The document variable exists as a global variable when your code is
running in a browser. It's not provided by the JS engine, nor is it
particularly controlled by the JavaScript specification. It takes the
form of something that looks an awful lot like a normal JS object , but
it's not really exactly that. It's a special object, often called a
"host object."

Moreover, the getElementById(..) method on document looks like a normal
JS function, but it's just a thinly exposed interface to a builtin
method provided by the DOM from your browser. In some (newergeneration)
browsers, this layer may also be in JS, but traditionally the DOM and
its behavior is implemented in something more like C/C++.

 

Everyone's favorite alert(..) pops up a message box in the user's
browser window. alert(..) is provided to your JS program by the browser,
not by the JS engine itself. The call you make sends the message to the
browser internals and it handles drawing and displaying the message box.
The same goes with console.log(..) ; your browser provides such
mechanisms and hooks them up to the developer tools.

 

 

YDKJS -2

Thursday, April 07, 2016

20:57

 

The this keyword is dynamically bound based on how the function in
question is executed, and it turns out there are four simple rules to
understand and fully determine this binding.

Closely related to the this keyword is the object prototype mechanism,
which is a lookup chain for properties, similar to how lexical scope
variables are found

 

It may be self evident or it may be surprising depending on your level
of interaction with various languages but despite the fact that
JavaScript falls under the general category of "dynamic" or
"interpreted" languages it is in fact a compiled language. It is not
compiled well in advance as are many traditionally compiled languages
nor are the results of compilation portable among various distributed
systems. But nevertheless the JavaScript engine performs many of the
same steps albeit in more sophisticated ways than we may commonly be
aware of any traditional language compiler

 

In traditional compiled language process, a chunk of source code, your
program, will undergo typically three steps before it is executed,
roughly called "compilation

 

1\. Tokenizing/Lexing: breaking up a string of characters into meaningful
(to the language) chunks called tokens. For instance consider the
program: var a = 2; . This program would likely be broken up into the
following tokens: var a = 2 and ; . Whitespace may or may not be
persisted as a token depending on whether it's meaningful or not.

The difference between tokenizing and lexing is subtle and academic but
it centers on whether or not these tokens are identified in a stateless
or stateful way. Put simply if the tokenizer were to invoke stateful
parsing rules to figure out whether a should be considered a distinct
token or just part of another token that would be lexing.

 

2\. Parsing: taking a stream (array) of tokens and turning it into a tree
of nested elements which collectively represent the grammatical
structure of the program. This tree is called an "AST" (Abstract Syntax
Tree). The tree for var a = 2; might start with a toplevel node called
VariableDeclaration with a child node called Identifier (whose value is
a ) and another child called AssignmentExpression which itself has a
child called NumericLiteral (whose value is 2 ).

 

3\. CodeGeneration: the process of taking an AST and turning it into
executable code. This part varies greatly depending on the language, the
platform it's targeting, etc.

 

The JavaScript engine is vastly more complex than just those three steps
as are most other language compilers. For instance in the process of
parsing and codegeneration there are certainly steps to optimize the
performance of the execution including collapsing redundant elements
etc.

 

For one thing JavaScript engines don't get the luxury (like other
language compilers) of having plenty of time to optimize because
JavaScript compilation doesn't happen in a build step ahead of time as
with other languages. For JavaScript the compilation that occurs happens
in many cases mere microseconds (or less!) before the code is executed.
To ensure the fastest performance JS engines use all kinds of tricks
(like JITs which lazy compile and even hot recompile etc.) Let's just
say for simplicity's sake that any snippet of JavaScript has to be
compiled before (usually right before!) it's executed. So the JS
compiler will take the program var a = 2; and compile it first and then
be ready to execute it usually right away.

 

Parts of JIT

 

1\. Engine: responsible for start to finish compilation and execution of
our JavaScript program.

2\. Compiler: one of Engine's friends; handles all the dirty work of
parsing and codegeneration (see previous section).

3\. Scope: another friend of Engine; collects and maintains a lookup list
of all the declared identifiers (variables), and enforces a strict set
of rules as to how these are accessible to currently executing code.

 

var a = 2;

In fact, Engine sees two distinct statements, one which Compiler will
handle during compilation, and one which Engine will handle during
execution. The first thing Compiler will do with this program is perform
lexing to break it down into tokens, which it will then parse into a
tree.

 

Compiler will instead proceed as:

1\. Encountering var a , Compiler asks Scope to see if a variable a
already exists for that particular scope collection. If so, Compiler
ignores this declaration and moves on. Otherwise, Compiler asks Scope to
declare a new variable called a for that scope collection.

2\. Compiler then produces code for Engine to later execute, to handle
the a = 2 assignment. The code Engine runs will first ask Scope if there
is a variable called a accessible in the current scope collection. If
so, Engine uses that variable. If not, Engine looks elsewhere

 

To summarize: two distinct actions are taken for a variable assignment:
First, Compiler declares a variable (if not previously declared in the
current scope), and second, when executing, Engine looks up the variable
in Scope and assigns to it, if found , else raises error

 

When Engine executes the code that Compiler produced for step (2) it has
to lookup the variable a to see if it has been declared and this lookup
is consulting Scope. But the type of lookup Engine performs affects the
outcome of the lookup. In our case it is said that Engine would be
performing an "LHS" lookup for the variable a . The other type of lookup
is called "RHS"

 

 

a = 2;

The reference to a here is an LHS reference, because we don't actually
care what the current value is, we simply want to find the variable as a
target for the = 2 assignment operation.

 

 

***Nested Scope***

 

Just as a block or function is nested inside another block or function,
scopes are nested inside other scopes. So, if a variable cannot be found
in the immediate scope, Engine consults the next outer containing scope,
continuing until found or until the outermost (aka, global) scope has
been reached.

 

If an RHS lookup fails to ever find a variable anywhere in the nested
Scopes this results in a ReferenceError being thrown by the Engine. It's
important to note that the error is of the type ReferenceError . By
contrast if the Engine is performing an LHS lookup and arrives at the
top floor (global Scope) without finding it and if the program is not
running in "Strict Mode" \[\^notestrictmode\] then the global Scope will
create a new variable of that name in the global scope and hand it back
to Engine.

 

Now if a variable is found for an RHS lookup but you try to do something
with its value that is impossible such as trying to execute as function
a non function value or reference a property on a null or undefined
value then Engine throws a different kind of error called a TypeError .
ReferenceError is Scope resolution failure related whereas TypeError
implies that Scope resolution was successful but that there was an
illegal/impossible action attempted against the result

 

***Lexical Scope***

 

lexical scope is scope that is defined at lexing time. In other words,
lexical scope is based on where variables and blocks of scope are
authored, by you, at write time, and thus is (mostly) set in stone by
the time the lexer processes your code.

 

Scope lookup stops once it finds the first match. The same identifier
name can be specified at multiple layers of nested scope which is called
"shadowing" (the inner identifier "shadows" the outer identifier).
Regardless of shadowing scope lookup always starts at the innermost
scope being executed at the time and works its way outward/upward until
the first match and stops

 

Global variables are also automatically properties of the global object
( window in browsers, etc.), so it is possible to reference a global
variable not directly by its lexical name, but instead indirectly as a
property reference of the global object.

window.a

 

No matter where a function is invoked from, or even how it is invoked,
its lexical scope is only defined by where the function was declared.
The lexical scope lookup process only applies to firstclass identifiers
such as the a b and c . If you had a reference to foo.bar.baz in a piece
of code the lexical scope lookup would apply to finding the foo
identifier but once it locates that variable object propertyaccess rules
take over to resolve the bar and baz properties respectively.

 

Evaluating **eval**(..) (pun intended) in that light it should be clear
how eval(..) allows you to modify the lexical scope environment by
cheating and pretending that authortime (aka lexical) code was there all
along. On subsequent lines of code after an eval(..) has executed the
Engine will not "know" or "care" that the previous code in question was
dynamically interpreted and thus modified the lexical scope environment.
The Engine will simply perform its lexical scope lookups as it always
does.

eval(..) when used in a strictmode program operates in its own lexical
scope, which means declarations made inside of the eval() do not
actually modify the enclosing scope.

 

 

The JavaScript Engine has a number of performance optimizations that it
performs during the compilation phase. Some of these boil down to being
able to essentially statically analyze the code as it lexes and
predetermine where all the variable and function declarations are so
that it takes less effort to resolve identifiers during execution. But
if the Engine finds an eval(..) or with in the code it essentially has
to assume that all its awareness of identifier location may be invalid
because it cannot know at lexing time exactly what code you may pass to
eval(..) to modify the lexical scope or the contents of the object you
may pass to with to create a new lexical scope to be consulted. In other
words in the pessimistic sense most of those optimizations it would make
are pointless if eval(..) or with are present so it simply doesn't
perform the optimizations at all. Your code will almost certainly tend
to run slower simply by the fact that you include an eval(..) or with
anywhere in the code.

 

 

 

function foo(a) {

var b = 2;

// some code

function bar() {

// ...

}

// more code

var c = 3;

}

 

 

In this snippet, the scope bubble for foo(..) includes identifiers a , b
, c and bar . It doesn't matter where in the scope a declaration
appears, the variable or function belongs to the containing scope
bubble, regardless

Because a , b , c , and bar all belong to the scope bubble of foo(..) ,
they are not accessible outside of foo(..) . That is, the following code
would all result in ReferenceError errors, as the identifiers are not
available to the global scope:

bar(); // fails

console.log( a, b, c ); // all 3 fail

However, all these identifiers ( a , b , c , foo , and bar ) are
accessible inside of foo(..) , and indeed also available inside of
bar(..)

 

***Can access a variable defined in higher scope in a nested scope. But
reverse is not possible. i.e checking for a variable happens from
current scope and upwards.. Not inwards..***

where we declare variables is not relevant when using var , because they
will always belong to the enclosing scope

 

The traditional way of thinking about functions is that you declare a
function, and then add code inside it. But the inverse thinking is
equally powerful and useful: take any arbitrary section of code you've
written, and wrap a function declaration around it, which in effect
"hides" the code. There's a variety of reasons motivating this
scopebased hiding. They tend to arise from the software design principle
"Principle of Least Privilege" \[\^noteleastprivilege\] also sometimes
called "Least Authority" or "Least Exposure". This principle states that
in the design of software such as the API for a module/object you should
expose only what is minimally necessary and "hide" everything else.

 

This principle extends to the choice of which scope to contain variables
and functions. If all variables and functions were in the global scope
they would of course be accessible to any nested scope. But this would
violate the "Least..." principle in that you are (likely) exposing many
variables or functions which you should otherwise keep private as proper
use of the code would discourage access to those variables/functions.

 

Another benefit of "hiding" variables and functions inside a scope is to
avoid unintended collision between two different identifiers with the
same name but different intended usages. Collision results often in
unexpected overwriting of values

 

function foo() {

function bar(a) {

i = 3; // changing the \`i\` in the enclosing scope's for‐loop

console.log( a + i );

}

for (var i=0; i&lt;10; i++) {

bar( i \* 2 ); // oops, infinite loop ahead!

}

}

foo();

 

The i = 3 assignment inside of bar(..) overwrites, unexpectedly, the i
that was declared in foo(..) at the forloop. In this case, it will
result in an infinite loop, because i is set to a fixed value of 3 and
that will forever remain &lt; 10 . The assignment inside bar(..) needs
to declare a local variable to use, regardless of what identifier name
is chosen. var I = 3; would fix the problem. Without this, I is searched
in higher scopes and finds it in foo() block.

 

***Global Namespaces***

 

A particularly strong example of (likely) variable collision occurs in
the global scope. Multiple libraries loaded into your program can quite
easily collide with each other if they don't properly hide their
internal/private functions and variables. Such libraries typically will
create a single variable declaration, often an object, with a
sufficiently unique name, in the global scope. This object is then used
as a "namespace" for that library

 

var MyReallyCoolLibrary = {

awesome: "stuff",

doSomething: function() {

// ...

},

doAnotherThing: function() {

// ...

}

};

 

 

***Module Management***

 

Another option for collision avoidance is the more modern "module"
approach using any of various dependency managers. Using these tools no
libraries ever add any identifiers to the global scope but are instead
required to have their identifier(s) be explicitly imported into another
specific scope through usage of the dependency manager's various
mechanisms. It should be observed that these tools do not possess
"magic" functionality that is exempt from lexical scoping rules. They
simply use the rules of scoping as explained here to enforce that no
identifiers are injected into any shared scope and are instead kept in
private noncollisionsusceptible scopes which prevents any accidental
scope collisions.

 

***Functions As Scopes***

 

We've seen that we can take any snippet of code and wrap a function
around it and that effectively "hides" any enclosed variable or function
declarations from the outside scope inside that function's inner scope.
While this technique "works" it is not necessarily very ideal. There are
a few problems it introduces. The first is that we have to declare a
namedfunction foo() which means that the identifier name foo itself
"pollutes" the enclosing scope (global in this case). We also have to
explicitly call the function by name ( foo() ) so that the wrapped code
actually executes

 

Fortunately, JavaScript offers a solution to both problems.

var a = 2;

(function foo(){ // &lt;‐‐ insert this

var a = 3;

console.log( a ); // 3

})(); // &lt;‐‐ and this

console.log( a ); // 2

 

First, notice that the wrapping function statement starts with
(function... as opposed to just function... . While this may seem like a
minor detail, it's actually a major change. Instead of treating the
function as a standard declaration, the function is treated as a
functionexpression

 

The easiest way to distinguish declaration vs. expression is the
position of the word "function" in the statement (not just a line, but a
distinct statement). If "function" is the very first thing in the
statement, then it's a function declaration. Otherwise, it's a function
expression

 

In the above snippet, the name foo is not bound in the enclosing scope,
but instead is bound only inside of its own function compared to
enclosing scope for normal function declarations. In other words,
(function foo(){ .. }) as an expression means the identifier foo is
found only in the scope where the .. indicates, not in the outer scope.
Hiding the name foo inside itself means it does not pollute the
enclosing scope unnecessarily.

 

***Anonymous vs. Named***

 

Anonymous function expressions are quick and easy to type, and many
libraries and tools tend to encourage this idiomatic style of code.
However, they have several drawbacks

to consider:

1\. Anonymous functions have no useful name to display in stack traces,
which can make debugging more difficult.

2\. Without a name, if the function needs to refer to itself, for
recursion, etc., the deprecated arguments.callee reference is
unfortunately required. Another example of needing to selfreference is
when an event handler function wants to unbind itself after it fires.

3\. Anonymous functions omit a name that is often helpful in providing
more readable/understandable code. A descriptive name helps selfdocument
the code in question.

 

Inline function expressions are powerful and useful the question of
anonymous vs. named doesn't detract from that. Providing a name for your
function expression quite effectively addresses all these drawbacks, but
has no tangible downsides. The best practice is to always name your
function expressions

 

setTimeout( function(){

console.log("I waited 1 second!");

}, 1000 );

 

 

setTimeout( function timeoutHandler(){ // &lt;‐‐ Look, I have a name!

console.log( "I waited 1 second!" );

}, 1000 );

 

***Invoking Function Expressions Immediately***

 

Now that we have a function as an expression by virtue of wrapping it in
a ( ) pair, we can execute that function by adding another () on the
end, like (function foo(){ .. })() . The first enclosing ( ) pair makes
the function an expression, and the second () executes the function.
This pattern is so common, a few years ago the community agreed on a
term for it: **IIFE**, which stands for Immediately Invoked Function
Expression. Of course, IIFE's don't need names, necessarily the most
common form of IIFE is to use an anonymous function

expression. While certainly less common, naming an IIFE has all the
aforementioned benefits over anonymous function expressions, so it's a
good practice to adopt.

 

Another variation on IIFE's which is quite common is to use the fact
that they are, in fact, just function calls, and pass in argument(s).

 

var a = 2;

(function IIFE( global ){

var a = 3;

console.log( a ); // 3

console.log( global.a ); // 2

})( window );

console.log( a ); // 2

 

Another application of this pattern addresses the (minor niche) concern
that the default undefined identifier might have its value incorrectly
overwritten, causing unexpected results. By naming a parameter undefined
, but not passing any value for that argument, we can guarantee that the
undefined identifier is in fact the undefined value in a block of code

 

undefined = true; // setting a land‐mine for other code! avoid!

(function IIFE( undefined ){

var a;

if (a === undefined) {

console.log( "Undefined is safe here!" );

}

})();

 

***Blocks As Scopes***

 

While functions are the most common unit of scope, and certainly the
most widespread of the design approaches in the majority of JS in
circulation, other units of scope are possible, and the usage of these
other scope units can lead to even better, cleaner to maintain code.

Block scope is a tool to extend the earlier "Principle of Least
Privilege Exposure" \[\^noteleastprivilege\] from hiding information in
functions to hiding information in blocks of our code.

 

It's a very little known fact that JavaScript in ES3 specified the
variable declaration in the catch clause of a try/catch to be
blockscoped to the catch block.

 

***LET***

 

The let keyword attaches the variable declaration to the scope of
whatever block (commonly a { .. } pair) it's contained in. In other
words, let implicitly hijacks any block's scope for its variable
declaration

 

var foo = true;

if (foo) {

let bar = foo \* 2;

bar = something( bar );

console.log( bar );

}

console.log( bar ); // ReferenceError

 

Creating explicit blocks for blockscoping can address some of these
concerns, making it more obvious where variables are attached and not.
Usually, explicit code is preferable over implicit or subtle code. This
explicit blockscoping style is easy to achieve, and fits more naturally
with how blockscoping works in other languages

 

var foo = true;

if (foo) {

{ // &lt;‐‐ explicit block

let bar = foo \* 2;

bar = something( bar );

console.log( bar );

}

}

console.log( bar ); // ReferenceError

 

However, declarations made with let will not hoist to the entire scope
of the block they appear in. Such declarations will not observably
"exist" in the block until the declaration statement.

{

console.log( bar ); // ReferenceError!

let bar = 2;

}

 

A particular case where let shines is in the forloop case as we
discussed previously.

for (let i=0; i&lt;10; i++) {

console.log( i );

}

console.log( i ); // ReferenceError

 

Not only does let in the forloop header bind the i to the forloop body,
but in fact, it rebinds it to each iteration of the loop, making sure to
reassign it the value from the end of the previous loop iteration

 

Because let declarations attach to arbitrary blocks rather than to the
enclosing function's scope (or global), there can be gotchas where
existing code has a hidden reliance on functionscoped var declarations,
and replacing the var with let may require additional care when
refactoring code

 

 

 

***Garbage Collection***

 

Another reason blockscoping is useful relates to closures and garbage
collection to reclaim memory

 

function process(data) {

// do something interesting

}

var someReallyBigData = { .. };

process( someReallyBigData );

var btn = document.getElementById( "my\_button" );

btn.addEventListener( "click", function click(evt){

console.log("button clicked");

}, /\*capturingPhase=\*/false );

 

The click function click handler callback doesn't need the
someReallyBigData variable at all. That means, theoretically, after
process(..) runs, the big memoryheavy data structure could be garbage
collected. However, it's quite likely (though implementation dependent)
that the JS engine will still have to keep the structure around, since
the click function has a

closure over the entire scope.

Blockscoping can address this concern, making it clearer to the engine
that it does not need to keep someReallyBigData around:

function process(data) {

// do something interesting

}

// anything declared inside this block can go away after!

{

let someReallyBigData = { .. };

process( someReallyBigData );

}

var btn = document.getElementById( "my\_button" );

btn.addEventListener( "click", function click(evt){

console.log("button clicked");

}, /\*capturingPhase=\*/false );

 

Declaring explicit blocks for variables to locally bind to is a powerful
tool that you can add to your code toolbox.

 

***const***

In addition to let , ES6 introduces const , which also creates a
blockscoped variable, but whose value is fixed (constant). Any attempt
to change that value at a later time results in an error.

 

var foo = true;

if (foo) {

var a = 2;

const b = 3; // block‐scoped to the containing \`if\`

a = 3; // just fine!

b = 4; // error!

}

console.log( a ); // 3

console.log( b ); // ReferenceError!

 

 

 

 

YDKJS - 3

Friday, April 08, 2016

10:38

 

 the this mechanism provides a more elegant way of implicitly "passing
along" an object reference, leading to cleaner API design and easier
re-use. For example, in below case objects me and you are passed using
this.

 

function identify() {\
return this.name.toUpperCase();\
}

function speak() {\
var greeting = "Hello, I'm " + identify.call( this );\
console.log( greeting );\
}

var me = {\
name: "Kyle"\
};

var you = {\
name: "Reader"\
};

identify.call( me ); // KYLE\
identify.call( you ); // READER

speak.call( me ); // Hello, I'm KYLE\
speak.call( you ); // Hello, I'm READER

 

 

To be clear, this does not, in any way, refer to a function's **lexical
scope**. It is true that internally, scope is kind of like an object
with properties for each of the available identifiers. But the scope
"object" is not accessible to JavaScript code. It's an inner part of
the *Engine*'s implementation.

 

Consider code which attempts (and fails!) to cross over the boundary and
use this to implicitly refer to a function's lexical scope:

 

function foo() {

var a = 2;

this.bar();

}

 

function bar() {

console.log( this.a );

}

 

foo(); //undefined

There's more than one mistake in this snippet. While it may seem
contrived, the code you see is a distillation of actual real-world code
that has been exchanged in public community help forums. It's a
wonderful (if not sad) illustration of just how misguided this
assumptions can be.

 

Firstly, an attempt is made to reference the bar() function via
this.bar(). It is almost certainly an accident that it works, but we'll
explain the how of that shortly. The most natural way to have invoked
bar() would have been to omit the leading this. and just make a lexical
reference to the identifier.

 

However, the developer who writes such code is attempting to use this to
create a bridge between the lexical scopes of foo() and bar(), so that
bar() has access to the variable a in the inner scope of foo(). No such
bridge is possible. You cannot use a this reference to look something up
in a lexical scope. It is not possible.

 

**Every time you feel yourself trying to mix lexical scope look-ups with
this, remind yourself: there is no bridge.**

 

***What's this?***

 

Having set aside various incorrect assumptions, let us now turn our
attention to how the this mechanism really works.

 

We said earlier that this is not an author-time binding but a runtime
binding. It is contextual based on the conditions of the function's
invocation. this binding has nothing to do with where a function is
declared, but has instead everything to do with the manner in which the
function is called.

 

When a function is invoked, an activation record, otherwise known as an
execution context, is created. This record contains information about
where the function was called from (the call-stack), how the function
was invoked, what parameters were passed, etc. One of the properties of
this record is the this reference which will be used for the duration of
that function's execution.

 

**this is neither a reference to the function itself, nor is it a
reference to the function's lexical scope. this is actually a binding
that is made when a function is invoked, and what it references is
determined entirely by the call-site where the function is called.**

 

***Call-site***

 

To understand this binding, we have to understand the call-site: the
location in code where a function is called (not where it's declared).
Finding the call-site is generally: "go locate where a function is
called from", but it's not always that easy, as certain coding patterns
can obscure the true call-site. What's important is to think about the
call-stack (the stack of functions that have been called to get us to
the current moment in execution). The call-site we care about is in the
invocation before the currently executing function

 

***Default Binding***

 

function foo() {

console.log( this.a );

}

 

var a = 2;

foo(); // 2

 

The first thing to note, if you were not already aware, is that
variables declared in the global scope, as var a = 2 is, are synonymous
with global-object properties of the same name. They're not copies of
each other, they are each other. Think of it as two sides of the same
coin.

in this case, the default binding for this applies to the function call,
and so points this at the global object.

 

In our snippet, foo() is called with a plain, un-decorated function
reference. None of the other rules we will demonstrate will apply here,
so the default binding applies instead. If strict mode is in effect, the
global object is not eligible for the default binding, so the this is
instead set to undefined. even though the overall this binding rules are
entirely based on the call-site, the global object is only eligible for
the default binding if the contents of foo() are not running in strict
mode; the strict mode state of the call-site of foo() is irrelevant.

 

function foo() {

console.log( this.a );

}

 

var a = 2;

 

(function(){

"use strict";

 

foo(); // 2

})();

 

***Implicit Binding***

 

function foo() {

console.log( this.a );

}

 

var obj = {

a: 2,

foo: foo

};

 

obj.foo(); // 2

 

at the point that foo() is called, it's preceded by an object reference
to obj. When there is a context object for a function reference, the
implicit binding rule says that it's that object which should be used
for the function call's this binding. Because obj is the this for the
foo() call, this.a is synonymous with obj.a.

 

Only the top/last level of an object property reference chain matters to
the call-site. For instance:

 

var obj2 = {

a: 42,

foo: foo

};

 

var obj1 = {

a: 2,

obj2: obj2

};

 

obj1.obj2.foo(); // 42

 

 

***Implicitly Lost***

 

One of the most common frustrations that this binding creates is when an
implicitly bound function loses that binding, which usually means it
falls back to the default binding, of either the global object or
undefined, depending on strict mode.

 

Consider:

function foo() {\
console.log( this.a );\
}

var obj = {\
a: 2,\
foo: foo\
};

var bar = obj.foo; // function reference/alias!

var a = "oops, global"; // \`a\` also property on global object

bar(); // "oops, global"

 

 

Even though bar appears to be a reference to obj.foo, in fact, it's
really just another reference to foo itself. Moreover, the call-site is
what matters, and the call-site is bar(), which is a plain, un-decorated
call and thus the default binding applies.

 

The more subtle, more common, and more unexpected way this occurs is
when we consider passing a callback function:

function foo() {\
console.log( this.a );\
}

function doFoo(fn) {\
// \`fn\` is just another reference to \`foo\`

fn(); // &lt;-- call-site!\
}

var obj = {\
a: 2,\
foo: foo\
};

var a = "oops, global"; // \`a\` also property on global object

doFoo( obj.foo ); // "oops, global"

Parameter passing is just an implicit assignment, and since we're
passing a function, it's an implicit reference assignment, so the end
result is the same as the previous snippet.

What if the function you're passing your callback to is not your own,
but built-in to the language? No difference, same outcome.

***Explicit Binding***

 

what if you want to force a function call to use a particular object for
the this binding, without putting a property function reference on the
object. "All" functions in the language have some utilities available to
them (via their \[\[Prototype\]\] -- more on that later) which can be
useful for this task. Specifically, functions have call(..) and
apply(..) methods. How do these utilities work? They both take, as their
first parameter, an object to use for the this, and then invoke the
function with that this specified. Since you are directly stating what
you want the this to be, we call it explicit binding

 

function foo() {\
console.log( this.a );\
}

var obj = {\
a: 2\
};

foo.call( obj ); // 2

Invoking foo with *explicit binding* by foo.call(..) allows us to force
its this to be obj.

If you pass a simple primitive value (of type string, boolean, or
number) as the this binding, the primitive value is wrapped in its
object-form (new String(..), new Boolean(..), or new Number(..),
respectively). This is often referred to as "boxing".

 

Unfortunately, explicit binding alone still doesn't offer any solution
to the issue mentioned previously, of a function "losing" its intended
this binding, or just having it paved over by a framework, etc.

 

***Hard Binding***

 

But a variation pattern around explicit binding actually does the trick.

 

function foo() {\
console.log( this.a );\
}

var obj = {\
a: 2\
};

var bar = function() {\
foo.call( obj );\
};

bar(); // 2\
setTimeout( bar, 100 ); // 2

// \`bar\` hard binds \`foo\`'s \`this\` to \`obj\`\
// so that it cannot be overriden\
bar.call( window ); // 2

 

 

We create a function bar() which, internally, manually calls
foo.call(obj), thereby forcibly invoking foo with obj binding for this.
No matter how you later invoke the function bar, it will always manually
invoke foo with obj. This binding is both explicit and strong, so we
call it hard binding.

 

Another way to express this pattern is to create a re-usable helper:

function foo(something) {\
console.log( this.a, something );\
return this.a + something;\
}

// simple \`bind\` helper\
function bind(fn, obj) {\
return function() {\
return fn.apply( obj, arguments );\
};\
}

var obj = {\
a: 2\
};

var bar = bind( foo, obj );

var b = bar( 3 ); // 2 3\
console.log( b ); // 5

 

Since *hard binding* is such a common pattern, it's provided with a
built-in utility as of ES5: Function.prototype.bind, and it's used like
this:

function foo(something) {\
console.log( this.a, something );\
return this.a + something;\
}

var obj = {\
a: 2\
};

var bar = foo.bind( obj );

var b = bar( 3 ); // 2 3\
console.log( b ); // 5

bind(..) returns a new function that is hard-coded to call the original
function with the this context set as you specified.

 

***API Call "Contexts"***

 

Many libraries' functions, and indeed many new built-in functions in the
JavaScript language and host environment, provide an optional parameter,
usually called "context", which is designed as a work-around for you not
having to use bind(..) to ensure your callback function uses a
particular this.

 

For instance:

function foo(el) {\
console.log( el, this.id );\
}

var obj = {\
id: "awesome"\
};

// use \`obj\` as \`this\` for \`foo(..)\` calls\
\[1, 2, 3\].forEach( foo, obj ); // 1 awesome 2 awesome 3 awesome

Internally, these various functions almost certainly use *explicit
binding* via call(..) or apply(..), saving you the trouble.

***new Binding***

 

 

JavaScript has a new operator, and the code pattern to use it looks
basically identical to what we see in those class-oriented languages;
most developers assume that JavaScript's mechanism is doing something
similar. However, there really is no connection to class-oriented
functionality implied by new usage in JS.

 

First, let's re-define what a "constructor" in JavaScript is. In JS,
constructors are just functions that happen to be called with the new
operator in front of them. They are not attached to classes, nor are
they instantiating a class. They are not even special types of
functions. They're just regular functions that are, in essence, hijacked
by the use of new in their invocation. So, pretty much any ol' function,
including the built-in object functions like Number(..) (see Chapter 3)
can be called with new in front of it, and that makes that function call
a constructor call. This is an important but subtle distinction: there's
really no such thing as "constructor functions", but rather construction
calls of functions.

 

When a function is invoked with new in front of it, otherwise known as a
constructor call, the following things are done automatically:

 

1.  a brand new object is created (aka, constructed) out of thin air

2.  the newly constructed object is \[\[Prototype\]\]-linked

3.  the newly constructed object is set as the this binding for that
    > function call

4.  unless the function returns its own alternate object, the
    > new-invoked function call will automatically return the newly
    > constructed object

 

***Everything In Order***

 

There must be an order of precedence to these rules, and so we will next
demonstrate what order to apply the rules. It should be clear that the
default binding is the lowest priority rule of the 4. explicit binding
takes precedence over implicit binding, which means you should ask first
if explicit binding applies before checking for implicit binding.

 

 

***Determining this***

Now, we can summarize the rules for determining this from a function
call's call-site, in their order of precedence. Ask these questions in
this order, and stop when the first rule applies.

1.  Is the function called with new (**new binding**)? If so, this is
    > the newly constructed object.\
    > var bar = new foo()

2.  Is the function called with call or apply (**explicit binding**),
    > even hidden inside a bind *hard binding*? If so, this is the
    > explicitly specified object.\
    > var bar = foo.call( obj2 )

3.  Is the function called with a context (**implicit binding**),
    > otherwise known as an owning or containing object? If
    > so, thisis *that* context object.\
    > var bar = obj1.foo()

4.  Otherwise, default the this (**default binding**). If in strict
    > mode, pick undefined, otherwise pick the global object.\
    > var bar = foo()

That's it. That's *all it takes* to understand the rules of this binding
for normal function calls.

 

 

-   If you pass null or undefined as a this binding parameter to call,
    > apply, or bind, those values are effectively ignored, and instead
    > the default binding rule applies to the invocation

 

 

 

 

YKDJS - 4

Tuesday, April 19, 2016

09:55

 

> ***Objects***
>
>  
>
> Objects come in two forms: the declarative (literal) form, and the
> constructed form.
>
> The literal syntax for an object looks like this:
>
> var myObj = {
>
> key: value
>
> // ...
>
> };
>
> The constructed form looks like this:
>
> var myObj = new Object();
>
> myObj.key = value;
>
>  
>
> The constructed form and the literal form result in exactly the same
> sort of object. The only difference really is that you can add one or
> more key/value pairs to the literal declaration, whereas with
> constructed-form objects, you must add the properties one-by-one.
>
>  
>
> ***Type***
>
> Objects are the general building block upon which much of JS is built.
> They are one of the 6 primary types (called "language types" in the
> specification) in JS:
>
>  
>
> string
>
> number
>
> boolean
>
> null
>
> undefined
>
> Object
>
>  
>
> Note that the simple primitives (string, number, boolean, null, and
> undefined) are not themselves objects. null is sometimes referred to
> as an object type, but this misconception stems from a bug in the
> language which causes typeof null to return the string "object"
> incorrectly (and confusingly). In fact, null is its own primitive
> type.
>
>  
>
> **It's a common mis-statement that "everything in JavaScript is an
> object". This is clearly not true.**
>
>  
>
> By contrast, there are a few special object sub-types, which we can
> refer to as complex primitives. **function** is a sub-type of object
> (technically, a "callable object"). Functions in JS are said to be
> "first class" in that they are basically just normal objects (with
> callable behavior semantics bolted on), and so they can be handled
> like any other plain object. **Arrays** are also a form of objects,
> with extra behavior. The organization of contents in arrays is
> slightly more structured than for general objects.
>
>  
>
> ***Built-in Objects***
>
>  
>
> There are several other object sub-types, usually referred to as
> built-in objects. For some of them, their names seem to imply they are
> directly related to their simple primitives counter-parts, but in
> fact, their relationship is more complicated
>
>  

-   String

-   Number

-   Boolean

-   Object

-   Function

-   Array

-   Date

-   RegExp

-   Error

>  
>
> var strPrimitive = "I am a string";
>
> typeof strPrimitive; // "string"
>
> strPrimitive instanceof String; // false
>
>  
>
> var strObject = new String( "I am a string" );
>
> typeof strObject; // "object"
>
> strObject instanceof String; // true
>
>  
>
> The primitive value "I am a string" is not an object, it's a primitive
> literal and immutable value. To perform operations on it, such as
> checking its length, accessing its individual character contents, etc,
> a String object is required. Luckily, the language automatically
> coerces a "string" primitive to a String object when necessary, which
> means you almost never need to explicitly create the Object form. It
> is strongly preferred by the majority of the JS community to use the
> literal form for a value, where possible, rather than the constructed
> object form.
>
>  
>
> The same sort of coercion happens between the number literal primitive
> 42 and the new Number(42) object wrapper, when using methods like
> 42.359.toFixed(2). Likewise for Boolean objects from "boolean"
> primitives. null and undefined have no object wrapper form, only their
> primitive values. By contrast, Date values can only be created with
> their constructed object form, as they have no literal form
> counter-part.
>
>  
>
> Since objects are created either way, the simpler literal form is
> almost universally preferred. Only use the constructed form if you
> need the extra options. Error objects are rarely created explicitly in
> code, but usually created automatically when exceptions are thrown.
> They can be created with the constructed form new Error(..), but it's
> often unnecessary.
>
>  
>
> ***Contents of Objects***
>
>  
>
> the contents of an object consist of values (any type) stored at
> specifically named locations, which we call **properties**. It's
> important to note that while we say "contents" which implies that
> these values are actually stored inside the object, that's merely an
> appearance. The engine stores values in implementation-dependent ways,
> and may very well not store them in some object container. What is
> stored in the container are these property names, which act as
> pointers (technically, references) to where the values are stored.
>
>  
>
> var myObject = {\
> a: 2\
> };
>
> myObject.a; // 2
>
> myObject\["a"\]; // 2
>
>  
>
> To access the value at the location a in myObject, we need to use
> either the . operator or the \[ \] operator. The .a syntax is usually
> referred to as "property" access, whereas the \["a"\] syntax is
> usually referred to as "key" access. In reality, they both access the
> same location, and will pull out the same value, 2, so the terms can
> be used interchangeably. The main difference between the two syntaxes
> is that the . operator requires an Identifier compatible property name
> after it, whereas the \[".."\] syntax can take basically any
> UTF-8/unicode compatible string as the name for the property. To
> reference a property of the name "Super-Fun!", for instance, you would
> have to use the \["Super-Fun!"\] access syntax, as Super-Fun! is not a
> valid Identifier property name. Also, since the \[".."\] syntax uses a
> string's value to specify the location, this means the program can
> programmatically build up the value of the string
>
>  
>
> In objects, property names are **always** strings. If you use any
> other value besides a string (primitive) as the property, it will
> first be converted to a string. This even includes numbers, which are
> commonly used as array indexes
>
>  
>
> var myObject = { };
>
> myObject\[true\] = "foo";\
> myObject\[3\] = "bar";\
> myObject\[myObject\] = "baz";
>
> myObject\["true"\]; // "foo"\
> myObject\["3"\]; // "bar"\
> myObject\["\[object Object\]"\]; // "baz"
>
>  
>
>  
>
> ***Computed Property Names***
>
>  
>
> ES6 adds computed property names, where you can specify an expression,
> surrounded by a \[ \] pair, in the key-name position of an
> object-literal declaration:
>
>  
>
> var prefix = "foo";
>
>  
>
> var myObject = {
>
> \[prefix + "bar"\]: "hello",
>
> \[prefix + "baz"\]: "world"
>
> };
>
>  
>
> myObject\["foobar"\]; // hello
>
> myObject\["foobaz"\]; // world
>
>  
>
> ***Arrays***
>
>  
>
> Arrays assume numeric indexing, which means that values are stored in
> locations, usually called indices, at non-negative integers, such as 0
> and 42.
>
>  
>
> var myArray = \[ "foo", 42, "bar" \];
>
> myArray.length; // 3
>
> myArray\[0\]; // "foo"
>
> myArray\[2\]; // "bar"
>
>  
>
> Arrays are objects, so even though each index is a positive integer,
> you can also add properties onto the array:
>
>  
>
> var myArray = \[ "foo", 42, "bar" \];
>
> myArray.baz = "baz";
>
> myArray.length; // 3
>
> myArray.baz; // "baz"
>
>  
>
> Notice that adding named properties (regardless of . or \[ \] operator
> syntax) does not change the reported length of the array. You could
> use an array as a plain key/value object, and never add any numeric
> indices, but this is a bad idea because arrays have behavior and
> optimizations specific to their intended use, and likewise with plain
> objects. Use objects to store key/value pairs, and arrays to store
> values at numeric indices
>
>  
>
> Be careful: If you try to add a property to an array, but the property
> name looks like a number, it will end up instead as a numeric index
> (thus modifying the array contents):
>
>  
>
> ***Property Descriptors***
>
>  
>
> Prior to ES5, the JavaScript language gave no direct way for your code
> to inspect or draw any distinction between the characteristics of
> properties, such as whether the property was read-only or not. But as
> of ES5, all properties are described in terms of a property
> descriptor.
>
>  
>
> var myObject = {\
> a: 2\
> };
>
> Object.getOwnPropertyDescriptor( myObject, "a" );\
> // {\
> // value: 2,\
> // writable: true,\
> // enumerable: true,\
> // configurable: true\
> // }
>
>  
>
> we can use Object.defineProperty(..) to add a new property, or modify
> an existing one (if it's configurable!), with the desired
> characteristics.
>
>  
>
> var myObject = {};
>
> Object.defineProperty( myObject, "a", {\
> value: 2,\
> writable: true,\
> configurable: true,\
> enumerable: true\
> } );
>
> myObject.a; // 2
>
>  
>
> The ability for you to change the value of a property is controlled
> by **writable**. As you can see, when non writable, our modification
> of the value silently failed. If we try in strict mode, we get an
> error:
>
>  Be careful: as you can see, changing configurable to false is
> a **one-way action, and cannot be undone!.** There's a nuanced
> exception to be aware of: even if the property is already
> configurable:false, writable can always be changed from true to false
> without error, but not back to true if already false**.** Another
> thing configurable:false prevents is the ability to use the delete
> operator to remove an existing property. Enumerable, name probably
> makes it obvious, but this characteristic controls if a property will
> show up in certain object-property enumerations, such as the for..in
> loop
>
>  
>
> It is sometimes desired to make properties or objects that cannot be
> changed (either by accident or intentionally). It's important to note
> that all of these approaches create shallow immutability. That is,
> they affect only the object and its direct property characteristics.
> If an object has a reference to another object (array, object,
> function, etc), the contents of that object are not affected, and
> remain mutable.
>
>  
>
> By combining writable:false and configurable:false, you can
> essentially create a constant (cannot be changed, redefined or
> deleted) as an object property, like:
>
> var myObject = {};
>
> Object.defineProperty( myObject, "FAVORITE\_NUMBER", {\
> value: 42,\
> writable: false,\
> configurable: false\
> } );
>
>  
>
>  
>
> If you want to prevent an object from having new properties added to
> it, but otherwise leave the rest of the object's properties alone,
> call **Object.preventExtensions(..):**
>
> **Object.seal(..)** creates a "sealed" object, which means it takes an
> existing object and essentially calls Object.preventExtensions(..) on
> it, but also marks all its existing properties as configurable:false.
> So, not only can you not add any more properties, but you also cannot
> reconfigure or delete any existing properties (though you can still
> modify their values).
>
>  
>
> **Object.freeze(..)** creates a frozen object, which means it takes an
> existing object and essentially calls Object.seal(..) on it, but it
> also marks all "data accessor" properties as writable:false, so that
> their values cannot be changed. This approach is the highest level of
> immutability that you can attain for an object itself, as it prevents
> any changes to the object or to any of its direct properties (though,
> as mentioned above, the contents of any referenced other objects are
> unaffected). You could "deep freeze" an object by calling
> Object.freeze(..) on the object, and then recursively iterating over
> all objects it references
>
>  
>
> ***Retrieving and Setting Properties from objects***
>
>  
>
> The myObject.a is a property access, but it doesn't just look in
> myObject for a property of the name a, as it might seem. According to
> the spec, the code above actually performs a \[\[Get\]\] operation
> (kinda like a function call: \[\[Get\]\]()) on the myObject. The
> default built-in \[\[Get\]\] operation for an object first inspects
> the object for a property of the requested name, and if it finds it,
> it will return the value accordingly. But one important result of this
> \[\[Get\]\] operation is that if it cannot through any means come up
> with a value for the requested property, it instead returns the value
> undefined.
>
>  
>
> This behavior is different from when you reference variables by their
> identifier names. If you reference a variable that cannot be resolved
> within the applicable lexical scope look-up, the result is not
> undefined as it is for object properties, but instead a ReferenceError
> is thrown.
>
>  
>
> Since there's an internally defined \[\[Get\]\] operation for getting
> a value from a property, it should be obvious there's also a default
> \[\[Put\]\] operation. It may be tempting to think that an assignment
> to a property on an object would just invoke \[\[Put\]\] to set or
> create that property on the object in question. But the situation is
> more nuanced than that. When invoking \[\[Put\]\], how it behaves
> differs based on a number of factors, including (most impactfully)
> whether the property is already present on the object or not.
>
>  
>
> If the property is present, the \[\[Put\]\] algorithm will roughly
> check:
>
>  

-   Is the property an accessor descriptor (see "Getters & Setters"
    > section below)? If so, call the setter, if any.

-   Is the property a data descriptor with writable of false? If so,
    > silently fail in non-strict mode, or throw TypeError in
    > strict mode.

-   Otherwise, set the value to the existing property as normal.

> If the property is not yet present on the object in question, the
> \[\[Put\]\] operation is even more nuanced and complex
>
>  
>
> ***Getters & Setters***
>
>  
>
> The default \[\[Put\]\] and \[\[Get\]\] operations for objects
> completely control how values are set to existing or new properties,
> or retrieved from existing properties, respectively. ES5 introduced a
> way to override part of these default operations, not on an object
> level but a per-property level, through the use of getters and
> setters. Getters are properties which actually call a hidden function
> to retrieve a value. Setters are properties which actually call a
> hidden function to set a value. When you define a property to have
> either a getter or a setter or both, its definition becomes an
> "accessor descriptor" (as opposed to a "data descriptor"). For
> accessor-descriptors, the value and writable characteristics of the
> descriptor are moot and ignored, and instead JS considers the set and
> get characteristics of the property (as well as configurable and
> enumerable).
>
>  
>
>  
>
> var myObject = {\
> // define a getter for \`a\`\
> get a() {\
> return 2;\
> }\
> };
>
> myObject.a = 3;
>
> myObject.a; // 2
>
> Since we only defined a getter for a, if we try to set the value
> of a later, the set operation won't throw an error but will just
> silently throw the assignment away. Even if there was a valid setter,
> our custom getter is hard-coded to return only 2, so the set operation
> would be moot.
>
>  
>
> To make this scenario more sensible, properties should also be defined
> with setters, which override the default \[\[Put\]\] operation (aka,
> assignment), per-property, just as you'd expect.
>
>  
>
> var myObject = {\
> // define a getter for \`a\`\
> get a() {\
> return this.\_a\_;\
> },
>
> // define a setter for \`a\`\
> set a(val) {\
> this.\_a\_ = val \* 2;\
> }\
> };
>
> myObject.a = 2;
>
> myObject.a; // 4
>
>  
>
> The \_a\_ name is purely by convention for this example and implies
> nothing special about its behavior
>
>  
>
> ***Existence***
>
>  
>
> We can ask an object if it has a certain property without asking to
> get that property's value:
>
>  
>
> var myObject = {\
> a: 2\
> };
>
> ("a" in myObject); // true\
> ("b" in myObject); // false
>
> myObject.hasOwnProperty( "a" ); // true\
> myObject.hasOwnProperty( "b" ); // false
>
>  
>
>  
>
> The in operator will check to see if the property is in the object, or
> if it exists at any higher level of the \[\[Prototype\]\] chain object
> traversal (see Chapter 5). By contrast, hasOwnProperty(..) checks to
> see if only myObject has the property or not, and will not consult the
> \[\[Prototype\]\] chain.
>
>  
>
> ***Iteration***
>
>  
>
> ES5 also added several iteration helpers for arrays, including
> forEach(..), every(..), and some(..). Each of these helpers accepts a
> function callback to apply to each element in the array, differing
> only in they respectively respond to a return value from the callback.
> forEach(..) will iterate over all values in the array, and ignores any
> callback return values. every(..) keeps going until the end or the
> callback returns a false (or "falsy") value, whereas some(..) keeps
> going until the end or the callback returns a true (or "truthy")
> value. These special return values inside every(..) and some(..) act
> somewhat like a break statement inside a normal for loop, in that they
> stop the iteration early before it reaches the end. If you iterate on
> an object with a for..in loop, you're also only getting at the values
> indirectly, because it's actually iterating only over the enumerable
> properties of the object, leaving you to access the properties
> manually to get the values.
>
>  
>
> But what if you want to iterate over the values directly instead of
> the array indices (or object properties)? Helpfully, ES6 adds a
> for..of loop syntax for iterating over arrays (and objects, if the
> object defines its own custom iterator): The for..of loop asks for an
> iterator object (from a default internal function known as @@iterator
> in spec-speak) of the thing to be iterated, and the loop then iterates
> over the successive return values from calling that iterator object's
> next() method, once for each loop iteration. Arrays have a built-in
> @@iterator, so for..of works easily on them
>
>  
>
> ***JavaScript Classes***
>
>  
>
> JS has had some class-like syntactic elements (like new and
> instanceof) for quite awhile, and more recently in ES6, some
> additions, like the class keyword.But does that mean JavaScript
> actually has classes? Plain and simple: No.
>
>  

 

 

YDKJS - 5

Tuesday, April 19, 2016

11:39

***Prototypes***

 

Objects in JavaScript have an internal property, denoted in the
specification as \[\[Prototype\]\], which is simply a reference to
another object. Almost all objects are given a non-null value for this
property, at the time of their creation.

The default \[\[Get\]\] operation proceeds to follow the
\[\[Prototype\]\] link of the object if it cannot find the requested
property on the object directly.

 

var anotherObject = {\
a: 2\
};

// create an object linked to \`anotherObject\`\
var myObject = Object.create( anotherObject );

myObject.a; // 2

 

So, we have myObject that is now \[\[Prototype\]\] linked to
anotherObject. Clearly myObject.a doesn't actually exist, but
nevertheless, the property access succeeds (being found on anotherObject
instead) and indeed finds the value 2. But, if a weren't found on
anotherObject either, its \[\[Prototype\]\] chain, if non-empty, is
again consulted and followed.

This process continues until either a matching property name is found,
or the \[\[Prototype\]\] chain ends. If no matching property is ever
found by the end of the chain, the return result from the \[\[Get\]\]
operation is undefined

 

Similar to this \[\[Prototype\]\] chain look-up process, if you use a
for..in loop to iterate over an object, any property that can be reached
via its chain (and is also enumerable -- see Chapter 3) will be
enumerated. If you use the in operator to test for the existence of a
property on an object, in will check the entire chain of the object
(regardless of enumerability).

 

The top-end of every normal \[\[Prototype\]\] chain is the built-in
Object.prototype. This object includes a variety of common utilities
used all over JS, because all normal (built-in, not host-specific
extension) objects in JavaScript "descend from" (aka, have at the top of
their \[\[Prototype\]\] chain) the Object.prototype object. Some
utilities found here you may be familiar with include .toString() and
.valueOf().

 

myObject.foo = "bar";

If the myObject object already has a normal data accessor property
called foo directly present on it, the assignment is as simple as
changing the value of the existing property.

If foo is not already present directly on myObject,
the \[\[Prototype\]\] chain is traversed, just like for
the \[\[Get\]\] operation. If foo is not found anywhere in the chain,
the property foo is added directly to myObject with the specified value,
as expected. However, if foo is already present somewhere higher in the
chain, nuanced (and perhaps surprising) behavior can occur with
the myObject.foo = "bar" assignment

 

If the property name foo ends up both on myObject itself and at a higher
level of the \[\[Prototype\]\] chain that starts at myObject, this is
called shadowing. The foo property directly on myObject shadows any foo
property which appears higher in the chain, because the myObject.foo
look-up would always find the foo property that's lowest in the chain.

 

-   If a normal data accessor (see Chapter 3) property named foo is
    > found anywhere higher on the \[\[Prototype\]\] chain,and it's not
    > marked as read-only (writable:false) then a new property
    > called foo is added directly to myObject, resulting in
    > a shadowed property.

-   If a foo is found higher on the \[\[Prototype\]\] chain, but it's
    > marked as read-only (writable:false), then both the setting of
    > that existing property as well as the creation of the shadowed
    > property on myObject are disallowed. If the code is running
    > in strict mode, an error will be thrown. Otherwise, the setting of
    > the property value will silently be ignored. Either way, no
    > shadowing occurs.

-   If a foo is found higher on the \[\[Prototype\]\] chain and it's a
    > setter (see Chapter 3), then the setter will always be called.
    > No foo will be added to (aka, shadowed on) myObject, nor will
    > the foo setter be redefined.

 

 

Most developers assume that assignment of a property (\[\[Put\]\]) will
always result in shadowing if the property already exists higher on the
\[\[Prototype\]\] chain, but as you can see, that's only true in one
(\#1) of the three situations just described. If you want to shadow foo
in cases \#2 and \#3, you cannot use = assignment, but must instead use
Object.defineProperty(..)

 

 

 

 

YDKJS - 6

Tuesday, April 19, 2016

12:08

If you have the number value 42, but you want to treat it like a string,
such as pulling out the "2" as a character in position 1, you obviously
must first convert (coerce) the value from number to string. But there
are many different ways that such coercion can happen. Some of these
ways are explicit, easy to reason about, and reliable. But if you're not
careful, coercion can happen in very strange and surprising ways.

 

**Built-in Types**

JavaScript defines seven built-in types:

-   null

-   undefined

-   boolean

-   number

-   string

-   object

-   symbol -- added in ES6!

 

The typeof operator inspects the type of the given value, and always
returns one of seven string values

 

It would have been nice (and correct!) if it returned "null", but this
original bug in JS has persisted for nearly two decades, and will likely
never be fixed because there's too much existing web content that relies
on its buggy behavior that "fixing" the bug would create more "bugs" and
break a lot of web software.

 

If you want to test for a null value using its type, you need a compound
condition:

 

var a = null;

(!a && typeof a === "object"); // true

 

null is the only primitive value that is "falsy"

 

***Values as Types***

 

In JavaScript, variables don't have types -- values have types.
Variables can hold any value, at any time. Another way to think about JS
types is that JS doesn't have "type enforcement," in that the engine
doesn't insist that a variable always holds values of the same initial
type that it starts out with. A variable can, in one assignment
statement, hold a string, and in the next hold a number, and so on.

 

The value 42 has an intrinsic type of number, and its type cannot be
changed. Another value, like "42" with the string type, can be created
from the number value 42 through a process called coercion.

If you use typeof against a variable, it's not asking "what's the type
of the variable?" as it may seem, since JS variables have no types.
Instead, it's asking "what's the type of the value in the variable?"

 

Variables that have no value currently, actually have the undefined
value. Calling typeof against such variables will return "undefined": An
"undefined" variable is one that has been declared in the accessible
scope, but at the moment has no other value in it. By contrast, an
"undeclared" variable is one that has not been formally declared in the
accessible scope.

 

***Arrays***

 

var a = \[ 1, "2", \[3\] \];

a.length; // 3\
a\[0\] === 1; // true\
a\[2\]\[0\] === 3; // true

 

Using delete on an array value will remove that slot from the array, but
even if you remove the final element, it does not update the length
property, so be careful!

 

Be careful about creating "sparse" arrays (leaving or creating
empty/missing slots):

var a = \[ \];

a\[0\] = 1;\
// no \`a\[1\]\` slot set here\
a\[2\] = \[ 3 \];

a\[1\]; // undefined

a.length; // 3

 

arrays are numerically indexed (as you'd expect), but the tricky thing
is that they also are objects that can have stringkeys/properties added
to them (but which don't count toward the length of the array):

 

var a = \[ \];

a\[0\] = 1;\
a\["foobar"\] = 2;

a.length; // 1\
a\["foobar"\]; // 2\
a.foobar; // 2

 

 

***Array-Likes***

 

One very common way to make such a conversion is to borrow
the slice(..) utility against the value:

function foo() {\
var arr = Array.prototype.slice.call( arguments );\
arr.push( "bam" );\
console.log( arr );\
}

foo( "bar", "baz" ); // \["bar","baz","bam"\]

If slice() is called without any other parameters, as it effectively is
in the above snippet, the default values for its parameters have the
effect of duplicating the array (or, in this case, array-like). As of
ES6, there's also a built-in utility called Array.from(..) that can do
the same task:

 

***Strings***

 

It's a very common belief that strings are essentially just arrays of
characters. While the implementation under the covers may or may not use
arrays, it's important to realize that JavaScript strings are really not
the same as arrays of characters. The similarity is mostly just
skin-deep.

 

var a = "foo";

var b = \["f","o","o"\];

Strings do have a shallow resemblance to arrays -- array-likes, as above
-- for instance, both of them having a length property, an indexOf(..)
method

 

JavaScript strings are immutable, while arrays are quite mutable.
Moreover, the a\[1\] character position access form was not always
widely valid JavaScript. Older versions of IE did not allow that syntax
(but now they do). Instead, the correct approach has been a.charAt(1). A
further consequence of immutable strings is that none of the string
methods that alter its contents can modify in-place, but rather must
create and return new strings. By contrast, many of the methods that
change array contents actually do modify in-place.

 

Also, many of the array methods that could be helpful when dealing
with strings are not actually available for them, but we can "borrow"
non-mutation array methods against our string:

a.join; // undefined\
a.map; // undefined

var c = Array.prototype.join.call( a, "-" );\
var d = Array.prototype.map.call( a, function(v){\
return v.toUpperCase() + ".";\
} ).join( "" );

c; // "f-o-o"\
d;

 

***Numbers***

 

Very large or very small numbers will by default be outputted in
exponent form, the same as the output of thetoExponential() method,
like:

var a = 5E10;\
a; // 50000000000\
a.toExponential(); // "5e+10"

 

 

Because number values can be boxed with the Number object wrapper (see
Chapter 3), number values can access methods that are built into the
Number.prototype

 

you have to be careful with the . operator. Since . is a valid numeric
character, it will first be interpreted as part of the number literal,
if possible, instead of being interpreted as a property accessor.

// invalid syntax:\
42.toFixed( 3 ); // SyntaxError

// these are all valid:\
(42).toFixed( 3 ); // "42.000"\
0.42.toFixed( 3 ); // "0.420"\
42..toFixed( 3 ); // "42.000"

 

 

NaN literally stands for "not a number",

 

 

var a = 2 / "foo"; // NaN

typeof a === "number"; // true

 

In other words: "the type of not-a-number is 'number'!" Hooray for
confusing names and semantics. NaN is a kind of "sentinel value" (an
otherwise normal value that's assigned a special meaning) that
represents a special kind of error condition within the number set. The
error condition is, in essence: "I tried to perform a mathematic
operation but failed, so here's the failed number result instead."

 

So, if you have a value in some variable and want to test to see if it's
this special failed-number NaN, you might think you could directly
compare to NaN itself, as you can with any other value,
like null or undefined. Nope.

var a = 2 / "foo";

a == NaN; // false\
a === NaN; // false

NaN is a very special value in that it's never equal to
another NaN value (i.e., it's never equal to itself). It's the only
value, in fact, that is not reflexive (without the Identity
characteristic x === x). So, NaN !== NaN. 

 

We use the built-in global utility called isNaN(..) and it tells us if
the value is NaN or not

 

The isNaN(..) utility has a fatal flaw. It appears it tried to take the
meaning of NaN ("Not a Number") too literally --

 

var a = 2 / "foo";\
var b = "foo";

a; // NaN\
b; // "foo"

window.isNaN( a ); // true\
window.isNaN( b ); // true -- ouch!

 

***Value vs. Reference***

 

In many other languages, values can either be assigned/passed by
value-copy or by reference-copy depending on the syntax you use.

 

In JavaScript, there are no pointers, and references work a bit
differently. You cannot have a reference from one JS variable to another
variable. That's just not possible. A reference in JS points at a
(shared) value, so if you have 10 different references, they are all
always distinct references to a single shared value; none of them are
references/pointers to each other.

 

var a = 2;\
var b = a; // \`b\` is always a copy of the value in \`a\`\
b++;\
a; // 2\
b; // 3

var c = \[1,2,3\];\
var d = c; // \`d\` is a reference to the shared \`\[1,2,3\]\` value\
d.push( 4 );\
c; // \[1,2,3,4\]\
d; // \[1,2,3,4\]

 

Simple values (aka scalar primitives) are always assigned/passed by
value-copy: null, undefined, string, number, boolean, and ES6's symbol.
Compound values -- objects (including arrays, and all boxed object
wrappers -- see Chapter 3) and functions -- always create a copy of the
reference on assignment or passing.

 

In the above snippet, because 2 is a scalar primitive, a holds one
initial copy of that value, and b is assigned another copy of the value.
When changing b, you are in no way changing the value in a. But both c
and d are separate references to the same shared value \[1,2,3\], which
is a compound value. It's important to note that neither c nor d more
"owns" the \[1,2,3\] value -- both are just equal peer references to the
value. So, when using either reference to modify (.push(4)) the actual
shared array value itself, it's affecting just the one shared value, and
both references will reference the newly modified value \[1,2,3,4\].

 

Since references point to the values themselves and not to the
variables, you cannot use one reference to change where another
reference is pointed:

 

var a = \[1,2,3\];\
var b = a;\
a; // \[1,2,3\]\
b; // \[1,2,3\]

// later\
b = \[4,5,6\];\
a; // \[1,2,3\]\
b; // \[4,5,6\]

When we make the assignment b = \[4,5,6\], we are doing absolutely
nothing to affect where a is still referencing (\[1,2,3\]). To do
that, b would have to be a pointer to a rather than a reference to
the array -- but no such capability exists in JS!

 

The most common way such confusion happens is with function parameters:

function foo(x) {\
x.push( 4 );\
x; // \[1,2,3,4\]

// later\
x = \[4,5,6\];\
x.push( 7 );\
x; // \[4,5,6,7\]\
}

var a = \[1,2,3\];

foo( a );

a; // \[1,2,3,4\] not \[4,5,6,7\]

 

***Boxing Wrappers***

 

Primitive values don't have properties or methods, so to access .length
or .toString() you need an object wrapper around the value. Thankfully,
JS will automatically box (aka wrap) the primitive value to fulfill such
accesses.

 

var a = "abc";

a.length; // 3

a.toUpperCase(); // "ABC"

 

So, if you're going to be accessing these properties/methods on your
string values regularly, like a i &lt; a.length condition in a for loop
for instance, it might seem to make sense to just have the object form
of the value from the start, so the JS engine doesn't need to implicitly
create it for you. But it turns out that's a bad idea. Browsers long ago
performance-optimized the common cases like .length, which means your
program will actually go slower if you try to "preoptimize" by directly
using the object form (which isn't on the optimized path). In general,
there's basically no reason to use the object form directly. It's better
to just let the boxing happen implicitly where necessary. In other
words, never do things like new String("abc"), new Number(42), etc --
always prefer using the literal primitive values "abc" and 42.

 

consider Boolean wrapped values:

 

var a = new Boolean( false );

 

if (!a) {

console.log( "Oops" ); // never runs

}

The problem is that you've created an object wrapper around the false
value, but objects themselves are "truthy" (see Chapter 4), so using the
object behaves oppositely to using the underlying false value itself,
which is quite contrary to normal expectation.

 

If you want to manually box a primitive value, you can use
the Object(..) function (no new keyword):

var a = "abc";\
var b = new String( a );\
var c = Object( a );

typeof a; // "string"\
typeof b; // "object"\
typeof c; // "object"

b instanceof String; // true\
c instanceof String; // true

Object.prototype.toString.call( b ); // "\[object String\]"\
Object.prototype.toString.call( c ); // "\[object String\]"

 

***Unboxing***

 

If you have an object wrapper and you want to get the underlying
primitive value out, you can use the valueOf() method:

 

var a = new String( "abc" );

var b = new Number( 42 );

var c = new Boolean( true );

 

a.valueOf(); // "abc"

b.valueOf(); // 42

c.valueOf(); // true

Unboxing can also happen implicitly, when using an object wrapper value
in a way that requires the primitive value.

 

***Array***

var a = new Array( 1, 2, 3 );\
a; // \[1, 2, 3\]

The Array(..) constructor does not require the new keyword in front of
it. If you omit it, it will behave as if you have used it anyway. So
Array(1,2,3) is the same outcome as new Array(1,2,3). The Array
constructor has a special form where if only one number argument is
passed, instead of providing that value as contents of the array, it's
taken as a length to "presize the array" (well, sorta). This is a
terrible idea. Firstly, you can trip over that form accidentally, as
it's easy to forget. But more importantly, there's no such thing as
actually presizing the array. Instead, what you're creating is an
otherwise empty array, but setting the length property of the array to
the numeric value specified. An array that has no explicit values in its
slots, but has a length property that implies the slots exist, is a
weird exotic type of data structure in JS with some very strange and
confusing behavior. An array with at least one "empty slot" in it is
often called a "sparse array."

 

***Date(..) and Error(..)***

 

The Date(..) and Error(..) native constructors are much more useful than
the other natives, because there is no literal form for either. To
create a date object value, you must use new Date(). The Date(..)
constructor accepts optional arguments to specify the date/time to use,
but if omitted, the current date/time is assumed. By far the most common
reason you construct a date object is to get the current timestamp value
(a signed integer number of milliseconds since Jan 1, 1970). You can do
this by calling getTime() on a date object instance. But an even easier
way is to just call the static helper function defined as of ES5:
Date.now()

 

If you call Date() without new, you'll get back a string representation
of the date/time at that moment. The exact form of this representation
is not specified in the language spec, though browsers tend to agree on
something close to: "Fri Jul 18 2014 00:31:02 GMT-0500 (CDT)"

 

The Error(..) constructor (much like Array() above) behaves the same
with the new keyword present or omitted.

The main reason you'd want to create an error object is that it captures
the current execution stack context into the object (in most JS engines,
revealed as a read-only .stack property once constructed). This stack
context includes the function call-stack and the line-number where the
error object was created, which makes debugging that error much easier.

You would typically use such an error object with the throw operator:

function foo(x) {\
if (!x) {\
throw new Error( "x wasn't provided" );\
}\
// ..\
}

 

***Native Prototypes***

 

Each of the built-in native constructors has its own .prototype object
-- Array.prototype, String.prototype, etc. These objects contain
behavior unique to their particular object subtype. For example, all
string objects, and by extension (via boxing) string primitives, have
access to default behavior as methods defined on the String.prototype
object.

 

 

 

 

YDKJS - 7

Wednesday, April 20, 2016

10:40

 

> ***Coercion***
>
>  
>
> Converting a value from one type to another is often called "type
> casting," when done explicitly, and "coercion" when done implicitly
> (forced by the rules of how a value is used). It may not be obvious,
> but JavaScript coercions always result in one of the scalar primitive
> values, like string, number, or boolean. There is no coercion that
> results in a complex value like object or function.
>
> Another way these terms are often distinguished is as follows: "type
> casting" (or "type conversion") occur in statically typed languages at
> compile time, while "type coercion" is a runtime conversion for
> dynamically typed languages.
>
>  
>
> ***ToString***
>
>  
>
> When any non-string value is coerced to a string representation, the
> conversion is handled by the ToString abstract operation in section
> 9.8 of the specification. Built-in primitive values have natural
> stringification: null becomes "null", undefined becomes "undefined"
> and true becomes "true". numbers are generally expressed in the
> natural way you'd expect, but , very small or very large numbers are
> represented in exponent form:
>
> For regular objects, unless you specify your own, the default
> toString() (located in Object.prototype.toString()) will return the
> internal \[\[Class\]\] like for instance "\[object Object\]".
>
> But as shown earlier, if an object has its own toString() method on
> it, and you use that object in a string-like way, its toString() will
> automatically be called, and the string result of that call will be
> used instead.
>
> Arrays have an overridden default toString() that stringifies as the
> (string) concatenation of all its values (each stringified
> themselves), with "," in between each value:
>
>  
>
> ***JSON Stringification***
>
>  
>
> For most simple values, JSON stringification behaves basically the
> same as toString() conversions, except that the serialization result
> is always a string:
>
>  
>
> JSON.stringify( 42 ); // "42"
>
> JSON.stringify( "42" ); // ""42"" (a string with a quoted string value
> in it)
>
> JSON.stringify( null ); // "null"
>
> JSON.stringify( true ); // "true"
>
> Any JSON-safe value can be stringified by JSON.stringify(..). But what
> is JSON-safe? Any value that can be represented validly in a JSON
> representation. The JSON.stringify(..) utility will automatically omit
> undefined, function, and symbol values when it comes across them. If
> such a value is found in an array, that value is replaced by null (so
> that the array position information isn't altered). If found as a
> property of an object, that property will simply be excluded
>
>  
>
> But if you try to JSON.stringify(..) an object with circular
> reference(s) in it, an error will be thrown. JSON stringification has
> the special behavior that if an object value has a toJSON() method
> defined, this method will be called first to get a value to use for
> serialization.If you intend to JSON stringify an object that may
> contain illegal JSON value(s), or if you just have values in the
> object that aren't appropriate for the serialization, you should
> define a toJSON() method for it that returns a JSON-safe version of
> the object.
>
>  
>
> It's a very common misconception that toJSON() should return a JSON
> stringification representation. That's probably incorrect, unless
> you're wanting to actually stringify the string itself (usually not!).
> toJSON() should return the actual regular value (of whatever type)
> that's appropriate, and JSON.stringify(..) itself will handle the
> stringification. In other words, toJSON() should be interpreted as "to
> a JSON-safe value suitable for stringification," not "to a JSON
> string" as many developers mistakenly assume.
>
>  
>
> An optional second argument can be passed to JSON.stringify(..) that
> is called **replacer**. This argument can either be an array or a
> function. It's used to customize the recursive serialization of an
> object by providing a filtering mechanism for which properties should
> and should not be included, in a similar way to how toJSON() can
> prepare a value for serialization.
>
> If replacer is an array, it should be an array of strings, each of
> which will specify a property name that is allowed to be included in
> the serialization of the object. If a property exists that isn't in
> this list, it will be skipped. If replacer is a function, it will be
> called once for the object itself, and then once for each property in
> the object, and each time is passed two arguments, key and value. To
> skip a key in the serialization, return undefined. Otherwise, return
> the value provided.
>
>  
>
> var a = {\
> b: 42,\
> c: "42",\
> d: \[1,2,3\]\
> };
>
> JSON.stringify( a, \["b","c"\] ); // "{"b":42,"c":"42"}"
>
> JSON.stringify( a, function(k,v){\
> if (k !== "c") return v;\
> } );\
> // "{"b":42,"d":\[1,2,3\]}"
>
>  
>
> A third optional argument can also be passed to JSON.stringify(..),
> called **space**, which is used as indentation for prettier
> human-friendly output. space can be a positive integer to indicate how
> many space characters should be used at each indentation level. Or,
> space can be a string, in which case up to the first ten characters of
> its value will be used for each indentation level
>
>  
>
> var a = {\
> b: 42,\
> c: "42",\
> d: \[1,2,3\]\
> };
>
> JSON.stringify( a, null, 3 );\
> // "{\
> // "b": 42,\
> // "c": "42",\
> // "d": \[\
> // 1,\
> // 2,\
> // 3\
> // \]\
> // }"
>
> JSON.stringify( a, null, "-----" );\
> // "{\
> // -----"b": 42,\
> // -----"c": "42",\
> // -----"d": \[\
> // ----------1,\
> // ----------2,\
> // ----------3\
> // -----\]\
> // }"
>
>  
>
> ***ToNumber***
>
>  
>
> ToNumber for a string value essentially works for the most part like
> the rules/syntax for numeric literals . If it fails, the result is
> NaN. Objects (and arrays) will first be converted to their primitive
> value equivalent, and the resulting value (if a primitive but not
> already a number) is coerced to a number according to the ToNumber
> rules just mentioned.
>
>  
>
> ***ToBoolean***
>
>  
>
> First and foremost, JS has actual keywords true and false, and they
> behave exactly as you'd expect of boolean values. It's a common
> misconception that the values 1 and 0 are identical to true/false.
> While that may be true in other languages, in JS the numbers are
> numbers and the booleans are booleans. You can coerce 1 to true (and
> vice versa) or 0 to false (and vice versa). But they're not the same.
>
>  
>
> All of JavaScript's values can be divided into two categories:

1.  values that will become false if coerced to boolean

2.  everything else (which will obviously become true)

>  
>
> From that table, we get the following as the so-called "falsy" values
> list:
>
>  
>
> undefined
>
> null
>
> false
>
> +0, -0, and NaN
>
> ""
>
> That's it. If a value is on that list, it's a "falsy" value, and it
> will coerce to false if you force a boolean coercion on it. By logical
> conclusion, if a value is not on that list, it must be on another
> list, which we call the "truthy" values list. But JS doesn't really
> define a "truthy" list per se. It gives some examples, such as saying
> explicitly that all objects are truthy, but mostly the spec just
> implies: anything not explicitly on the falsy list is therefore
> truthy.
>
>  
>
> ***Falsy Objects***
>
>  
>
> spec calls all objects truthy, right? There should be no such thing as
> a "falsy object." What could that possibly even mean?
>
> Consider:
>
> var a = new Boolean( false );\
> var b = new Number( 0 );\
> var c = new String( "" );
>
> We know all three values here are objects (see Chapter 3) wrapped
> around obviously falsy values. But do these objects behave as true or
> as false? That's easy to answer:
>
> var d = Boolean( a && b && c );
>
> d; // true
>
> So, all three behave as true, as that's the only way d could end up
> as true.
>
> So, if "falsy objects" are not just objects wrapped around falsy
> values, what the heck are they? The tricky part is that they can show
> up in your JS program, but they're not actually part of JavaScript
> itself. There are certain cases where browsers have created their own
> sort of exotic values behavior, namely this idea of "falsy objects,"
> on top of regular JS semantics. A "falsy object" is a value that looks
> and acts like a normal object (properties, etc.), but when you coerce
> it to a boolean, it coerces to a false value.
>
>  
>
> ***Truthy Values***
>
>  
>
> Consider:
>
> var a = "false";\
> var b = "0";\
> var c = "''";
>
> var d = Boolean( a && b && c );
>
> d;
>
> What value do you expect d to have here? It's gotta be
> either true or false.
>
> It's true. Why? Because despite the contents of those string values
> looking like falsy values, the string values themselves are all
> truthy, because "" is the only string value on the falsy list.
>
>  
>
> var a = \[\]; // empty array -- truthy or falsy?\
> var b = {}; // empty object -- truthy or falsy?\
> var c = function(){}; // empty function -- truthy or falsy?
>
> var d = Boolean( a && b && c );
>
> d;
>
> Yep, you guessed it, d is still true here. Why? Same reason as before.
> Despite what it may seem like, \[\], {}, andfunction(){} are not on
> the falsy list, and thus are truthy values.
>
>  
>
>  
>
> ***Explicit Coercion***
>
>  
>
> To coerce between strings and numbers, we use the built-in String(..)
> and Number(..) functions (which we referred to as "native
> constructors" but very importantly, we do not use the new keyword in
> front of them. As such, we're not creating object wrappers. Instead,
> we're actually explicitly coercing between the two types
>
>  
>
> var a = 42;\
> var b = String( a );
>
> var c = "3.14";\
> var d = Number( c );
>
> b; // "42"\
> d; // 3.14
>
>  
>
> Besides String(..) and Number(..), there are other ways to
> "explicitly" convert these values between string and number:
>
> var a = 42;\
> var b = a.toString();
>
> var c = "3.14";\
> var d = +c;
>
> b; // "42"\
> d; // 3.14
>
>  
>
> +c here is showing the unary operator form (operator with only one
> operand) of the + operator. Instead of performing mathematic addition
> (or string concatenation -- see below), the unary + explicitly coerces
> its operand (c) to a number value. The unary - operator also coerces
> like + does, but it also flips the sign of the number.
>
>  
>
> Another common usage of the unary + operator is to coerce
> a Date object into a number, because the result is the unix timestamp
> (milliseconds elapsed since 1 January 1970 00:00:00 UTC)
> representation of the date/time value:
>
> var d = new Date( "Mon, 18 Aug 2014 08:53:06 CDT" );
>
> +d; // 1408369986000
>
> The most common usage of this idiom is to get the current *now* moment
> as a timestamp, such as:
>
> var timestamp = +new Date();
>
>  
>
> But coercion is not the only way to get the timestamp out of
> a Date object. A noncoercion approach is perhaps even preferable, as
> it's even more explicit:
>
> var timestamp = new Date().getTime();\
> // var timestamp = (new Date()).getTime();\
> // var timestamp = (new Date).getTime();
>
> But an even more preferable noncoercion option is to use the ES5
> added Date.now() static function:
>
> var timestamp = Date.now();
>
>  
>
> ***Explicitly: Parsing Numeric Strings***
>
>  
>
> A similar outcome to coercing a string to a number can be achieved by
> parsing a number out of a string's character contents. There are,
> however, distinct differences between this parsing and the type
> conversion
>
>  
>
> var a = "42";\
> var b = "42px";
>
> Number( a ); // 42\
> parseInt( a ); // 42
>
> Number( b ); // NaN\
> parseInt( b ); // 42
>
>  
>
> Parsing a numeric value out of a string is tolerant of non-numeric
> characters -- it just stops parsing left-to-right when encountered --
> whereas coercion is not tolerant and fails resulting in the NaN value.
> Parsing should not be seen as a substitute for coercion. These two
> tasks, while similar, have different purposes. Parse a string as a
> number when you don't know/care what other non-numeric characters
> there may be on the right-hand side. Coerce a string (to a number)
> when the only acceptable values are numeric and something like "42px"
> should be rejected as a number.
>
>  
>
> If you pass a non-string, the value you pass will automatically be
> coerced to a string first (see "ToString" earlier), which would
> clearly be a kind of hidden implicit coercion. It's a really bad idea
> to rely upon such a behavior in your program, so never use
> parseInt(..) with a non-string value.
>
>  
>
> ***ToBoolean***
>
>  
>
> Just like with String(..) and Number(..) above, Boolean(..) (without
> the new, of course!) is an explicit way of forcing the ToBoolean
> coercion:
>
>  
>
> var a = "0";\
> var b = \[\];\
> var c = {};
>
> var d = "";\
> var e = 0;\
> var f = null;\
> var g;
>
> Boolean( a ); // true\
> Boolean( b ); // true\
> Boolean( c ); // true
>
> Boolean( d ); // false\
> Boolean( e ); // false\
> Boolean( f ); // false\
> Boolean( g ); // false
>
>  
>
> Just like the unary + operator coerces a value to a number (see
> above), the unary ! negate operator explicitly coerces a value to a
> boolean. The problem is that it also flips the value from truthy to
> falsy or vice versa. So, the most common way JS developers explicitly
> coerce to boolean is to use the !! double-negate operator, because the
> second ! will flip the parity back to the original:
>
>  
>
> ***Implicit Coercion***
>
>  
>
> Implicit coercion refers to type conversions that are hidden, with
> non-obvious side-effects that implicitly occur from other actions.
>
>  
>
> The + operator is overloaded to serve the purposes of both number
> addition and string concatenation.
>
>  
>
> var a = "42";\
> var b = "0";
>
> var c = 42;\
> var d = 0;
>
> a + b; // "420"\
> c + d; // 42
>
>  
>
> What's different that causes "420" vs 42? It's a common misconception
> that the difference is whether one or both of the operands is a
> string, as that means + will assume string concatenation. While that's
> partially true, it's more complicated than that.
>
>  
>
> But here's where coercing the boolean values to numbers (0 or 1,
> obviously) can greatly help:
>
> function onlyOne() {\
> var sum = 0;\
> for (var i=0; i &lt; arguments.length; i++) {\
> // skip falsy values. same as treating\
> // them as 0's, but avoids NaN's.\
> if (arguments\[i\]) {\
> sum += arguments\[i\];\
> }\
> }\
> return sum == 1;\
> }
>
> var a = true;\
> var b = false;
>
> onlyOne( b, a ); // true\
> onlyOne( b, a, b, b, b ); // true
>
> onlyOne( b, b ); // false\
> onlyOne( b, a, b, b, b, a ); // false
>
>  
>
>  
>
> ***Operators || and &&***
>
>  
>
> In fact, I would argue these operators shouldn't even be called
> "logical \_\_\_ operators", as that name is incomplete in describing
> what they do. If I were to give them a more accurate (if more clumsy)
> name, I'd call them "selector operators," or more completely, "operand
> selector operators." They result in the value of one (and only one) of
> their two operands. In other words, they select one of the two
> operand's values.
>
> var a = 42;\
> var b = "abc";\
> var c = null;
>
> a || b; // 42\
> a && b; // "abc"
>
> c || b; // "abc"\
> c && b; // null
>
>  
>
> In languages like C and PHP, those expressions result in true or
> false, but in JS (and Python and Ruby, for that matter!), the result
> comes from the values themselves.
>
>  
>
> Both || and && operators perform a boolean test on the first operand
> (a or c). If the operand is not already boolean (as it's not, here), a
> normal ToBoolean coercion occurs, so that the test can be performed.
>
>  
>
> For the || operator, if the test is true, the || expression results in
> the value of the first operand (a or c). If the test is false, the ||
> expression results in the value of the second operand (b).
>
>  
>
> Inversely, for the && operator, if the test is true, the && expression
> results in the value of the second operand (b). If the test is false,
> the && expression results in the value of the first operand (a or c).
>
>  
>
> The result of a || or && expression is always the underlying value of
> one of the operands, not the (possibly coerced) result of the test.
>
>  
>
> Another way of thinking about these operators:
>
> a || b;\
> // roughly equivalent to:\
> a ? a : b;
>
> a && b;\
> // roughly equivalent to:\
> a ? b : a;
>
>  
>
> ***Loose Equals vs. Strict Equals***
>
>  
>
> Loose equals is the == operator, and strict equals is the ===
> operator. Both operators are used for comparing two values for
> "equality," but the "loose" vs. "strict" indicates a very important
> difference in behavior between the two, specifically in how they
> decide "equality."
>
>  
>
> A very common misconception about these two operators is: "== checks
> values for equality and === checks both values and types for
> equality." While that sounds nice and reasonable, it's inaccurate.
> **The correct description is: "== allows coercion in the equality
> comparison and === disallows coercion."**
>
>  
>
> Don't fall into the trap, as many have, of thinking this has anything
> to do with performance, though, as if == is going to be slower than
> === in any relevant way. While it's measurable that coercion does take
> a little bit of processing time, it's mere microseconds (yes, that's
> millionths of a second!).
>
>  
>
> To illustrate == coercion, let's first build off
> the string and number examples earlier in this chapter:
>
> var a = 42;\
> var b = "42";
>
> a === b; // false\
> a == b; // true
>
>  
>
> As we'd expect, a === b fails, because no coercion is allowed, and
> indeed the 42 and "42" values are different. However, the second
> comparison a == b uses loose equality, which means that if the types
> happen to be different, the comparison algorithm will perform implicit
> coercion on one or both values. But exactly what kind of coercion
> happens here? Does the a value of 42 become a string, or does the b
> value of "42" become a number?
>
>  
>
> In the ES5 spec, clauses 11.9.3.4-5 say:
>
>  
>
> If Type(x) is Number and Type(y) is String, return the result of the
> comparison x == ToNumber(y).
>
> If Type(x) is String and Type(y) is Number, return the result of the
> comparison ToNumber(x) == y.
>
>  
>
> Consider:
>
> var a = "42";\
> var b = true;
>
> a == b; // false
>
>  
>
> clauses 11.9.3.6-7:

1.  If Type(x) is Boolean, return the result of the
    > comparison ToNumber(x) == y.

2.  If Type(y) is Boolean, return the result of the comparison x
    > == ToNumber(y).

>  
>
> the value "42" is neither == true nor == false. At first, that
> statement might seem crazy. How can a value be neither truthy nor
> falsy? But that's the problem! You're asking the wrong question,
> entirely. It's not your fault, really. Your brain is tricking you."42"
> is indeed truthy, but "42" == true is not performing a boolean
> test/coercion at all, no matter what your brain says. "42" is not
> being coerced to a boolean (true), but instead true is being coerced
> to a 1, and then "42" is being coerced to 42. Whether we like it or
> not, ToBoolean is not even involved here, so the truthiness or
> falsiness of "42" is irrelevant to the == operation!
>
>  
>
> Another example of implicit coercion can be seen with == loose
> equality between null and undefined values. Yet again quoting the ES5
> spec, clauses 11.9.3.2-3:

1.  If x is null and y is undefined, return true.

2.  If x is undefined and y is null, return true.

>  
>
>  
>
> var a = null;\
> var b;
>
> a == b; // true\
> a == null; // true\
> b == null; // true
>
> a == false; // false\
> b == false; // false\
> a == ""; // false\
> b == ""; // false\
> a == 0; // false\
> b == 0; // false
>
> The coercion between null and undefined is safe and predictable, and
> no other values can give false positives in such a check. I recommend
> using this coercion to allow null and undefined to be
> indistinguishable and thus treated as the same value.
>
>  
>
> If an object/function/array is compared to a simple scalar primitive
> (string, number, or boolean), the ES5 spec says in clauses 11.9.3.8-9:

1.  If Type(x) is either String or Number and Type(y) is Object, return
    > the result of the comparison x == ToPrimitive(y).

2.  If Type(x) is Object and Type(y) is either String or Number, return
    > the result of the comparison ToPrimitive(x) == y.

>  
>
> var a = 42;\
> var b = \[ 42 \];
>
> a == b; // true
>
>  
>
> var a = "abc";\
> var b = Object( a ); // same as \`new String( a )\`
>
> a === b; // false\
> a == b; // true
>
> a == b is true because b is coerced (aka "unboxed," unwrapped)
> via ToPrimitive to its underlying "abc" simple scalar primitive value,
> which is the same as the value in a.
>
>  
>
> ***Safely Using Implicit Coercion***
>
>  

1.  If either side of the comparison can have true or false values,
    > don't ever, EVER use ==.

2.  If either side of the comparison can have \[\], "", or 0 values,
    > seriously consider not using ==.

>  
>
> ![](media/image1.png){width="6.0in" height="4.84375in"}
>
>  
>
> ***Abstract Relational Comparison***
>
>  
>
> While this part of implicit coercion often gets a lot less attention,
> it's important nonetheless to think about what happens with a &lt; b
> comparisons (similar to how we just examined a == b in depth). The
> algorithm is only defined for a &lt; b. So, a &gt; b is handled as b
> &lt; a. The algorithm first calls ToPrimitive coercion on both values,
> and if the return result of either call is not a string, then both
> values are coerced to number values using the ToNumber operation
> rules, and compared numerically. However, if both values are strings
> for the &lt; comparison, simple lexicographic (natural alphabetic)
> comparison on the characters is performed:

 

 

YDKJS - 8

Wednesday, April 20, 2016

14:22

***Statement Completion Values***

 

It's a fairly little known fact that statements all have completion
values (even if that value is just undefined). How would you even go
about seeing the completion value of a statement?

The most obvious answer is to type the statement into your browser's
developer console, because when you execute it, the console by default
reports the completion value of the most recent statement it executed.

 

b = ( a++, a ); (Increment a and assign to b)

 

***else if And Optional Blocks***

 

It's a common misconception that JavaScript has an else if clause,
because you can do:

if (a) {\
// ..\
}\
else if (b) {\
// ..\
}\
else {\
// ..\
}

But there's a hidden characteristic of the JS grammar here: there is
no else if. But if and else statements are allowed to omit the {
} around their attached block if they only contain a single statement.
You've seen this many times before, undoubtedly:

if (a) doSomething( a );

Many JS style guides will insist that you always use { } around a single
statement block, like:

if (a) { doSomething( a ); }

However, the exact same grammar rule applies to the else clause, so
the else if form you've likely always coded isactually parsed as:

if (a) {\
// ..\
}\
else {\
if (b) {\
// ..\
}\
else {\
// ..\
}\
}

 

 

***try..finally***

You're probably familiar with how the try..catch block works. But have
you ever stopped to consider the finally clause that can be paired with
it? In fact, were you aware that try only requires
either catch or finally, though both can be present if needed.

The code in the finally clause always runs (no matter what), and it
always runs right after the try (and catch if present) finish, before
any other code runs. In one sense, you can kind of think of the code in
a finally clause as being in a callback function that will always be
called regardless of how the rest of the block behaves.

 

 

***switch***

switch (a) {\
case 2:\
// do something\
break;\
case 42:\
// do another thing\
break;\
default:\
// fallback to here\
}

As you can see, it evaluates a once, then matches the resulting value to
each case expression (just simple value expressions here). If a match is
found, execution will begin in that matched case, and will either go
until a break is encountered or until the end of the switch block is
found.

 

First, the matching that occurs between the a expression and
each case expression is identical to the === algorithm. However, you may
wish to allow coercive equality, and to do so you'll need to sort of
"hack" the switch statement a bit:

 

var a = "42";

switch (true) {\
case a == 10:\
console.log( "10 or '10'" );\
break;\
case a == 42:\
console.log( "42 or '42'" );\
break;\
default:\
// never gets here\
}\
// 42 or '42'

 

JavaScript operators all have well-defined rules for precedence (which
ones bind first before others) and associativity (how multiple operator
expressions are implicitly grouped).

ASI (Automatic Semicolon Insertion) is a parser-error-correction
mechanism built into the JS engine, which allows it under certain
circumstances to insert an assumed ; in places where it is required, was
omitted, and where insertion fixes the parser error.

 

JavaScript has several types of errors, but it's less known that it has
two classifications for errors: "early" (compiler thrown, uncatchable)
and "runtime" (try..catchable). All syntax errors are obviously early
errors that stop the program before it runs, but there are others, too.

 

 

 

 

 

 

Callback

Wednesday, April 20, 2016

15:16

One benefit of this function-as-object concept is that you can pass code
to another function in the same way you would pass a regular variable or
object

 

// define our function with the callback argument\
function some\_function(arg1, arg2, callback) {\
        // this generates a random number between\
        // arg1 and arg2\
        var my\_number = Math.ceil(Math.random() \*\
                (arg1 - arg2) + arg2);\
        // then we're done, so we'll call the callback and\
        // pass our result\
        callback(my\_number);\
}\
// call the function\
some\_function(5, 15, function(num) {\
        // this anonymous function will run when the\
        // callback is called\
        console.log("callback called! " + num);\
});

 

It might seem silly to go through all that trouble when the value could
just be returned normally, but there are situations where that’s
impractical and callbacks are necessary.

Traditionally functions work by taking input in the form of arguments
and returning a value using a return statement (ideally a single return
statement at the end of the function: one entry point and one exit
point). This makes sense. Functions are essentially mappings between
input and output.

 

Javascript gives us an option to do things a bit differently. Rather
than wait around for a function to finish by returning a value, we can
use callbacks to do it asynchronously. This is useful for things that
take a while to finish, like making an AJAX request, because we aren’t
holding up the browser. We can keep on doing other things while waiting
for the callback to be called. In fact, very often we are required (or,
rather, strongly encouraged) to do things asynchronously in Javascript.

 

function some\_function2(url, callback) {\
        var httpRequest; // create our XMLHttpRequest object\
        if (window.XMLHttpRequest) {\
                httpRequest = new XMLHttpRequest();\
        } else if (window.ActiveXObject) {\
                // Internet Explorer is stupid\
                httpRequest = new\
                        ActiveXObject("Microsoft.XMLHTTP");\
        }

httpRequest.onreadystatechange = function() {\
                // inline function to check the status\
                // of our request\
                // this is called on every state change\
                if (httpRequest.readyState === 4 &amp;&amp;\
                                httpRequest.status === 200) {\
                        callback.call(httpRequest.responseXML);\
                        // call the callback function\
                }\
        };\
        httpRequest.open('GET', url);\
        httpRequest.send();\
}\
// call the function\
some\_function2("text.xml", function() {\
        console.log(this);\
});\
console.log("this will run before the above callback");

 

 

We’re using two anonymous functions here. It’s important to remember
that we could just as easily be using named functions, but for sake of
brevity they’re just written inline. The first anonymous function is run
every time there’s a state change in our httpRequest object. We ignore
it until the state is 4 (meaning it’s done) and the status is 200
(meaning it was successful). In the real world you’d want to check if
the request failed, but we’re assuming the file exists and can be loaded
by the browser. This anonymous function is assigned to
httpRequest.onreadystatechange, so it is not run right away but rather
called every time there’s a state change in our request.

 

When we finally finish our AJAX request using call(). Alternatively you
could use apply() (the difference between the two is beyond the scope of
this tutorial, but it involves how you pass arguments to the function).

 

The neat thing about using call() is that we set the context in which
the function is executed. This means that when we use the this keyword
inside our callback function it refers to whatever we passed as the
first argument for call(). In this case, when we refer to this inside
our anonymous callback function we are referring to the responseXML from
the AJAX request.

 

Finally, the second console.log statement will run before the first,
because the callback isn’t executed until the request is over, and until
that happens the rest of the code goes right on ahead and keeps running.

 

 

 

***Browser Asynchronous APIs***

 

Luckily, Browsers provide a number of asynchronous APIs such as the
commonly used XHR (XMLHttpRequest or 'AJAX') APIs, as well as IndexedDB,
SQLite, HTML5 Web workers, and the HTML5 GeoLocation APIs to name a few.
Even some DOM related actions are exposed asynchronously, such CSS3
animation via the transitionEnd events.

 

The way browsers expose asynchronous programming to the application
logic is via events or callbacks. In event-based asynchronous APIs,
developers register an event handler for a given object (e.g. HTML
Element or other DOM objects) and then call the action. The browser will
perform the action usually in a different thread, and trigger the event
in the main thread when appropriate.

 

Other browser APIs, such as SQLite and HTML5 Geolocation, are callback
based, meaning that the developer passes a function as argument that
will get called back by the underlying implementation with the
corresponding resolution.

 

***Making Applications Asynchronous-Ready***

 

*// WRONG: this will make the UI freeze when getting the data*\
var data = getData();\
alert("We got data: " + data);

 

 

This API design requires the getData() to be blocking, which will freeze
the user interface until the data is fetched. If the data is local in
the JavaScript context then this might not be an issue, however if the
data needs to be fetched from the network or even locally in a SQLite or
index store this could have dramatic impact on the user experience.

The right design is to proactively make all application API that could
take some time to process, asynchronous from the beginning as
retrofitting synchronous application code to be asynchronous can be a
daunting task.

For example the simplistic getData() API would become something like:

getData(function(data){\
alert("We got data: " + data);\
});

 

 

***Handling Failures***

 

One catch of asynchronous programing is that the traditional try/catch
way to handle failures does not really work anymore, as errors usually
happen in another thread. Consequently, the callee needs to have a
structured way to notify the caller when something goes wrong during the
processing.

 

In an event-based asynchronous API this is often accomplished by the
application code querying the event or object when receiving the event.
For callback based asynchronous APIs, the best practice is to have a
second argument that takes a function that would be called in case of a
failure with the appropriate error information as argument.

 

*// getData(successFunc,failFunc);*\
getData(function(data){\
alert("We got data: " + data);\
}, function(ex){\
alert("oops, some problem occured: " + ex);\
});

 

 

Luckily, there is a relatively old pattern, called Promises (kind of
similar to Future in Java) and a robust and modern implementation in
jQuery core called \$.Deferred that provides a simple and powerful
solution to asynchronous programing.'

 

To make it simple, the Promises pattern defines that the asynchronous
API returns a Promise object which is kind of a “Promise that the result
will be resolved with the corresponding data.” To get the resolution,
the caller gets the Promise object and calls a done(successFunc(data))
which will tell the Promise object to call this successFunc when the
“data” is resolved.

 

*// get the promise object for this API*\
var dataPromise = getData();

*// register a function to get called when the data is resolved*\
dataPromise.done(function(data){\
alert("We got data: " + data);\
});

*// register the failure function*\
dataPromise.fail(function(ex){\
alert("oops, some problem occured: " + ex);\
});

*// Note: we can have as many dataPromise.done(...) as we want.*\
dataPromise.done(function(data){\
alert("We asked it twice, we get it twice: " + data);\
});

 

 

Here, we get the dataPromise object first and then call the .done method
to register a function we want to get called back when the data gets
resolved. We can also call the .fail method to handle the eventual
failure. Note that we can have as many .done or .fail calls as we need
since the underlying Promise implementation (jQuery code) will handle
the registration and callbacks.

 

With this pattern, it is relatively easy to implement more advanced
synchronization code, and jQuery already provides the most common one
such a \$.when.

 

*// assuming both getData and getLocation return their respective
Promise*\
var combinedPromise = \$.when(getData(), getLocation())

*// function will be called when both getData and getLocation resolve*\
combinePromise.done(function(data,location){\
alert("We got data: " + dataResult + " and location: " + location);\
});

 

And the beauty of it all is that jQuery.Deferred makes it very easy for
developers to implement the asynchronous function. For example, the
getData could look something like this:

 

 

function getData(){\
*// 1) create the jQuery Deferred object that will be used*\
var deferred = \$.Deferred();\
\
*// ---- AJAX Call ---- //*\
XMLHttpRequest xhr = new XMLHttpRequest();\
xhr.open("GET","data",true);\
\
*// register the event handler*\
xhr.addEventListener('load',function(){\
if(xhr.status === 200){\
*// 3.1) RESOLVE the DEFERRED (this will trigger all the done()...)*\
deferred.resolve(xhr.response);\
}else{\
*// 3.2) REJECT the DEFERRED (this will trigger all the fail()...)*\
deferred.reject("HTTP error: " + xhr.status);\
}\
},false)\
\
*// perform the work*\
xhr.send();\
*// Note: could and should have used jQuery.ajax.*\
*// Note: jQuery.ajax return Promise, but it is always a good idea to
wrap it*\
*// with application semantic in another Deferred/Promise*\
*// ---- /AJAX Call ---- //*\
\
*// 2) return the promise of this deferred*\
return deferred.promise();\
}

 

 

So, when the getData() is called, it first creates a new jQuery.Deferred
object (1) and then returns its Promise (2) so that the caller can
register its done and fail functions. Then, when the XHR call returns,
it either resolves the deferred (3.1) or reject it (3.2). Doing the
deferred.resolve will trigger all the done(...) functions and other
promise functions (e.g., then and pipe) and calling deferred.reject will
call all the fail() functions.

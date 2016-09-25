 

Thursday, January 29, 2015

18:08

 

Assembly language is a small abstraction of the underlying machine. Many
so-called “imperative” languages that followed (such as FORTRAN, BASIC,
and C) were abstractions of assembly language. These languages are big
improvements over assembly language, but their primary abstraction still
requires you to think in terms of the structure of the computer rather
than the structure of the problem you are trying to solve. The
programmer must establish the association between the machine model (in
the “solution space,” which is the place where you’re implementing that
solution, such as a computer) and the model of the problem that is
actually being solved. The alternative to modeling the machine is to
model the problem you’re trying to solve. Early languages such as LISP
and APL chose particular views of the world. The object-oriented
approach goes a step further by providing tools for the programmer to
represent elements in the problem space. We refer to the elements in the
problem space and their representations in the solution space as
“objects

 

These characteristics represent a pure approach to object-oriented
programming

**Everything is an object.** Think of an object as a fancy variable; it
stores data, but you can “make requests” to that object, asking it to
perform operations on itself.

**A program is a bunch of objects telling each other what to do by
sending messages**

**Each object has its own memory made up of other objects**. Put another
way, you create a new kind of object by making a package containing
existing objects. Thus, you can build complexity into a program while
hiding it behind the simplicity of objects

**Every object has a type**. Using the parlance, each object is an
instance of a class, in which “class” is synonymous with “type

**All objects of a particular type can receive the same messages**

 

**An object has state, behavior and identity.**

 

Objects that are identical except for their state during a program’s
execution are grouped together into “classes of objects,” **and that’s
where the keyword class came from.** Creating abstract data types
(classes) is a fundamental concept in object-oriented programming. The
members (elements) of each class share some commonality: At the same
time, each member has its own state.

 

a class describes a set of objects that have identical characteristics
(data elements) and behaviors (functionality), a class is really a data
type because a floating point number, for example, also has a set of
characteristics and behaviors. The difference is that a programmer
defines a class to fit a problem rather than being forced to use an
existing data type that was designed to represent a unit of storage in a
machine. You extend the programming language by adding new data types
specific to your needs. Once a class is established, you can make as
many objects of that class as you like, and then manipulate those
objects as if they are the elements that exist in the problem you are
trying to solve.

 

There needs to be a way to make a request of the object so that it will
do something, such as complete a transaction, draw something on the
screen, or turn on a switch. And each object can satisfy only certain
requests. The requests you can make of an object are defined by its
interface, and the type is what determines the interface. The interface
determines the requests that you can make for a particular object.
However, there must be code somewhere to satisfy that request. This,
along with the hidden data, comprises the implementation.

 

The goal of the class creator is to build a class that exposes only
what’s necessary to the client programmer and keeps everything else
hidden. Why? Because if it’s hidden, the client programmer can’t access
it, which means that the class creator can change the hidden portion at
will without worrying about the impact on anyone else. The hidden
portion usually represents the tender insides of an object that could
easily be corrupted by a careless or uninformed client programmer, so
hiding the implementation reduces program bugs. So the first reason for
access control is to keep client programmers’ hands off portions they
shouldn’t touch. The second reason for access control is to allow the
library designer to change the internal workings of the class without
worrying about how it will affect the client programmer. Java uses three
explicit keywords to set the boundaries in a class: **public**,
**private**, and **protected.** Java also has a “**default**” access,
which comes into play if you don’t use one of the aforementioned
specifiers.

 

The simplest way to reuse a class is to just use an object of that class
directly, but you can also place an object of that class inside a new
class. Because you are composing a new class from existing classes, this
concept is called **composition.** Composition is often referred to as a
“has-a” relationship, as in “A car has an engine. Composition comes with
a great deal of flexibility. The member objects of your new class are
typically private, making them inaccessible to the client programmers
who are using the class. This allows you to change those members without
disturbing existing client code. You can also change the member objects
at run time, to dynamically change the behavior of your program

 

It seems a pity, however, to go to all the trouble to create a class and
then be forced to create a brand new one that might have similar
functionality. It’s nicer if we can take the existing class, clone it,
and then make additions and modifications to the clone. This is
effectively what you get with inheritance, with the exception that if
the original class (called the base class or superclass or parent class)
is changed, the modified “clone” (called the derived class or inherited
class or subclass or child class) also reflects those changes.
Inheritance, does not have this flexibility since the compiler must
place compile-time restrictions on classes created with inheritance

 

![](media/image1.png){width="3.7604166666666665in"
height="3.1145833333333335in"}

When you inherit from an existing type, you create a new type. This new
type contains not only all the members of the existing type (although
the private ones are hidden away and inaccessible), but more importantly
it duplicates the interface of the base class. That is, all the messages
you can send to objects of the base class you can also send to objects
of the derived class. Since we know the type of a class by the messages
we can send to it, this means that the derived class is the same type as
the base class. In the previous example, “A circle is a shape.”

 

You have two ways to differentiate your new derived class from the
original base class. The first is quite straightforward: You simply add
brand new methods to the derived class. These new methods are not part
of the base-class interface. This means that the base class simply
didn’t do as much as you wanted it to, so you added more methods. The
second and more important way to differentiate your new class is to
change the behavior of an existing base-class method. This is referred
to as **overriding** that method. As a result, you can exactly
substitute an object of the derived class for an object of the base
class. This can be thought of as **pure substitution**, and it’s often
referred to as the substitution principle.

 

When dealing with type hierarchies, you often want to treat an object
not as the specific type that it is, but instead as its base type. This
allows you to write code that doesn’t depend on specific types. In the
shape example, methods manipulate generic shapes, unconcerned about
whether they’re circles, squares, triangles, or some shape that hasn’t
even been defined yet. All shapes can be drawn, erased, and moved, so
these methods simply send a message to a shape object. Such code is
unaffected by the addition of new types, and adding new types is the
most common way to extend an object-oriented program to handle new
situations. If a method is going to tell a generic shape to draw itself,
or a generic vehicle to steer, or a generic bird to move, the compiler
cannot know at compile time precisely what piece of code will be
executed.

 

![](media/image2.png){width="4.6875in" height="2.28125in"}

 

The compiler cannot make a function call in the traditional sense. The
function call generated by a non-OOP compiler causes what is called
**early binding**. It means the compiler generates a call to a specific
function name, and the runtime system resolves this call to the absolute
address of the code to be executed. To solve the problem,
object-oriented languages use the concept of **late binding**. When you
send a message to an object, the code being called isn’t determined
until run time. The compiler does ensure that the method exists and
performs type checking on the arguments and return value, but it doesn’t
know the exact code to execute. To perform late binding, Java uses a
special bit of code in lieu of the absolute call. This code calculates
the address of the method body, using information stored in the object.
Thus, each object can behave differently according to the contents of
that special bit of code. When you send a message to an object, the
object actually does figure out what to do with that message.

 

void doSomething(Shape shape) {

shape.erase();

// ...

shape.draw();

}

 

 

Circle circle = new Circle();

Triangle triangle = new Triangle();

Line line= new Line();

doSomething(circle);

doSomething(triangle);

doSomething(line);

 

We call this process of treating a derived type as though it were its
base type **upcasting**. The name cast is used in the sense of casting
into a mold and the up comes from the way the inheritance diagram is
typically arranged, with the base type at the top and the derived
classes fanning out downward.

 

In Java and the name of this ultimate base class is simply **Object**.
It turns out that the benefits of the singly rooted hierarchy are many.
All objects in a singly rooted hierarchy have an interface in common, so
they are all ultimately the same fundamental type. All objects in a
singly rooted hierarchy can be guaranteed to have certain functionality.
You know you can perform certain basic operations on every object in
your system. All objects can easily be created on the heap, and argument
passing is greatly simplified. A singly rooted hierarchy makes it much
easier to implement a **garbage collector**, which is one of the
fundamental improvements of Java over C++. And since information about
the type of an object is guaranteed to be in all objects, you’ll never
end up with an object whose type you cannot determine.

 

In general, you don’t know how many objects you’re going to need to
solve a particular problem, or how long they will last. You also don’t
know how to store those objects. The solution to most problems in
object-oriented design seems flippant: You create another type of
object. The new type of object that solves this particular problem holds
references to other objects. Of course, you can do the same thing with
an array, which is available in most languages. But this new object,
generally called a **container** will expand itself whenever necessary
to accommodate everything you place inside it. So you don’t need to know
how many objects you’re going to hold in a container. Fortunately, a
good OOP language comes with a set of containers as part of the package

 

From a design standpoint, all you really want is a container that can be
manipulated to solve your problem. If a single type of container
satisfied all of your needs, there’d be no reason to have different
kinds. There are two reasons that you need a choice of containers.
First, containers provide different types of interfaces and external
behavior. A stack has a different interface and behavior than a queue,
which is different from a set or a list. One of these might provide a
more flexible solution to your problem than the other. Second, different
containers have different efficiencies for certain operations. For
example, there are two basic types of List: ArrayList and LinkedList.
Both are simple sequences that can have identical interfaces and
external behaviors. But certain operations can have significantly
different costs. Randomly accessing elements in an ArrayList is a
constant-time operation; it takes the same amount of time regardless of
the element you select. However, in a LinkedList it is expensive to move
through the list to randomly select an element, and it takes longer to
find an element that is farther down the list. On the other hand, if you
want to insert an element in the middle of a sequence, it’s cheaper in a
LinkedList than in an ArrayList

 

Before Java SE5, containers held the one universal type in Java: Object.
The singly rooted hierarchy means that everything is an Object, so a
container that holds Objects can hold anything.6 This made containers
easy to reuse. To use such a container, you simply add object references
to it and later ask for them back. But, since the container held only
Objects, when you added an object reference into the container it was
upcast to Object, thus losing its character. When fetching it back, you
got an Object reference, and not a reference to the type that you put
in. Here, the cast is used again, but this time you’re not casting up
the inheritance hierarchy to a more general type. Instead, you cast down
the hierarchy to a more specific type. This manner of casting is called
downcasting. Downcasting and the runtime checks require extra time for
the running program and extra effort from the programmer. Wouldn’t it
make sense to somehow create the container so that it knows the types
that it holds, eliminating the need for the downcast and a possible
mistake? The solution is called a **parameterized type mechanism**. One
of the big changes in Java SE5 is the addition of parameterized types,
called **generics** in Java.

 

ArrayList&lt;Shape&gt; shapes = new ArrayList&lt;Shape&gt;();

 

One critical issue when working with objects is the way they are created
and destroyed. Each object requires resources, most notably memory, in
order to exist. When an object is no longer needed it must be cleaned up
so that these resources are released for reuse. How can you possibly
know when to destroy the objects? When you’re done with the object, some
other part of the system might not be.

 

For maximum runtime speed, the storage and lifetime can be determined
while the program is being written, by placing the objects on the stack
(these are sometimes called automatic or scoped variables) or in the
static storage area. This places a priority on the speed of storage
allocation and release, and this control can be very valuable in some
situations. However, you sacrifice flexibility because you must know the
exact quantity, lifetime, and type of objects while you’re writing the
program.

 

The second approach is to create objects dynamically in a pool of memory
called the heap. In this approach, you don’t know until run time how
many objects you need, what their lifetime is, or what their exact type
is. Those are determined at the spur of the moment while the program is
running. If you need a new object, you simply make it on the heap at the
point that you need it. Because the storage is managed dynamically, at
run time, the amount of time required to allocate storage on the heap
can be noticeably longer than the time to create storage on the stack.
Creating storage on the stack is often a single assembly instruction to
move the stack pointer down and another to move it back up. The time to
create heap storage depends on the design of the storage mechanism. Java
uses dynamic memory allocation, exclusively.7 Every time you want to
create an object, you use the new operator to build a dynamic instance
of that object.

 

With languages that allow objects to be created on the stack, the
compiler determines how long the object lasts and can automatically
destroy it. However, if you create it on the heap the compiler has no
knowledge of its lifetime. In a language like C++, you must determine
programmatically when to destroy the object, which can lead to memory
leaks if you don’t do it correctly. Java provides a feature called a
garbage collector that automatically discovers when an object is no
longer in use and destroys it. A garbage collector is much more
convenient because it reduces the number of issues that you must track
and the code you must write. With Java, the garbage collector is
designed to take care of the problem of releasing the memory (although
this doesn’t include other aspects of cleaning up an object). The
garbage collector “knows” when an object is no longer in use, and it
then automatically releases the memory for that object. This, combined
with the fact that all objects are inherited from the single root class
Object and that you can create objects only one way—on the heap—makes
the process of programming in Java much simpler than programming in C++.

 

Ever since the beginning of programming languages, error handling has
been a particularly difficult issue. major problem with most
error-handling schemes is that they rely on programmer vigilance in
following an agreed-upon convention that is not enforced by the
language. If the programmer is not vigilant—often the case if they are
in a hurry—these schemes can easily be forgotten. An exception is an
object that is “thrown” from the site of the error and can be “caught”
by an appropriate exception handler designed to handle that particular
type of error. It’s as if exception handling is a different, parallel
path of execution that can be taken when things go wrong. And because it
uses a separate execution path, it doesn’t need to interfere with your
normally executing code. This tends to make that code simpler to write
because you aren’t constantly forced to check for errors. In addition, a
thrown exception is unlike an error value that’s returned from a method
or a flag that’s set by a method in order to indicate an error
condition—these can be ignored. An exception cannot be ignored, so it’s
guaranteed to be dealt with at some point. Finally, exceptions provide a
way to reliably recover from a bad situation. Instead of just exiting
the program, you are often able to set things right and restore
execution, which produces much more robust programs. Java’s exception
handling stands out among programming languages, because in Java,
exception handling was wired in from the beginning and you’re forced to
use it. It is the single acceptable way to report errors. If you don’t
write your code to properly handle exceptions, you’ll get a compile-time
error message. This guaranteed consistency can sometimes make error
handling much easier.

 

Friday, January 30, 2015

17:44

 

Java. You treat everything as an object, using a single consistent
syntax. Although you treat everything as an object, the identifier you
manipulate is actually a “reference” to an object. That is, just because
you have a reference doesn’t mean there’s necessarily an object
connected to it. When you create a reference, you want to connect it
with a new object. You do so, in general, with the new operator.

 

**Registers**. This is the fastest storage because it exists in a place
different from that of other storage: inside the processor. However, the
number of registers is severely limited, so registers are allocated as
they are needed

 

**The stack**. This lives in the general random-access memory (RAM)
area, but has direct support from the processor via its stack pointer.
The stack pointer is moved down to create new memory and moved up to
release that memory. This is an extremely fast and efficient way to
allocate storage, second only to registers. The Java system must know,
while it is creating the program, the exact lifetime of all the items
that are stored on the stack. This constraint places limits on the
flexibility of your programs, so while some Java storage exists on the
stack—in particular, object references—Java objects themselves are not
placed on the stack.

 

**The heap**. This is a general-purpose pool of memory (also in the RAM
area) where all Java objects live. The nice thing about the heap is
that, unlike the stack, the compiler doesn’t need to know how long that
storage must stay on the heap. Thus, there’s a great deal of flexibility
in using storage on the heap. Whenever you need an object, you simply
write the code to create it by using new, and the storage is allocated
on the heap when that code is executed.

 

**Constant storage**. Constant values are often placed directly in the
program code, which is safe since they can never change. Sometimes
constants are cordoned off by themselves so that they can be optionally
placed in read-only memory (ROM), in embedded systems.

 

**Non-RAM storage**. If data lives completely outside a program, it can
exist while the program is not running, outside the control of the
program. The two primary examples of this are streamed objects, in which
objects are turned into streams of bytes, generally to be sent to
another machine, and persistent objects, in which the objects are placed
on disk so they will hold their state even when the program is
terminated.

 

One group of types, which you’ll use quite often in your programming,
gets special treatment. You can think of these as “**primitive**” types.
The reason for the special treatment is that to create an object with
new—especially a small, simple variable—isn’t very efficient, because
new places objects on the heap. For these types Java falls back on the
approach taken by C and C++. That is, instead of creating the variable
by using new, an “automatic” variable is created that is not a
reference. The variable holds the value directly, and it’s placed on the
stack, so it’s much more efficient. Java determines the size of each
primitive type. These sizes don’t change from one machine architecture
to another.

The “wrapper” classes for the primitive data types allow you to make a
non-primitive object on the heap to represent that primitive type. For
example:

char c = ‘x’;

Character ch = new Character(c);

Java SE5 autoboxing will automatically convert from a primitive to a
wrapper type

 

One of the primary goals of Java is safety, so many of the problems that
plague programmers in C and C++ are not repeated in Java. A Java array
is guaranteed to be initialized and cannot be accessed outside of its
range. The range checking comes at the price of having a small amount of
memory overhead on each array as well as verifying the index at run
time, but the assumption is that the safety and increased productivity
are worth the expense. When you create an array of objects, you are
really creating an array of references, and each of those references is
automatically initialized to a special value with its own keyword: null.
When Java sees null, it recognizes that the reference in question isn’t
pointing to an object.

 

Most procedural languages have the concept of scope. This determines
both the visibility and lifetime of the names defined within that scope.
In C, C++, and Java, scope is determined by the placement of curly
braces {}

 

You cannot do the following, even though it is legal in C and C++:

{

int x = 12;

{

int x = 96; // Illegal

}

}

 

Java objects do not have the same lifetimes as primitives. When you
create a Java object using new, it hangs around past the end of the
scope. Thus if you use:

{

String s = new String("a string");

} // End of scope

the reference s vanishes at the end of the scope. However, the String
object that s was pointing to is still occupying memory. In this bit of
code, there is no way to access the object after the end of the scope,
because the only reference to it is out of scope. It turns out that
because objects created with new stay around for as long as you want
them, a whole slew of C++ programming problems simply vanish in Java. In
C++ you must not only make sure that the objects stay around for as long
as you need them, you must also destroy the objects when you’re done
with them. That brings up an interesting question. If Java leaves the
objects lying around, what keeps them from filling up memory and halting
your program? This is exactly the kind of problem that would occur in
C++. This is where a bit of magic happens. Java has a garbage collector,
which looks at all the objects that were created with new and figures
out which ones are not being referenced anymore. Then it releases the
memory for those objects, so the memory can be used for new objects.

 

What establishes the type of an object? You might expect there to be a
keyword called “type,” and that certainly would have made sense.
Historically, however, most objectoriented languages have used the
keyword class to mean “I’m about to tell you what a new type of object
looks like

 

class ATypeName { /\* Class body goes here \*/ }

However, you can create an object of this type using new:

ATypeName a = new ATypeName();

 

Each object keeps its own storage for its fields; ordinary fields are
not shared among objects. When a primitive data type is a member of a
class, it is guaranteed to get a default value if you do not initialize
it: This guarantee doesn’t apply to local variables—those that are not
fields of a class. Thus, if within a method definition you have:

int x;

Then x will get some arbitrary value

 

 

Methods in Java determine the messages an object can receive. The
fundamental parts of a method are the name, the arguments, the return
type, and the body. Here is the basic form:

ReturnType methodName( /\* Argument list \*/ ) {

/\* Method body \*/

}

 

Methods in Java can be created only as part of a class. The method
argument list specifies what information you pass into the method. As
you might guess, this information—like everything else in Java—takes the
form of objects. So, what you must specify in the argument list are the
types of the objects to pass in and the name to use for each one. As in
any situation in Java where you seem to be handing objects around, you
are actually passing references

 

**The static keyword**

Ordinarily, when you create a class you are describing how objects of
that class look and how they will behave. You don’t actually get an
object until you create one using new, and at that point storage is
allocated and methods become available. There are two situations in
which this approach is not sufficient. One is if you want to have only a
single piece of storage for a particular field, regardless of how many
objects of that class are created, or even if no objects are created.
The other is if you need a method that isn’t associated with any
particular object of this class. That is, you need a method that you can
call even if no objects are created. You can achieve both of these
effects with the static keyword. since static methods don’t need any
objects to be created before they are used, they cannot directly access
non-static members or methods by simply calling those other members
without referring to a named object (since non-static members and
methods must be tied to a particular object).

 

System class has several fields, and if you select out, you’ll discover
that it’s a static PrintStream object. Since it’s static, you don’t need
to create anything with new. The out object is always there, and you can
just use it. What you can do with this out object is determined by its
type:

 

The name of the class is the same as the name of the file. When you’re
creating a standalone program such as this one, one of the classes in
the file must have the same name as the file. (The compiler complains if
you don’t do this.). The public keyword means that the method is
available to the outside world (described in detail in the Access
Control chapter). The argument to main( ) is an array of String objects.
The args won’t be used in this program, but the Java compiler insists
that they be there because they hold the arguments from the command
line.

 

Wednesday, July 08, 2015

19:15

 

**Short-circuiting**

When dealing with logical operators, you run into a phenomenon called
“short-circuiting.” This means that the expression will be evaluated
only until the truth or falsehood of the entire expression can be
unambiguously determined. As a result, the latter parts of a logical
expression might not be evaluated.

 

 

**Casting operators**

The word cast is used in the sense of “casting into a mold.” Java will
automatically change one type of data into another when appropriate. For
instance, if you assign an integral value to a floating point variable,
the compiler will automatically convert the int to a float

 

In Java, casting is safe, with the exception that when you perform a
so-called narrowing conversion (that is, when you go from a data type
that can hold more information to one that doesn’t hold as much), you
run the risk of losing information. Here the compiler forces you to use
a cast, in effect saying, “This can be a dangerous thing to do—if you
want me to do it anyway you must make the cast explicit.” With a
widening conversion an explicit cast is not needed, because the new type
will more than hold the information from the old type so that no
information is ever lost. Java allows you to cast any primitive type to
any other primitive type, except for boolean, which doesn’t allow any
casting at all.

 

Wednesday, July 08, 2015

19:18

 

Earlier in this chapter I stated that the **comma** operator (not the
comma separator, which is used to separate definitions and method
arguments) has only one use in Java: in the control expression of a for
loop

 

You can also control the flow of the loop inside the body of any of the
iteration statements by using break and continue. break quits the loop
without executing the rest of the statements in the loop. continue stops
the execution of the current iteration and goes back to the beginning of
the loop to begin the next iteration

 

Wednesday, July 08, 2015

19:20

 

Two of these safety issues are initialization and cleanup. Many C bugs
occur when the programmer forgets to initialize a variable.

The name of the constructor is the same as the name of the class. It
makes sense that such a method will be called automatically during
initialization.

Note that the coding style of making the first letter of all methods
lowercase does not apply to constructors, since the name of the
constructor must match the name of the class exactly. A constructor that
takes no arguments is called the default constructor.

 

The constructor is an unusual type of method because it has no return
value. This is distinctly different from a void return value, in which
the method returns nothing but you still have the option to make it
return something else. Constructors return nothing and you don’t have an
option (the new expression does return a reference to the newly created
object, but the constructor itself has no return value). If there were a
return value, and if you could select your own, the compiler would
somehow need to know what to do with that return value

 

Thus, method overloading is essential to allow the same method name to
be used with different argument types. And although method overloading
is a must for constructors, it’s a general convenience and can be used
with any method. If the methods have the same name, how can Java know
which method you mean? There’s a simple rule: Each overloaded method
must take a unique list of argument types. Even differences in the
ordering of arguments are sufficient to distinguish two methods,
although you don’t normally want to take this approach because it
produces difficult-to-maintain code: A primitive can be automatically
promoted from a smaller type to a larger one, and this can be slightly
confusing in combination with overloading

 

It is common to wonder, “Why only class names and method argument lists?
Why not distinguish between methods based on their return values?” For
example, these two methods, which have the same name and arguments, are
easily distinguished from each other:

void f() {}

int f() { return 1; }

This might work fine as long as the compiler could unequivocally
determine the meaning from the context, as in int x = f( ). However, you
can also call a method and ignore the return value. This is often
referred to as calling a method for its side effect, since you don’t
care about the return value, but instead want the other effects of the
method call. So if you call the method this way:

f();

how can Java determine which f( ) should be called? And how could
someone reading the code see it?

 

If you create a class that has no constructors, the compiler will
automatically create a default constructor for you.

 

**This**

 

If you have two objects of the same type called a and b, you might
wonder how it is that you can call a method peel( ) for both those
objects. If there’s only one method called peel( ), how can that method
know whether it’s being called for the object a or b?

 

 

 

 

 

 

 

Monday, July 13, 2015

15:28

 

Constructors return nothing and you don’t have an option (the new
expression does return a reference to the newly created object, but the
constructor itself has no return value). If there were a return value,
and if you could select your own, the compiler would somehow need to
know what to do with that return value.

 

It is common to wonder, “Why only class names and method argument lists?
Why not distinguish between methods based on their return values?” For
example, these two methods, which have the same name and arguments, are
easily distinguished from each other:

void f() {}

int f() { return 1; }

This might work fine as long as the compiler could unequivocally
determine the meaning from the context, as in int x = f( ). However, you
can also call a method and ignore the return value. This is often
referred to as calling a method for its side effect, since you don’t
care about the return value, but instead want the other effects of the
method call.

 

To allow you to write the code in a convenient object-oriented syntax in
which you “send a message to an object,” the compiler does some
undercover work for you. There’s a secret first argument passed to the
method peel( ), and that argument is the reference to the object that’s
being manipulated. So the two method calls become something like:

Banana.peel(a, 1);

Banana.peel(b, 2);

This is internal and you can’t write these expressions and get the
compiler to accept them, but it gives you an idea of what’s happening.
Suppose you’re inside a method and you’d like to get the reference to
the current object. Since that reference is passed secretly by the
compiler, there’s no identifier for it. However, for this purpose
there’s a keyword: this. The this keyword—which can be used only inside
a non-static method—produces the reference to the object that the method
has been called for. You can treat the reference just like any other
object reference. Keep in mind that if you’re calling a method of your
class from within another method of your class, you don’t need to use
this. You simply call the method

 

When you write several constructors for a class, there are times when
you’d like to **call one constructor from another** to avoid duplicating
code. You can make such a call by using the this keyword. In a
constructor, the this keyword takes on a different meaning when you give
it an argument list. It makes an explicit call to the constructor that
matches that argument list. Thus you have a straightforward way to call
other constructors:

**this(petals);**

//! this(s); // Can’t call two!

while you can call one constructor using this, you cannot call two. In
addition, the constructor call must be the first thing you do, or you’ll
get a compiler error message.

 

**Static** means that there is no this for that particular method. You
cannot call non-static methods from inside static methods2 (although the
reverse is possible), and you can call a static method for the class
itself, without any object. In fact, that’s primarily what a static
method is for. It’s as if you’re creating the equivalent of a global
method. However, global methods are not permitted in Java, and putting
the static method inside a class allows it access to other static
methods and to static fields.

 

You might observe that the heap isn’t in fact a conveyor belt, and if
you treat it that way, you’ll start paging memory—moving it on and off
disk, so that you can appear to have more memory than you actually do.
Paging significantly impacts performance. Eventually, after you create
enough objects, you’ll run out of memory. The trick is that the garbage
collector steps in, and while it collects the garbage it compacts all
the objects in the heap so that you’ve effectively moved the “heap
pointer” closer to the beginning of the conveyor belt and farther away
from a page fault. The garbage collector rearranges things and makes it
possible for the high-speed, infinite-free-heap model to be used while
allocating storage.

 

A simple but slow garbage-collection technique is called reference
counting. This means that each object contains a reference counter, and
every time a reference is attached to that object, the reference count
is increased. Every time a reference goes out of scope or is set to
null, the reference count is decreased. Thus, managing reference counts
is a small but constant overhead that happens throughout the lifetime of
your program. The garbage collector moves through the entire list of
objects, and when it finds one with a reference count of zero it
releases that storage (however, reference counting schemes often release
an object as soon as the count goes to zero). The one drawback is that
if objects circularly refer to each other they can have nonzero
reference counts while still being garbage.

 

In faster schemes, garbage collection is not based on reference
counting. Instead, it is based on the idea that any non-dead object must
ultimately be traceable back to a reference that lives either on the
stack or in static storage. The chain might go through several layers of
objects. Thus, if you start in the stack and in the static storage area
and walk through all the references, you’ll find all the live objects.
For each reference that you find, you must trace into the object that it
points to and then follow all the references in that object, tracing
into the objects they point to, etc., until you’ve moved through the
entire Web that originated with the reference on the stack or in static
storage. Each object that you move through must still be alive.

 

the JVM uses an adaptive garbage-collection scheme, and what it does
with the live objects that it locates depends on the variant currently
being used. One of these variants is stop-and-copy. This means that—for
reasons that will become apparent—the program is first stopped (this is
not a background collection scheme). Then, each live object is copied
from one heap to another, leaving behind all the garbage. In addition,
as the objects are copied into the new heap, they are packed end-to-end,
thus compacting the new heap. Of course, when an object is moved from
one place to another, all references that point at the object must be
changed. The reference that goes from the heap or the static storage
area to the object can be changed right away, but there can be other
references pointing to this object that will be encountered later during
the “walk.” These are fixed up as they are found (you could imagine a
table that maps old addresses to new ones

 

There are two issues that make these so-called “copy collectors”
inefficient. The first is the idea that you have two heaps and you slosh
all the memory back and forth between these two separate heaps,
maintaining twice as much memory as you actually need. Some JVMs deal
with this by allocating the heap in chunks as needed and simply copying
from one chunk to another. The second issue is the copying process
itself. Once your program becomes stable, it might be generating little
or no garbage. Despite that, a copy collector will still copy all the
memory from one place to another, which is wasteful

 

To prevent this, some JVMs detect that no new garbage is being generated
and switch to a different scheme (this is the “adaptive” part). This
other scheme is called mark-and-sweep. Mark-and-sweep follows the same
logic of starting from the stack and static storage, and tracing through
all the references to find live objects. However, each time it finds a
live object, that object is marked by setting a flag in it, but the
object isn’t collected yet. Only when the marking process is finished
does the sweep occur. During the sweep, the dead objects are released.
However, no copying happens, so if the collector chooses to compact a
fragmented heap, it does so by shuffling objects around

 

> ***Member initialization***

 

Java goes out of its way to guarantee that variables are properly
initialized before they are used. In the case of a method’s local
variables, this guarantee comes in the form of a compile-time error. If
a primitive is a field in a class, however, things are a bit different.
Each primitive field of a class is guaranteed to get an initial value.

 

The constructor can be used to perform initialization, and this gives
you greater flexibility in your programming because you can call methods
and perform actions at run time to determine the initial values. There’s
one thing to keep in mind, however: You aren’t precluding the automatic
initialization, which happens before the constructor is entered.

public class Counter {

int i;

Counter() { i = 7; }

// ...

} ///:\~

then i will first be initialized to 0, then to 7. This is true with all
the primitive types and with object references, including those that are
given explicit initialization at the point of definition. For this
reason, the compiler doesn’t try to force you to initialize elements in
the constructor at any particular place, or before they are
used—initialization is already guaranteed.

 

Within a class, the order of initialization is determined by the order
that the variables are defined within the class. The variable
definitions may be scattered throughout and in between method
definitions, but the variables are initialized before any methods can be
called—even the constructor

 

***static data initialization***

 

There’s only a single piece of storage for a static, regardless of how
many objects are created. You can’t apply the static keyword to local
variables, so it only applies to fields. If a field is a static
primitive and you don’t initialize it, it gets the standard initial
value for its type. If it’s a reference to an object, the default
initialization value is null. static initialization occurs only if it’s
necessary. They are initialized only when the first class object is
created (or the first static access occurs). After that, the static
objects are not reinitialized. The order of initialization is statics
first, if they haven’t already been initialized by a previous object
creation, and then the non-static objects

 

1.  Even though it doesn’t explicitly use the static keyword, the
    > constructor is actually a static method. So the first time an
    > object of type Dog is created, or the first time a static method
    > or static field of class Dog is accessed, the Java interpreter
    > must locate Dog.class, which it does by searching through
    > the classpath.

2.  As Dog.class is loaded (creating a Class object, which you’ll learn
    > about later), all of its static initializers are run. Thus, static
    > initialization takes place only once, as the Class object is
    > loaded for the first time.

3.  When you create a new Dog( ), the construction process for a Dog
    > object first allocates enough storage for a Dog object on
    > the heap.

4.  This storage is wiped to zero, automatically setting all the
    > primitives in that Dog object to their default values (zero for
    > numbers and the equivalent for boolean and char) and the
    > references to null.

5.  Any initializations that occur at the point of field definition
    > are executed.

6.  Constructors are executed. As you shall see in the Reusing Classes
    > chapter, this might actually involve a fair amount of activity,
    > especially when inheritance is involved.

 

Java allows you to group other static initializations inside a special
“static clause” (sometimes called a static block) in a class. This code,
like other static initializations, is executed only once: the first time
you make an object of that class or the first time you access a static
member of that class (even if you never make an object of that class).

 

Java provides a similar syntax, called instance initialization, for
initializing non-static variables for each object.

 

An array is simply a sequence of either objects or primitives that are
all the same type and are packaged together under one identifier name.
Arrays are defined and used with the square-brackets indexing operator
\[ \]

int\[\] a1;

You can also put the square brackets after the identifier to produce
exactly the same meaning:

int a1\[\];

The compiler doesn’t allow you to tell it how big the array is. This
brings us back to that issue of “references.” All that you have at this
point is a reference to an array (you’ve allocated enough storage for
that reference), and there’s been no space allocated for the array
object itself. To create storage for the array, you must write an
initialization expression. For arrays, initialization can appear
anywhere in your code, but you can also use a special kind of
initialization expression that must occur at the point where the array
is created. This special initialization is a set of values surrounded by
curly braces. The storage allocation (the equivalent of using new) is
taken care of by the compiler in this case

 

The second form provides a convenient syntax to create and call methods
that can produce an effect similar to C’s variable argument lists (known
as “varargs” in C). These can include unknown quantities of arguments as
well as unknown types. Since all classes are ultimately inherited from
the common root class Object (a subject you will learn more about as
this book progresses), you can create a method that takes an array of
Object. With varargs, you no longer have to explicitly write out the
array syntax—the compiler will actually fill it in for you when you
specify varargs

static void printArray(Object... args) {

for(Object obj : args)

it’s possible to pass zero arguments to a vararg list.

 

***ENUM***

 

An apparently small addition in Java SE5 is the enum keyword, which
makes your life much easier when you need to group together and use a
set of enumerated types

public enum Spiciness {

NOT, MILD, MEDIUM, HOT, FLAMING

} ///:\~

 

This creates an enumerated type called Spiciness with five named values.
Because the instances of enumerated types are constants, they are in all
capital letters by convention (if there are multiple words in a name,
they are separated by underscores).

To use an enum, you create a reference of that type and assign it to an
instance:

 

Spiciness howHot = Spiciness.MEDIUM;

System.out.println(howHot);

 

The compiler automatically adds useful features when you create an enum.
For example, it creates a toString( ) so that you can easily display the
name of an enum instance, which is how the print statement above
produced its output. The compiler also creates an ordinal( ) method to
indicate the declaration order of a particular enum constant, and a
static values( ) method that produces an array of values of the enum
constants in the order that they were declared:

 

An especially nice feature is the way that enums can be used inside
switch statements

 

Thursday, July 30, 2015

10:50

 

A package contains a group of classes, organized together under a single
namespace.

When you create a source-code file for Java, it’s commonly called a
compilation unit (sometimes a translation unit). Each compilation unit
must have a name ending in .java, and inside the compilation unit there
can be a public class that must have the same name as the file
(including capitalization, but excluding the .java file name extension).
There can be only one public class in each compilation unit; otherwise,
the compiler will complain. If there are additional classes in that
compilation unit, they are hidden from the world outside that package
because they’re not public, and they comprise “support” classes for the
main public class

 

When you compile a .java file, you get an output file for each class in
the .java file. Each output file has the name of a class in the .java
file, but with an extension of .class. Thus you can end up with quite a
few .class files from a small number of .java files. A working program
is a bunch of .class files, which can be packaged and compressed into a
Java ARchive (JAR) file (using Java’s jar archiver). The Java
interpreter is responsible for finding, loading, and interpreting2 these
files. A library is a group of these class files. Each source file
usually has a public class and any number of non-public classes, so
there’s one public component for each source file. If you want to say
that all these components (each in its own separate .java and .class
files) belong together, that’s where the package keyword comes in.

 

package access;

you’re stating that this compilation unit is part of a library named
access. Put another way, you’re saying that the public class name within
this compilation unit is under the umbrella of the name access, and
anyone who wants to use that name must either fully specify the name or
use the import keyword in combination with access, using the choices
given previously

 

Part of this trick is resolving the package name into a directory on
your machine, so that when the Java program runs and it needs to load
the .class file, it can locate the directory where the .class file
resides. The Java interpreter proceeds as follows. First, it finds the
environment variable CLASSPATH3 (set via the operating system, and
sometimes by the installation program that installs Java or a Java-based
tool on your machine). CLASSPATH contains one or more directories that
are used as roots in a search for .class files. Starting at that root,
the interpreter will take the package name and replace each dot with a
slash to generate a path name off of the CLASSPATH root (so package
foo.bar.baz becomes foo\\bar\\baz or foo/bar/baz or possibly something
else, depending on your operating system). This is then concatenated to
the various entries in the CLASSPATH. That’s where it looks for the
.class file with the name corresponding to the class you’re trying to
create. (It also searches some standard directories relative to where
the Java interpreter resides.). There’s a variation when using JAR
files, however. You must put the actual name of the JAR file in the
classpath, not just the path where it’s located.

 

When the compiler encounters the import statement for the simple
library, it begins searching at the directories specified by CLASSPATH,
looking for subdirectory net/mindview/simple, then seeking the compiled
files of the appropriate names (Vector.class for Vector, and List.class
for List). Note that both the classes and the desired methods in Vector
and List must be public.

 

A very common use is for debugging code. The debugging features are
enabled during development and disabled in the shipping product. You can
accomplish this by changing the package that’s imported in order to
change the code used in your program from the debug version to the
production version.

 

It’s worth remembering that anytime you create a package, you implicitly
specify a directory structure when you give the package a name. The
package must live in the directory indicated by its name, which must be
a directory that is searchable starting from the CLASSPATH.
Experimenting with the package keyword can be a bit frustrating at
first, because unless you adhere to the package-name to directory-path
rule, you’ll get a lot of mysterious runtime messages about not being
able to find a particular class, even if that class is sitting there in
the same directory. If you get a message like this, try commenting out
the package statement, and if it runs, you’ll know where the problem
lies.

 

The Java access specifiers **public, protected, and private** are placed
in front of each definition for each member in your class, whether it’s
a field or a method. Each access specifier only controls the access for
that particular definition.

If you don’t provide an access specifier, it means “package access

 

**package access** (and sometimes “friendly”). It means that all the
other classes in the current package have access to that member, but to
all the classes outside of this package, the member appears to be
private. Since a compilation unit—a file—can belong only to a single
package, all the classes within a single compilation unit are
automatically available to each other via package access.

 

Access control is often referred to as implementation hiding. Wrapping
data and methods within classes in combination with implementation
hiding is often called encapsulation.5 The result is a data type with
characteristics and behaviors

 

1.  There can be only one public class per compilation unit (file).

2.  The name of the public class must exactly match the name of the file
    > containing the compilation unit, including capitalization

3.  It is possible, though not typical, to have a compilation unit with
    > no public class at all. In this case, you can name the file
    > whatever you like

 

Friday, July 31, 2015

15:35

 

you simply create objects of your existing class inside the new class.
This is called composition, because the new class is composed of objects
of existing classes. The second approach is more subtle. It creates a
new class as a type of an existing class. You literally take the form of
the existing class and add code to it without modifying the existing
class. This technique is called inheritance

 

It turns out that you’re always doing inheritance when you create a
class, because unless you explicitly inherit from some other class, you
implicitly inherit from Java’s standard root class Object. But
inheritance doesn’t just copy the interface of the base class. When you
create an object of the derived class, it contains within it a subobject
of the base class. This subobject is the same as if you had created an
object of the base class by itself. It’s just that from the outside, the
subobject of the base class is wrapped within the derived-class object.
Of course, it’s essential that the base-class subobject be initialized
correctly, and there’s only one way to guarantee this: Perform the
initialization in the constructor by calling the base-class constructor,
which has all the appropriate knowledge and privileges to perform the
base-class initialization. Java automatically inserts calls to the
base-class constructor in the derived-class constructor. If your class
doesn’t have default arguments, or if you want to call a base-class
constructor that has an argument, you must explicitly write the calls to
the base-class constructor using the super keyword and the appropriate
argument list:

 

A third relationship, which is not directly supported by Java, is called
delegation. This is midway between inheritance and composition, because
you place a member object in the class you’re building (like
composition), but at the same time you expose all the methods from the
member object in your new class (like inheritance).

 

If a Java base class has a method name that’s overloaded several times,
redefining that method name in the derived class will not hide any of
the base-class versions (unlike C++). Thus overloading works regardless
of whether the method was defined at this level or in a base class

 

Java SE5 has added the **@Override** annotation, which is not a keyword
but can be used as if it were. When you mean to override a method, you
can choose to add this annotation and the compiler will produce an error
message if you accidentally overload instead of overriding

 

Composition is generally used when you want the features of an existing
class inside your new class, but not its interface. That is, you embed
an object so that you can use it to implement features in your new
class, but the user of your new class sees the interface you’ve defined
for the new class rather than the interface from the embedded object.
For this effect, you embed private objects of existing classes inside
your new class. When you inherit, you take an existing class and make a
special version of it. In general, this means that you’re taking a
general-purpose class and specializing it for a particular need. With a
little thought, you’ll see that it would make no sense to compose a car
using a vehicle object—a car doesn’t contain a vehicle, it is a vehicle.
The is-a relationship is expressed with inheritance, and the has-a
relationship is expressed with composition.

 

Casting from a derived type to a base type moves up on the inheritance
diagram, so it’s commonly referred to as **upcasting**. Upcasting is
always safe because you’re going from a more specific type to a more
general type. That is, the derived class is a superset of the base
class. It might contain more methods than the base class, but it must
contain at least the methods in the base class. The only thing that can
occur to the class interface during the upcast is that it can lose
methods, not gain them. This is why the compiler allows upcasting
without any explicit casts or other special notation.

 

**final data**: Many programming languages have a way to tell the
compiler that a piece of data is “constant.” A field that is both static
and final has only one piece of storage that cannot be changed. When
final is used with object references rather than primitives, the meaning
can be confusing. With a primitive, final makes the value a constant,
but with an object reference, final makes the reference a constant. Once
the reference is initialized to an object, it can never be changed to
point to another object. However, the object itself can be modified.
This restriction includes arrays, which are also objects.

Java allows the creation of blank finals, which are fields that are
declared as final but are not given an initialization value. In all
cases, the blank final must be initialized before it is used, and the
compiler ensures this. However, blank finals provide much more
flexibility in the use of the final keyword since, for example, a final
field inside a class can now be different for each object, and yet it
retains its immutable quality

 

**final arguments**: Java allows you to make arguments final by
declaring them as such in the argument list. This means that inside the
method you cannot change what the argument reference points to:

 

**final methods**: There are two reasons for final methods. The first is
to put a “lock” on the method to prevent any inheriting class from
changing its meaning. The second reason for final methods is efficiency.
In earlier implementations of Java, if you made a method final, you
allowed the compiler to turn any calls to that method into inline calls.
In more recent version of Java, the virtual machine (in particular, the
hotspot technologies) can detect these situations and optimize away the
extra indirection, so its no longer necessary-in fact, it is now
generally discouraged-to use final to try to help the optimizer

 

Any **private methods** in a class are implicitly final. Because you
can’t access a private method, you can’t override it. You can add the
final specifier to a private method, but it doesn’t give that method any
extra meaning. This issue can cause confusion, because if you try to
override a private method (which is implicitly final), it seems to work,
and the compiler doesn’t give an error message. “Overriding” can only
occur if something is part of the base-class interface. That is, you
must be able to upcast an object to its base type and call the same
method (the point of this will become clear in the next chapter). If a
method is private, it isn’t part of the base-class interface. It is just
some code that’s hidden away inside the class, and it just happens to
have that name, but if you create a public, protected, or package-access
method with the same name in the derived class, there’s no connection to
the method that might happen to have that name in the base class. You
haven’t overridden the method; you’ve just created a new method. Since a
private method is unreachable and effectively invisible, it doesn’t
factor into anything except for the code organization of the class for
which it was defined

 

**final classes:** When you say that an entire class is final (by
preceding its definition with the final keyword), you state that you
don’t want to inherit from this class or allow anyone else to do so.

 

Friday, July 31, 2015

15:48

 

Connecting a method call to a method body is called binding. When
binding is performed before the program is run (by the compiler and
linker, if there is one), it’s called **early binding**. The solution is
called late binding, which means that the binding occurs at run time,
based on the type of object. **Late binding** is also called dynamic
binding or runtime binding. When a language implements late binding,
there must be some mechanism to determine the type of the object at run
time and to call the appropriate method. That is, the compiler still
doesn’t know the object type, but the method-call mechanism finds out
and calls the correct method body. All method binding in Java uses late
binding unless the method is static or final (private methods are
implicitly final.

 

Why would you declare a method final? As noted in the last chapter, it
prevents anyone from overriding that method. Perhaps more important, it
effectively “turns off” dynamic binding, or rather it tells the compiler
that dynamic binding isn’t necessary. This allows the compiler to
generate slightly more efficient code for final method calls.

 

However, only ordinary method calls can be polymorphic. For example, if
you access a field directly, that access will be resolved at compile
time,

 

When a Sub object is upcast to a Super reference, any field accesses are
resolved by the compiler, and are thus not polymorphic. In this example,
different storage is allocated for Super.field and Sub.field. Thus, Sub
actually contains two fields called field: its own and the one that it
gets from Super. However, the Super version is not the default that is
produced when you refer to field in Sub; in order to get the Super field
you must explicitly say super.field.

 

As usual, constructors are different from other kinds of methods. This
is also true when polymorphism is involved. **Even though constructors
are not polymorphic** (they’re actually static methods, but the static
declaration is implicit), it’s important to understand the way
constructors work in complex hierarchies and with polymorphism

 

The order of the constructor calls is important. When you inherit, you
know all about the base class and can access any public and protected
members of the base class. This means that you must be able to assume
that all the members of the base class are valid when you’re in the
derived class.

 

If you call a dynamically-bound method inside a constructor, the
overridden definition for that method is used. However, the effect of
this call can be rather unexpected because the overridden method will be
called before the object is fully constructed. This can conceal some
difficult-to-find bugs.

 

As a result, a good guideline for constructors is, “Do as little as
possible to set the object into a good state, and if you can possibly
avoid it, don’t call any other methods in this class.” The only safe
methods to call inside a constructor are those that are final in the
base class. (This also applies to private methods, which are
automatically final.) These cannot be overridden and thus cannot produce
this kind of surprise.

 

Java SE5 adds **covariant return types**, which means that an overridden
method in a derived class can return a type derived from the type
returned by the base-class method.

 

Since you lose the specific type information via an upcast (moving up
the inheritance hierarchy), it makes sense that to retrieve the type
information—that is, to move back down the inheritance hierarchy—you use
a downcast. However, you know an upcast is always safe because the base
class cannot have a bigger interface than the derived class. Therefore,
every message you send through the base class interface is guaranteed to
be accepted. But with a downcast, you don’t really know that a shape
(for example) is actually a circle. It could instead be a triangle or
square or some other type. To solve this problem, there must be some way
to guarantee that a downcast is correct, so that you won’t accidentally
cast to the wrong type and then send a message that the object can’t
accept. This would be quite unsafe. in Java, every cast is checked. at
run time this cast is checked to ensure that it is in fact the type you
think it is. If it isn’t, you get a ClassCastException. This act of
checking types at run time is called **runtime type identification
(RTTI)**.

 

Friday, July 31, 2015

17:12

 

> Interfaces and abstract classes provide more structured way to
> separate interface from implementation.
>
>  
>
> It establishes a basic form, so that you can say what’s common for all
> the derived classes. Another way of saying this is to call Instrument
> an abstract base class, or simply an **abstract class.** If you have
> an abstract class like Instrument, objects of that specific class
> almost always have no meaning. You create an abstract class when you
> want to manipulate a set of classes through its common interface. Java
> provides a mechanism for doing this called the abstract method.1 This
> is a method that is incomplete; it has only a declaration and no
> method body. A class containing abstract methods is called an abstract
> class. If a class contains one or more abstract methods, the class
> itself must be qualified as abstract. (Otherwise, the compiler gives
> you an error message.)
>
>  
>
> what is the compiler supposed to do when someone tries to make an
> object of that class? It cannot safely create an object of an abstract
> class, so you get an error message from the compiler. This way, the
> compiler ensures the purity of the abstract class, and you don’t need
> to worry about misusing it. If you inherit from an abstract class and
> you want to make objects of the new type, you must provide method
> definitions for all the abstract methods in the base class. If you
> don’t (and you may choose not to), then the derived class is also
> abstract, and the compiler will force you to qualify that class with
> the abstract keyword.
>
>  
>
> It’s possible to make a class abstract without including any abstract
> methods. This is useful when you’ve got a class in which it doesn’t
> make sense to have any abstract methods, and yet you want to prevent
> any instances of that class
>
>  
>
> The interface keyword produces a completely abstract class, one that
> provides no implementation at all. It allows the creator to determine
> method names, argument lists, and return types, but no method bodies.
> An interface provides only a form, but no implementation. An interface
> says, "All classes that implement this particular interface will look
> like this." Thus, any code that uses a particular interface knows what
> methods might be called for that interface, and that’s all
>
>  
>
> To create an interface, use the interface keyword instead of the class
> keyword. As with a class, you can add the public keyword before the
> interface keyword (but only if that interface is defined in a file of
> the same name). If you leave off the public keyword, you get package
> access, so the interface is only usable within the same package. **An
> interface can also contain fields, but these are implicitly static and
> final.** is because interfaces don't contain any state
> information/have a state associated with them. 
>
>  
>
> You can choose to explicitly declare the methods in an interface as
> public, but they are public even if you don’t say it. So when you
> implement an interface, the methods from the interface must be defined
> as public. Otherwise, they would default to package access, and you’d
> be reducing the accessibility of a method during inheritance, which is
> not allowed by the Java compiler.
>
>  

1.  Why can't interfaces contain static methods?

> There is no technical reason why an interface couldn't support static
> methods. This is [summed up nicely by the
> poster](http://stackoverflow.com/questions/129267/why-no-static-methods-in-interfaces-but-static-fields-and-inner-classes-ok/135722#135722) of
> the question you duplicated. One of the comments I made there
> emphasizes this point. In the end, I think this was just a choice by
> the language designers. This might actually be considered as a [small
> language change](http://blogs.oracle.com/darcy/entry/project_coin).
> \[Update: An [official
> proposal](http://docs.google.com/Doc?docid=dfkwr6vq_30dtg2z9d8&hl=en) was
> made to add static methods to interfaces in Java 7,\] and was
> initially slated for inclusion, but was later [dropped due to
> unforeseen
> complications.](http://bugs.sun.com/view_bug.do?bug_id=4093687)
>
> *Update:* In fact, in Java 8, *interfaces can have static methods,* 
>
>  

1.  Why can't static methods be overridden?

> Static methods are resolvable at compile time. Dynamic dispatch makes
> sense for instance methods, where the compiler can't determine the the
> concrete type of the object, and, thus, can't resolve the method to
> invoke. But invoking a static method requires a class, and since that
> class is known at compile time, dynamic dispatch is unnecessary
>
>  
>
> Whenever a method works with a class instead of an interface, you are
> limited to using that class or its subclasses. If you would like to
> apply the method to a class that isn’t in that hierarchy, you’re out
> of luck. An interface relaxes this constraint considerably. As a
> result, it allows you to write more reusable code
>
>  
>
> Because an interface has no implementation at all—that is, there is no
> storage associated with an interface—there’s nothing to prevent many
> interfaces from being combined. This is valuable because there are
> times when you need to say, "An x is an a and a b and a c. You place
> all the interface names after the implements keyword and separate them
> with commas. You can have as many interfaces as you want. You can
> upcast to each interface, because each interface is an independent
> type.
>
>  
>
> one of the core reasons for interfaces is shown in the preceding
> example: to upcast to more than one base type. You can easily add new
> method declarations to an interface by using inheritance, and you can
> also combine several interfaces into a new interface with inheritance.
> In both cases you get a new interface
>
>  
>
> Because any fields you put into an interface are automatically static
> and final, the interface is a convenient tool for creating groups of
> constant values. With Java SE5, you now have the much more powerful
> and flexible enum keyword, so it rarely makes sense to use interfaces
> for constants anymore
>
>  
>
> Fields defined in interfaces cannot be "blank finals," but they can be
> initialized with non-constant expressions. Since the fields are
> static, they are initialized when the class is first loaded, which
> happens when any of the fields are accessed for the first time
>
>  
>
>  
>
>

 

Friday, July 31, 2015

17:26

It’s possible to place a class definition within another class
definition. This is called an inner class. The inner class is a valuable
feature because it allows you to group classes that logically belong
together and to control the visibility of one within the other. If you
want to make an object of the inner class anywhere except from within a
non-static method of the outer class, you must specify the type of that
object as OuterClassName.InnerClassName. In inner class, an object of
that inner class has a link to the enclosing object that made it, and so
it can access the members of that enclosing object—without any special
qualifications. In addition, inner classes have access rights to all the
elements in the enclosing class. The inner class secretly captures a
reference to the particular object of the enclosing class that was
responsible for creating it. Then, when you refer to a member of the
enclosing class, that reference is used to select that member.
Construction of the inner-class object requires the reference to the
object of the enclosing class, and the compiler will complain if it
cannot access that reference.

 

If you need to produce the reference to the outer-class object, you name
the outer class followed by a dot and this. The resulting reference is
automatically the correct type, which is known and checked at compile
time, so there is no runtime overhead. Sometimes you want to tell some
other object to create an object of one of its inner classes. To do this
you must provide a reference to the other outer-class object in the new
expression, using the .new syntax,

 

public class Inner {

public DotThis outer() {

return DotThis.this;

// A plain "this" would be Inner’s "this"

}

}

 

DotNew dn = new DotNew();

DotNew.Inner dni = dn.new Inner();

 

To create an object of the inner class directly, you don’t follow the
same form and refer to the outer class name DotNew as you might expect,
but instead you must use an object of the outer class to make an object
of the inner class,

 

**It’s not possible** to create an object of the inner class unless you
already have an object of the outer class. This is because the object of
the inner class is quietly connected to the object of the outer class
that it was made from. However, **if you make a nested class (a static
inner class**), then it doesn’t need a reference to the outer-class
object

 

The contents( ) method combines the creation of the return value with
the definition of the class that represents that return value! In
addition, the class is **anonymous**; it has no name. If you’re defining
an anonymous inner class and want to use an object that’s defined
outside the anonymous inner class, the compiler requires that the
argument reference be final,

 

 

**Nested classes**

If you don’t need a connection between the inner-class object and the
outerclass object, then you can make the inner class static. This is
commonly called a nested class.2 To understand the meaning of static
when applied to inner classes, you must remember that the object of an
ordinary inner class implicitly keeps a reference to the object of the
enclosing class that created it. This is not true, however, when you say
an inner class is static. A nested class means:

1.You don’t need an outer-class object in order to create an object of a
nested class.

2.You can’t access a non-static outer-class object from an object of a
nested class.

 

Nested classes are different from ordinary inner classes in another way,
as well. Fields and methods in ordinary inner classes can only be at the
outer level of a class, so ordinary inner classes cannot have static
data, static fields, or nested classes. However, nested classes can have
all of these:

 

**Classes inside interfaces**

Normally, you can’t put any code inside an interface, but a nested class
can be part of an interface. Any class you put inside an interface is
automatically public and static. Since the class is static, it doesn’t
violate the rules for interfaces—the nested class is only placed inside
the namespace of the interface.

It doesn’t matter how deeply an inner class may be nested—it can
transparently access all of the members of all the classes it is nested
within,

 

**Closures & callbacks**

A closure is a callable object that retains information from the scope
in which it was created. From this definition, you can see that an inner
class is an object-oriented closure, because it doesn’t just contain
each piece of information from the outer-class object ("the scope in
which it was created"), but it automatically holds a reference back to
the whole outer-class object, where it has permission to manipulate all
the members, even private ones.

 

One of the most compelling arguments made to include some kind of
pointer mechanism in Java was to allow callbacks. With a callback, some
other object is given a piece of information that allows it to call back
into the originating object at some later point

 

**Can inner classes be overridden?**

What happens when you create an inner class, then inherit from the
enclosing class and redefine the inner class? That is, is it possible to
"override" the entire inner class? This seems like it would be a
powerful concept, but "overriding" an inner class as if it were another
method of the outer class doesn’t really do anything: there isn’t any
extra inner-class magic going on when you inherit from the outer class.
The two inner classes are completely separate entities, each in its own
namespace.

 

**Local inner classes**

As noted earlier, inner classes can also be created inside code blocks,
typically inside the body of a method. A local inner class cannot have
an access specifier because it isn’t part of the outer class, but it
does have access to the final variables in the current code block and
all the members of the enclosing class.

 

Since every class produces a .class file that holds all the information
about how to create objects of this type (this information produces a
"meta-class" called the Class object), you might guess that inner
classes must also produce .class files to contain the information for
their Class objects. The names of these files/classes have a strict
formula: **the name of the enclosing class, followed by a ‘\$’, followed
by the name of the inner class.** If inner classes are anonymous, the
compiler simply starts generating numbers as inner-class identifiers. If
inner classes are nested within inner classes, their names are simply
appended after a ‘\$’ and the outer-class identifier

 

Wednesday, August 05, 2015

11:00

 

The java.util library has a reasonably complete set of container classes
to solve this problem, the basic types of which are List, Set, Queue,
and Map. These types of objects are also known as **collection**
classes. Among their other characteristics—Set, for example, holds only
one object of each value, and Map is an associative array that lets you
associate objects with other objects—the Java container classes will
automatically resize themselves.

 

**Generics and type-safe containers**

One of the problems of using pre-Java SE5 containers was that the
compiler allowed you to insert an incorrect type into a container. For
example, consider a container of Apple objects, using the basic
workhorse container, ArrayList. ArrayList also has a method size( ) to
let you know how many elements have been added, so that you don’t
inadvertently index off the end and cause an error. In this example,
Apples and Oranges are placed into the container, then pulled out.
Normally, the Java compiler will give you a warning because the example
does not use generics. The classes Apple and Orange are distinct; they
have nothing in common except that they are both Objects. Since
ArrayList holds Objects, you can not only add Apple objects into this
container using the ArrayList method add( ), but you can also add Orange
objects without complaint at either compile time or run time. When you
go to fetch out what you think are Apple objects using the ArrayList
method get( ), you get back a reference to an Object that you must cast
to an Apple. At run time, when you try to cast the Orange object to an
Apple, you’ll get an error in the form of the aforementioned exception.

 

Applying predefined generic classes is usually straightforward. For
example, to define an ArrayList intended to hold Apple objects, you say
ArrayList&lt;Apple&gt; instead of just ArrayList. The angle brackets
surround the type parameters (there may be more than one), which specify
the type(s) that can be held by that instance of the container. **With
generics, you’re prevented, at compile time**, from putting the wrong
type of object into a container. Also notice that the cast is no longer
necessary when fetching items back out from the List. Since the List
knows what type it holds, it does the cast for you when you call get().

 

You are not limited to putting the exact type of object into a container
when you specify that type as a generic parameter. Upcasting works the
same with generics as it does with other types. Thus, you can add a
subtype of Apple to a container that is specified to hold Apple objects

 

**Collection**: a sequence of individual elements with one or more rules
applied to them. A List must hold the elements in the way that they were
inserted, a Set cannot have duplicate elements, and a Queue produces the
elements in the order determined by a queuing discipline

 

**Map**: a group of key-value object pairs, allowing you to look up a
value using a key. An ArrayList allows you to look up an object using a
number, so in a sense it associates numbers to objects. A map allows you
to look up an object using another object. It’s also called an
associative array, because it associates objects with other objects, or
a dictionary, because you look up a value object using a key object just
like you look up a definition using a word.: a group of key-value object
pairs, allowing you to look up a value using a key. An ArrayList allows
you to look up an object using a number, so in a sense it associates
numbers to objects. A map allows you to look up an object using another
object. It’s also called an associative array, because it associates
objects with other objects, or a dictionary, because you look up a value
object using a key object just like you look up a definition using a
word.

 

It’s also possible to use the output of Arrays.asList( ) directly, as a
List, but the underlying representation in this case is the array, which
cannot be resized. If you try to add( ) or delete( ) elements in such a
list, that would attempt to change the size of an array, so you’ll get
an "Unsupported Operation" error at run time.

 

A limitation of Arrays.asList( ) is that it takes a best guess about the
resulting type of the List, and doesn’t pay attention to what you’re
assigning it to. it’s possible to insert a "hint" in the middle of
Arrays.asList( ), to tell the compiler what the actual target type
should be for the resulting List type produced by Arrays.asList( ).
(Page 303)

 

**ArrayList and LinkedList** are both types of List, and you can see
from the output that they both hold elements in the same order in which
they are inserted. The difference between the two is not only
performance for certain types of operations, but also that a LinkedList
contains more operations than an ArrayList

 

**Why not sorted list **

Because all lists are already sorted by its order.

You can "resort" them with another ordering
using java.util.Collections.sort().

EDIT:

Lists as data structures are based in what is interesting is the
ordering in which the items where inserted.

Sets do not have that information.

If you want to order by addition time, use List. If you want to order by
other criteria, use SortedSet

 

From
&lt;<http://stackoverflow.com/questions/8725387/why-is-there-no-sortedlist-in-java>&gt;

 

 

 

**HashSet, TreeSet and LinkedHashSet** are types of Set. The output
shows that a Set will only hold one of each identical item, but it also
shows that the different Set implementations store the elements
differently. If storage order is important, you can use a TreeSet, which
keeps the objects in ascending comparison order, or a LinkedHashSet,
which keeps the objects in the order in which they were added

 

A **Map** (also called an associative array) allows you to look up an
object using a key, like a simple database. The associated object is
called a value

 

***List***

Lists promise to maintain elements in a particular sequence. The List
interface adds a number of methods to Collection that allow insertion
and removal of elements in the middle of a List.

 

•The basic ArrayList, which excels at randomly accessing elements, but
is slower when inserting and removing elements in the middle of a List.

•The LinkedList, which provides optimal sequential access, with
inexpensive insertions and deletions from the middle of the List. A
LinkedList is relatively slow for random access, but it has a larger
feature set than the ArrayList

 

The subList( ) method allows you to easily create a slice out of a
larger list, and this naturally produces a true result when passed to
containsAll( ) for that larger list. It’s also interesting to note that
order is unimportant—you can see in output lines 11 and 12 that calling
the intuitively named Collections.sort( ) and Collections.shuffle( ) on
sub doesn’t affect the outcome of containsAll( ). subList( ) produces a
list backed by the original list. Therefore, changes in the returned
list are reflected in the original list, and vice versa

 

***Iterator***

 

The concept of an Iterator (another design pattern) can be used to
achieve this abstraction. An iterator is an object whose job is to move
through a sequence and select each object in that sequence without the
client programmer knowing or caring about the underlying structure of
that sequence. In addition, an iterator is usually what’s called a
lightweight object: one that’s cheap to create

 

1.Ask a Collection to hand you an Iterator using a method called
iterator( ). That Iterator will be ready to return the first element in
the sequence.

2.Get the next object in the sequence with next( ).

3.See if there are any more objects in the sequence with hasNext( ).

4.Remove the last element returned by the iterator with remove( ).

 

**ListIterator**

The ListIterator is a more powerful subtype of Iterator that is produced
only by List classes. While Iterator can only move forward, ListIterator
is bidirectional. It can also produce the indexes of the next and
previous elements relative to where the iterator is pointing in the
list, and it can replace the last element that it visited using the set(
) method. You can produce a ListIterator that points to the beginning of
the List by calling listIterator( ), and you can also create a
ListIterator that starts out pointing to an index n in the list by
calling listIterator(n).

 

***LinkedList***

The LinkedList also implements the basic List interface like ArrayList
does, but it performs certain operations (insertion and removal in the
middle of the List) more efficiently than does ArrayList. Conversely, it
is less efficient for random-access operations. LinkedList also adds
methods that allow it to be used as a stack, a Queue or a double-ended
queue (deque).

getFirst( ) and element( ) are identical—they return the head (first
element) of the list without removing it, and throw
NoSuchElementException if the List is empty. peek( ) is a slight
variation of those two that returns null if the list is empty

 

***Stack***

A stack is sometimes referred to as a "last-in, first-out" (LIFO)
container. It’s sometimes called a pushdown stack, because whatever you
"push" on the stack last is the first item you can "pop" off of the
stack.

 

***Set***

A Set refuses to hold more than one instance of each object value. If
you try to add more than one instance of an equivalent object, the Set
prevents duplication. Set has the same interface as Collection, so there
isn’t any extra functionality like there is in the two different types
of List. Instead, the Set is exactly a Collection—it just has different
behavior. A Set determines membership based on the "value" of an object.
**HashSet** uses hashing for speed. The order maintained by a HashSet is
different from a TreeSet or a LinkedHashSet, since each implementation
has a different way of storing elements. TreeSet keeps elements sorted
into a red-black tree data structure, whereas HashSet uses the hashing
function. LinkedHashSet also uses hashing for lookup speed, but appears
to maintain elements in insertion order using a linked list.

 

***Map***

Maps, like arrays and Collections, can easily be expanded to multiple
dimensions; you simply make a Map whose values are Maps

 

***Queue***

A queue is typically a “first-in, first-out" (FIFO) container. That is,
you put things in at one end and pull them out at the other, and the
order in which you put them in will be the same order in which they come
out. Queues are commonly used as a way to reliably transfer objects from
one area of a program to another. Queues are especially important in
concurrent programming. offer( ) is one of the Queue-specific methods;
it inserts an element at the tail of the queue if it can, or returns
false

 

***PriorityQueue***

First-in, first-out (FIFO) describes the most typical queuing
discipline. A queuing discipline is what decides, given a group of
elements in the queue, which one goes next. First-in, first-out says
that the next element should be the one that was waiting the longest.
Apriority queue says that the element that goes next is the one with the
greatest need (the highest priority).

When you offer( ) an object onto a PriorityQueue, that object is sorted
into the queue.5 The default sorting uses the natural order of the
objects in the queue, but you can modify the order by providing your own
Comparator. The PriorityQueue ensures that when you call peek( ), poll(
) or remove( ), the element you get will be the one with the highest
priority

 

**Collection** is the root interface that describes what is common for
all sequence containers. implementing Collection also means providing an
iterator( ) method: In addition, the java.utiLAbstractCollection class
provides a default implementation for a Collection, so that you can
create a new subtype of AbstractCollection without unnecessary code
duplication. So if I write a method that takes a Collection, that method
can be applied to any type that implements Collection—and this allows a
new class to choose to implement Collection in order to be used with my
method

 

![](media/image1.png){width="9.875in" height="4.114583333333333in"}

 

 

The dotted boxes represent interfaces, and the solid boxes are regular
(concrete) classes. The dotted lines with hollow arrows indicate that a
particular class is implementing an interface. The solid arrows show
that a class can produce objects of the class the arrow is pointing to

 

Wednesday, August 05, 2015

11:27

 

An exceptional condition is a problem that prevents the continuation of
the current method or scope. It’s important to distinguish an
exceptional condition from a normal problem, in which you have enough
information in the current context to somehow cope with the difficulty.
With an exceptional condition, you cannot continue processing because
you don’t have the information necessary to deal with the problem in the
current context. All you can do is jump out of the current context and
relegate that problem to a higher context. This is what happens when you
throw an exception. When you throw an exception, several things happen.
First, the exception object is created in the same way that any Java
object is created: on the heap, with new. Then the current path of
execution (the one you couldn’t continue) is stopped and the reference
for the exception object is ejected from the current context. At this
point the exception-handling mechanism takes over and begins to look for
an appropriate place to continue executing the program. This appropriate
place is the exception handler, whose job is to recover from the problem
so the program can either try another tack or just continue.

 

Exceptions allow you to (if nothing else) force the program to stop and
tell you what went wrong, or (ideally) force the program to deal with
the problem and return to a stable state.

 

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

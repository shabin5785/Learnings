 

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

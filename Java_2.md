 

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

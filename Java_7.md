 

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

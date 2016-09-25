 

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

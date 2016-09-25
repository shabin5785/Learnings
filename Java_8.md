 

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

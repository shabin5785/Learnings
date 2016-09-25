 

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

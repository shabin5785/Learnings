Command Line

Thursday, January 21, 2016

11:35

 

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Compile a file by adding dependent jars.. package com.test.

so copy file inside com/test and compile from inside test....

 

javac -cp .:/jars/\* com/template/\*.java

javac -cp .:/home/pms/logtail/lib/\* GbFileWriter.java

 

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

 

java -cp \*:. com/infy/test/graphite/TestGraphite

java -cp \*:./classes logrotate.LogWriter & ==== java -cp
\*:./classes:lib/log4j-1.2.17.jar logrotate.LogWriter

 

java -cp \*:. com/pms/UploadToGraph

 

 

From the docs
--&gt; <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/javac.html> See
the option section.

-d directory

Set the destination directory for class files. The directory must
already exist; javac will not create it. If a class is part of a
package, javac puts the class file in a subdirectory reflecting the
package name, creating directories as needed. For example, if you
specify -d C:\\myclasses and the class is called com.mypackage.MyClass,
then the class file is called
C:\\myclasses\\com\\mypackage\\MyClass.class. If -d is not specified,
javac puts each class files in the same directory as the source file
from which it was generated.

Note: The directory specified by -d is not automatically added to your
user class path.

 

 

When you invoke a program using java on the command-line, you should
supply the fully-qualified class name of the class that contains
your main method and omit the *.class*, like so:

java com.Hello

The java program needs this fully-qualified class name to understand
which class you are referring to.

 

From
&lt;<http://stackoverflow.com/questions/12096016/java-cant-find-main-class>&gt;

 

 

 

 

OCJP 1

Wednesday, January 27, 2016

10:14

 

**Interfaces**

A powerful companion to inheritance is the use of interfaces. Interfaces
are like a 100-percent abstract superclass that defines the methods a
subclass must support, but not how they must be supported

 

**Identifiers** must start with a letter, a currency character ( \$ ),
or a connecting character such as the underscore ( \_ ). Identifiers
cannot start with a digit! Identifiers in Java are **case-sensitive**;
foo and FOO are two different identifiers.

 

import and package statements apply to all classes within a source code
file.

In other words, there's no way to declare multiple classes in a file and
have

them in different packages or use different imports.

 

The **javac** command is used to invoke Java's compiler.Here's the
structural overview for javac :

javac \[options\] \[source files\]

 

The **java** command is used to invoke the Java Virtual Machine (JVM).
Here's the

basic structure of the command:

java \[options\] class \[args\]

 

naming a method main() doesn't give it the superpowers we normally
associate with main(). As far as the compiler and the JVM are concerned,
the only version of main() with superpowers is the main() with this
signature:

**public static void main(String\[\] args) **

Other versions of main() with other signatures are perfectly legal, but
they're

treated as normal methods.

 

here is some flexibility in the declaration of the "special" main()
method (the one used to start a Java application): the order of its
modifiers can be altered a little, the String array doesn't have to be
named args , and as of Java 5 it can be declared using var-args syntax.
The following are all legal declarations for the "special" main() :

static public void main(String\[\] args)

public static void main(String... x)

static public void main(String bang\_a\_gong\[\])

Only other thing that's important for you to know is that

**main() can be overloaded**

** **

Static imports can be used when you want to "save typing" while using a
class's static members. (You can use this feature on classes in the API
and on your own classes.)

 

When we say code from one class (class A) has access to another class
(class B), it means class A can do one of three things:

■ Create an instance of class B.

■ Extend class B (in other words, become a subclass of class B).

■ Access certain methods and variables within class B, depending on the
access

control of those methods and variables.

In effect, access means visibility.

 

 

You can modify a class declaration using the keyword **final , abstract
, or **

**strictfp .**

** **

Marking a class as strictfp means that any method code in the class will

conform to the IEEE 754 standard rules for floating points. Without that
modifier, floating points used in the methods might behave in a
platform-dependent way. If you don't declare a class as strictfp , you
can still get **strictfp** behavior on a method-by-method basis, by
declaring a method as strictfp

 

 

 

 

A **final class** obliterates a key benefit of OO—extensibility. So
unless you have a serious safety or security issue, assume that someday
another programmer will need to extend your class.

 

An **abstract class** can never be instantiated. Its sole purpose,
mission in life, raison d'être, is to be extended (subclassed). (Note,
however, that you can compile and execute an abstract class, as long as
you don't try to make an instance of it.)

 

Coding with abstract class types (including interfaces, discussed later
in this

chapter) lets you take advantage of **polymorphism**, and gives you the
greatest degree of flexibility and extensibility.

 

a class as both abstract and final . They have nearly opposite meanings.
An abstract class must be subclassed, whereas a final class must not be
subclassed. If you see this combination of abstract and final modifiers
used for a class or method declaration, the code will not compile

 

When you create an interface, you're defining a contract for what a
class can do, without saying anything about how the class will do it.
**An interface is a contract.** interface as a 100-percent abstract
class.

 

 

■ All interface methods are implicitly public and abstract . In other
words,

you do not need to actually type the public or abstract modifiers in the

method declaration, but the method is still always public and abstract .

■ All variables defined in an interface must be public , static , and
final —

in other words, interfaces can declare only constants, not instance
variables.

■ Interface methods must not be static .

■ Because interface methods are abstract, they cannot be marked final ,

strictfp , or native . (More on these modifiers later in the chapter.)

■ An interface can extend one or more other interfaces.

■ An interface cannot extend anything but another interface.

■ An interface cannot implement another interface or class.

■ An interface must be declared with the keyword interface .

■ Interface types can be used polymorphically

 

**it is not an overriding method!** It is simply a method that happens
to have the same name as a private method (which you're not supposed to
know about) in the superclass. The rules of overriding do not apply, so
you can make this newly-declared-but-just-happens-to-match method
declare new exceptions, or change the return type, or do anything else
you want it to do.

 

It means the subclass inherits the member. It does not, however, mean
the subclass-outside-the-package can access the member using a reference
to an instance of the superclass. In other words, protected =
inheritance. Protected does not mean that the subclass can treat the
protected superclass member as though it were public. So if the
subclass-outside-the-package gets a reference to the superclass (by, for
example, creating an instance of the superclass somewhere in the
subclass' code), the subclass cannot use the dot operator on the
superclass reference to access the protected member. To a
subclass-outside-the- package, a protected member might as well be
default (or even private ), when the subclass is using a reference to
the superclass. The subclass can see the protected member only through
inheritance

** **

package certification;

public class Parent {

protected int x = 9; // protected access

}

 

 

 

 

 

package other;

// Different package

import certification.Parent;

class Child extends Parent {

public void testIt() {

System.out.println("x is " + x); // No problem; Child

// inherits x

}

}

 

package other;

import certification.Parent;

class Child extends Parent {

public void testIt() {

System.out.println("x is " + x);

//

//

Parent p = new Parent();

//

//

System.out.println("X in parent is " + p.x); //

}

}

 

**For a subclass outside the package, the protected member can be
accessed only through inheritance**.

 

Once the subclass-outside-the-package inherits the protected member,
that

member (as inherited by the subclass) becomes private to any code
outside the

subclass, with the exception of subclasses of the subclass.

 

**There is never a case where an access modifier can be applied to a
local variable,In fact, there is only one modifier that can ever be
applied to local **

**variables— final .**

 

It's legal to extend SuperClass , since the class isn't marked final ,
but we can't override the final method

 

You can, however, have an abstract class with no abstract methods.

 

 

**Var-arg limits** : The var-arg must be the last parameter in the
method's

signature, and you can have only one var-arg in a method

** **

Constructors can't be marked static (they are after all associated with
object instantiation), and they can't be marked final or abstract
(because they can't be overridden)

 

**Instance Variables** : Instance variables are defined inside the
class, but outside of any method, and are initialized only when the
class is instantiated. Instance variables are the fields that belong to
each unique object

 

A **local variable** is a variable declared within a method. That means
the variable is not just initialized within the method, but also
declared within the method. Just as the local variable starts its life
inside the method, it's also destroyed when the method has completed.
Local variables are always on the stack, not the heap. Although the
value of the variable might be passed into, say, another method that
then stores the value in an instance variable, the variable itself lives
only within the scope of the method.

 

while the local variable is on the stack, if the variable is an object
reference, the object itself will still be created on the heap. There is
no such

thing as a stack object, only a stack variable.

 

It is possible to declare a local variable with the same name as an
instance

variable. It's known as **shadowing.** To avoid name collision, use the
keyword **this**,it refers to the object currently running.

 

Arrays can hold either primitives or object references, but **an array
itself will always be an object on the heap**, even if the array is
declared to hold primitive elements. In other words, there is no such
thing as a primitive array, but you can make an array of primitive

 

A reference variable marked **final** can't ever be reassigned to refer
to a different object. The data within the object can be modified, but
the reference variable cannot be changed. In other words, a final
reference still allows you to modify the state of the object it refers
to, but you can't modify the reference variable to make it refer to a
different object.

 

enum CoffeeSize { BIG, HUGE, OVERWHELMING };

It's not required that enum constants be in all caps.enum that isn't
enclosed in a class can be declared with only the public or default
modifier, just like a non-inner class

 

Every enum has a static method, **values()** , that returns an array of
the

enum 's values in the order they're declared.

 

You can NEVER invoke an enum constructor directly. The enum constructor

is invoked automatically, with the arguments you define after the
constant

value.

You can define more than one argument to the constructor, and you can

overload the enum constructors

 

 

The ability to make changes in your implementation code without breaking
the

code of others who use your code is a key benefit of **encapsulation**.
You want to hide implementation details behind a public programming
interface. By interface, we mean the set of accessible methods your code
makes available for other code to call—in other words, your code's API.
By hiding implementation details, you can rework your method code

 

Whenever you create a class, you automatically inherit all of class
**Object** 's methods

 

Code reuse through inheritance means that methods with generic

functionality. The second (and related) use of inheritance is to allow
your classes to be accessed **polymorphically**—a capability provided by
interfaces as well.

 

In OO, the concept of **IS-A** is based on class inheritance or
interface

implementation. IS-A is a way of saying, "This thing is a type of that
thing.

 

**HAS-A** relationships are based on usage, rather than inheritance. In
other words,

class A HAS-A B if code in class A has a reference to an instance of
class B.

 

**Reference Variable**

 

■ A reference variable can be of only one type, and once declared, that
type

can never be changed (although the object it references can change).

■ A reference is a variable, so it can be reassigned to other objects
(unless the reference is declared final ).

■ A reference variable's type determines the methods that can be invoked
on

the object the variable is referencing.

■ A reference variable can refer to any object of the same type as the
declared

reference, or—this is the big one—it can refer to any subtype of the
declared

type!

 

■ A reference variable can be declared as a class type or an interface
type. If

the variable is declared as an interface type, it can reference any
object of any class that implements the interface

 

method invocations allowed by the compiler are based solely on the
declared type of the reference, regardless of the object type.

 

even though the compiler only knows about the declared reference type,
the Java Virtual Machine **(JVM) at runtime knows what the object really
is**.

 

*Polymorphic method invocations apply only to instance methods. You can
always *

*refer to an object with a more general reference variable type (a
superclass or *

*interface), but at runtime, the ONLY things that are dynamically
selected based *

*on the actual object (rather than the reference type) are instance
methods. Not *

*static methods. Not variables. Only overridden instance methods are
dynamically *

*invoked based on the real object's type.*

* *

For abstract methods you inherit from a superclass, you have no choice:
You must

implement the method in the subclass unless the subclass is also
abstract.

 

**The overriding method cannot have a more restrictive access modifier
than the **

**method being overridden** (for example, you can't override a method
marked public

and make it protected ).What makes that superclass reference to a
subclass instance possible is that the subclass is guaranteed to be able
to do everything the superclass can do. The access level **CAN be less
restrictive** than that of the overridden method.The overriding method
CAN throw any unchecked (runtime) exception, regardless of whether the
overridden method declares the exception

The overriding method must NOT throw checked exceptions that are new or
broader than those declared by the overridden method. For example, a
method that declares a FileNotFoundException cannot be overridden by a
method that declares a SQLException , Exception , or any other non-
runtime exception unless it's a subclass of FileNotFoundException .The
overriding method can throw narrower or fewer exceptions. **You cannot
override a method marked static.If a method can't be inherited, you
cannot override it**

 

Using **super** to invoke an overridden method applies only to instance

methods. (Remember that static methods can't be overridden.) And you can
use

super only to access a method in a class' superclass, not the superclass
of the

superclass

 

**OverLoading**

■ Overloaded methods MUST change the argument list.

■ Overloaded methods CAN change the return type.

■ Overloaded methods CAN change the access modifier.

■ Overloaded methods CAN declare new or broader checked exceptions.

■ A method can be overloaded in the same class or in a subclass. In
other words,

if class A defines a doStuff(int i) method, the subclass B could define
a

doStuff(String s) method without overriding the superclass version that

takes an int . So two methods with the same name but in different
classes

can still be considered overloaded if the subclass inherits one version
of the

method and then declares another overloaded version in its class
definition.

 

To summarize, which overridden version of the method to call (in other
words, from which class in the inheritance tree) is decided at runtime
based on object type, but which overloaded version of the method to call
is based on the reference type of the argument passed at compile time.

 

So it's true that polymorphism doesn't determine which overloaded
version is called; polymorphism does come into play when the decision is
about which overridden version of a method is called.

 

 

 

 

Dog d = (Dog) animal; // compiles but fails later

All the compiler can do is verify that the two types are in the same

inheritance tree, so that depending on whatever code might have come
before the

downcast, it's possible that animal is of type Dog . The compiler must
allow things that might possibly work at runtime. However, if the
compiler knows with certainty that the cast could not possibly work,
compilation will fail.

 

Unlike downcasting, **upcasting** (casting up the inheritance tree to a
more general

type) works implicitly (that is, you don't have to type in the cast)
because when you upcast you're implicitly restricting the number of
methods you can invoke, as opposed to downcasting, which implies that
later on, you might want to invoke a more specific method.

 

An implementation class can itself be abstract ! For example, the
following is legal for a class Ball implementing Bounceable :

abstract class Ball implements Bounceable { }

 

subclassing defines who and what you are, whereas implementing defines a
role you can play or a hat you can wear, d espite how different you
might be from some other class implementing the same interface

 

An interface can itself extend another interface, but it can never
implement

anything.An interface can extend more than one interface! a class is not
allowed to extend multiple classes in Java. An interface, however, is
free to extend multiple interfaces

 

**Return Types**

 

if you inherit a method but overload it in a subclass, you're not

subject to the restrictions of overriding, which means you can declare
any return type you like. **What you can't do is change only the return
type. To overload a method, remember, you must change the argument
list.**

 

public class Foo{

void go() { }

}

public class Bar extends Foo {

String go(int x) {

return null;

}

}

 

Or, as of Java 5, you're allowed to change the return type in the

overriding method as long as the new return type is a subtype of the
declared return type of the overridden (superclass) method

 

class Alpha {

Alpha doStuff(char c) {

return new Alpha();

}

}

class Beta extends Alpha {

Beta doStuff(char c) {

return new Beta();

}

}

 

In a method with a primitive return type, you can return any value or
vari-

able that can be implicitly converted to the declared return type.

public int foo() {

char c = 'c';

return c; // char is compatible with int

}

 

**Constructors and Instantiation**

** **

Horse h = new Horse();

But what really happens when you say new Horse() ? (Assume Horse extends

Animal and Animal extends Object .)

 

1\. Horse constructor is invoked. Every constructor invokes the
constructor

of its superclass with an (implicit) call to super() , unless the
constructor

invokes an overloaded constructor of the same class (more on that in a

minute).

2\. Animal constructor is invoked ( Animal is the superclass of Horse ).

3\. Object constructor is invoked At this point we're on the top of the
stack.

4\. Object instance variables are given their explicit values. By
explicit values, we mean values that are assigned at the time the
variables are declared, such as int x = 27 , where 27 is the explicit
value

5\. Object constructor completes.

6\. Animal instance variables are given their explicit values (if any).

7\. Animal constructor completes.

8\. Horse instance variables are given their explicit values (if any).

9\. Horse constructor completes.

 

 

■ Constructors can use any access modifier, including private .

■ It's legal (but stupid) to have a method with the same name as the
class,

but that doesn't make it a constructor. If you see a return type, it's a
method

rather than a constructor. In fact, you could have both a method and a

constructor with the same name—the name of the class—in the same class,

and that's not a problem for Java.

■ Every constructor has, as its first statement, either a call to an
overloaded

constructor ( this() ) or a call to the superclass constructor ( super()
),

although remember that this call can be inserted by the compiler.

■ A no-arg constructor is not necessarily the default (that is,
compiler-supplied) constructor, although the default constructor is
always a no-arg constructor. The default constructor is the one the
compiler provides! Although the default constructor is always a no-arg
constructor, you're free to put in your own no-arg constructor.

■ You cannot make a call to an instance method or access an instance
variable

until after the super constructor runs.

■ Only static variables and methods can be accessed as part of the call
to

super() or this() .

■ Abstract classes have constructors, and those constructors are always
called

when a concrete subclass is instantiated.

■ Interfaces do not have constructors. Interfaces are not part of an
object's

inheritance tree.

■ The only way a constructor can be invoked is from within another
constructor.

 

 

If your superclass does not have a no-arg constructor, you must type a
constructor in your class (the subclass) because you need a place to put
in the call to super() with the appropriate arguments.

 

**constructors are never inherited.They can't be overridden**

** **

this() always means a call to another constructor in the same class.

The first line in a constructor must be a call to super() or a call to
this()

If you have neither of those calls in your constructor, the compiler
will insert the no-arg call to super(). The preceding rule means a
constructor can never have both a call to super() and a call to this() .
Because each of those calls must be the first statement in a
constructor, you can't legally use both in the same constructor. That
also means the compiler will not put a call to super() in any
constructor that has a call to this() .

 

 

 

 

**Initialization blocks**

 

Initialization blocks are the third place in a Java program where
operations can be performed. Initialization blocks run when the class is
first loaded (a static initialization block) or when an instance is
created (an instance initialization block)

 

A static initialization block runs once, when the class is first loaded.
An instance initialization block runs once every time a new instance is
created.

 

It is important to note that unlike methods or constructors, the order
in which initialization blocks appear in a class matters. When it's time
for initialization blocks to run, if a class has more than one, they
will run in the order in which they appear in the class file—in other
words, from the top down

 

**Static**

 

static methods can't be overridden! This doesn't mean they can't be
redefined in a subclass, but redefining and overriding aren't the same
thing.

 

***Storage***

*** ***

■ Instance variables and objects live on the heap.

■ Local variables live on the stack.

main() is placed on the stack.(Methods on stack). Local objects, like
passed to functions are kept on stack(Copy of reference..). So reference
on stack..

 

 

**characters** are just 16-bit unsigned integers under the hood. That
means you can assign a number literal, assuming it will fit into the
unsigned 16-bit range (0 to 65535).

 

A variable referring to an object is just that—a **reference variable**.
A reference variable bit holder contains bits representing a way to get
to the object. Not an object. All we can say for sure is that the
variable's value is not the object, but rather a value representing a
specific object on the heap.

 

**Casting** lets you convert primitive values from one type to
another.Casts can be implicit or explicit. An implicit cast means you
don't have to write code for the cast; the conversion happens
automatically. Typically, an implicit cast

happens when you're doing a widening conversion—in other words, putting
a

smaller thing (say, a byte ) into a bigger container (such as an int
).The large-value-into-small-container conversion is referred to as
narrowing and requires an explicit cast, where you tell the compiler
that you're aware of the danger and accept full responsibility.

 

 

**Float**

every floating-point literal is implicitly a double (64 bits), not a
float . So the literal 32.3 , for example, is considered a double . If
you try to assign a double to a float , the compiler knows you don't
have enough room in a 32-bit float container to hold the precision of a
64-bit double , and it lets you know. The following code looks good, but
it won't compile:

float f = 32.3;

In order to assign a floating-point literal to a float variable, you
must either cast the value or append an f to the end of the literal

 

**Reference Variable Assignments.**

** **

Button b = new Button();

 

 

 

The preceding line does three key things:

■ Makes a reference variable named b , of type Button

■ Creates a new Button object on the heap

■ Assigns the newly created Button object to the reference variable b

 

public class Foo {

public void doFooStuff() { }

}

public class Bar extends Foo {

public void doBarStuff() { }

}

class Test {

public static void main (String \[\] args) {

Foo reallyABar = new Bar(); // Legal because Bar is a

// subclass of Foo

Bar reallyAFoo = new Foo(); // Illegal! Foo is not a

// subclass of Bar

}

}

***The rule is that you can assign a subclass of the declared type but
not a superclass of the declared type***. Remember, a Bar object is
guaranteed to be able to do anything a Foo can do, so anyone with a Foo
reference can invoke Foo methods even though the object is actually a
Bar .

In the preceding code, we see that Foo has a method doFooStuff() that
someone with a Foo reference might try to invoke. If the object
referenced by the Foo variable is really a Foo , no problem. But it's
also no problem if the object is a Bar , since Bar inherited the
doFooStuff() method. You can't make it work in

reverse, however. If somebody has a Bar reference, they're going to
invoke

doBarStuff() , but if the object is a Foo , it won't know how to
respond.

 

 

**Variable Scope**

** **

■ Static variables have the longest scope; they are created when the
class is

loaded, and they survive as long as the class stays loaded in the Java
Virtual

Machine (JVM).

■ Instance variables are the next most long-lived; they are created when
a new

instance is created, and they live until the instance is removed.

■ Local variables are next; they live as long as their method remains on
the stack. As we'll soon see, however, local variables can be alive and
still be "out of scope."

■ Block variables live only as long as the code block is executing.

 

 

**Array Instance Variables**

** **

An array is an object; thus, an array instance variable that's declared
but not explicitly initialized will have a value of null , just as any
other object reference instance variable.

if the array is initialized, what happens to the elements contained in
the array? All array elements are given their default values—the same
default values that elements of that type get when they're instance
variables. The bottom line: Array elements are always, always, always
given default values, regardless of where the array itself is declared
or instantiated

 

 

**Local (Stack, Automatic) Primitives and Objects**

Local variables are defined within a method, and they include a method's
parameters

Instance variable references are always given a default value of null,
until they are explicitly initialized to something else. But local
references are not given a default value; in other words, they aren't
null. If you don't initialize a local reference variable, then by
default, its value is—well that's the whole point: it doesn't have any
value at all!

 

Array elements are given their default values (0, false, null,
'\\u0000', and so on) regardless of whether the array is declared as an
instance or local variable. The array object itself, however, will not
be initialized if it's declared locally. In other words, you must
explicitly initialize an array reference if it's declared and used
within a method, but at the moment you construct an array object, all of
its elements are assigned their default values

 

With primitive variables an assignment of one variable to another means
the contents (bit pattern) of one variable are copied into another.
Object reference variables work exactly the same way. The contents of a
reference variable are a bit pattern so if you assign reference variable
a1 to reference variable b1 the bit pattern in a1 is copied and the new
copy is placed into b1.

 

One exception to the way object references are assigned is String. In
Java, String objects are given special treatment. For one thing, String
objects are immutable; you can't change the value of a String object.
But any time we make any changes at all to a String the VM will update
the reference variable to refer to a different object. The different
object might be a new object or it might not be but it will definitely
be a different object. The reason we can't say for sure whether a new
object is created is because of the String constant pool.

 

■ A new string is created (or a matching String is found in the String
pool), leaving the original String object untouched.

■ The reference used to modify the String (or rather, make a new String
by modifying a copy of the original) is then assigned the brand new
String object.

 

**Passing Object Reference Variables**

 

When you pass an object variable into a method, you must keep in mind
that you're passing the object reference, and not the actual object
itself. you aren't even passing the actual reference variable but rather
a copy of the reference variable. A copy of a variable means you get a
copy of the bits in that variable so when you pass a reference variable
you're passing a copy of the bits representing how to get to a specific
object. In other words both the caller and the called method will now
have identical copies of the reference; thus both will refer to the same
exact (not a copy) object on the heap

 

Java is actually pass-by-value for all variables running within a single
VM. Pass-by-value means pass-by-variable-value. And that means
pass-by-copy-ofthe- variable!. It makes no difference if you're passing
primitive or reference variables; you are always passing a copy of the
bits in the variable. So for a primitive variable you're passing a copy
of the bits representing the value. For example if you pass an int
variable with the value of 3 you're passing a copy of the bits
representing 3. The called method then gets its own copy of the value to
do with it what it likes. And if you're passing an object reference
variable you're passing a copy of the bits representing the reference to
an object. The called method then gets its own copy of the reference
variable to do with it what it likes. But because two identical
reference variables refer to the exact same object if the called method
modifies the object (by invoking setter methods for example) the caller
will see that the object the caller's original variable refers to has
also been changed

 

The called method can't change the caller's variable, although for
object reference variables, the called method can change the object the
variable referred to. it means the called method can't reassign the
caller's original reference variable and make it refer to a different
object or null

 

**Shadowing** involves reusing a variable name that's already been
declared somewhere else. The effect of shadowing is to hide the
previously declared variable in such a way that it may look as though
you're using the hidden variable but you're actually using the shadowing
variable.

 

**Memory Management and Garbage Collection**

 

The heap is that part of memory where Java objects live, and it's the
one and only part of memory that is in any way involved in the garbage
collection process. When the garbage collector runs its purpose is to
find and delete objects that cannot be reached. If you think of a Java
program as being in a constant cycle of creating the objects it needs
(which occupy space on the heap) and then discarding them when they're
no longer needed creating new objects discarding them and so on the
missing piece of the puzzle is the garbage collector. When it runs it
looks for those discarded objects and deletes them from memory so that
the cycle of using memory and releasing it can continue.

 

The garbage collector is under the control of the JVM; JVM decides when
to run the garbage collector. From within your Java program you can ask
the JVM to run the garbage collector but there are no guarantees under
any circumstances that the JVM will comply. Left to its own devices the
JVM will typically run the garbage collector when it senses that memory
is running low.

 

You might hear that the garbage collector uses a mark and sweep
algorithm and for any given Java implementation that might be true but
the Java specification doesn't guarantee any particular implementation.
You might hear that the garbage collector uses reference counting; once
again maybe yes maybe no.

 

In a nutshell every Java program has from one to many threads. Each
thread has its own little execution stack. Normally you (the programmer)
cause at least one thread to run in a Java program the one with the
main() method at the bottom of the stack. In addition to having its own
little execution stack each thread has its own lifecycle. ***an object
is eligible for garbage collection when no live thread can access it***.
When we talk about reaching an object we're really talking about having
a reachable reference variable that refers to the object in question. If
our Java program has a reference variable that refers to an object and
that reference variable is available to a live thread then that object
is considered reachable.

 

Can a Java application run out of memory? Yes. The garbage collection
system attempts to remove objects from memory when they are not used.
However if you maintain too many live objects (objects referenced from
other live objects) the system can run out of memory

 

-   The first way to remove a reference to an object is to set the
    > reference variable that refers to the object to null

-   We can also decouple a reference variable from an object by setting
    > the reference variable to refer to another object. Objects that
    > are created in a method also need to be considered. When a method
    > is invoked any local variables created exist only for the duration
    > of the method. Once the method has returned the objects created in
    > the method are eligible for garbage collection. There is an
    > obvious exception however. If an object is returned from the
    > method its reference might be assigned to a reference variable in
    > the method that called it; hence it will not be eligible for
    > collection

 

 

**the finalize() Method**

 

Java provides a mechanism that lets you run some code just before your
object is deleted by the garbage collector. This code is located in a
method named finalize()

that all classes inherit from class Object. you can never count on the
garbage collector to delete an object. So any code that you put into
your class's overridden finalize() method is not guaranteed to run.
Because the finalize() method for any given object might run but you
can't count on it don't put any essential code into your finalize()
method

 

**Operators**

Reference variables can be tested to see if they refer to the same
object by using the == operator. Remember the == operator is looking at
the bits in the variable so for reference variables this means that if
the bits in both reference variables are identical then both refer to
the same object.

 

**The equals() Method in Class Objec**t The equals() method in class
Object works the same way that the == operator works. If two references
point to the same object the equals() method will return true. If two
references point to different objects even if they have the same values
the method will return false.

 

**The equals() Method in Class String** The equals() method in class
String has been overridden. When the equals() method is used to compare
two strings it will return true if the strings have the same value and
it will return false if the strings have different values. For String's
equals() method values ARE case sensitive.

 

**Equality for enums** *Once you've declared an enum it's not
expandable. At runtime there's no way to make additional enum
constants*. Of course you can have as many variables as you'd like refer
to a given enum constant so it's important to be able to compare two
enum reference variables to see if they're "equal"—that is do they refer
to the same enum constant. You can use either the == operator or the
equals() method to determine whether two variables are referring to the
same enum constant:

 

The **instanceof** operator is used for object reference variables only
and you can use it to check whether an object is of a particular type.
By "type " we mean class or interface type—in other words whether the
object referred to by the variable on the left side of the operator
passes the IS-A test for the class or interface type on the right side.
Even if the object being tested is not an actual instantiation of the
class type on the right side of the operator instanceof will still
return true if the object being compared is assignment compatible with
the type on the right. In addition, it is legal to test whether the null
reference is an instance of a class. This will always result in false,

 

**String Concatenation**

 

String a = "String";

int b = 3;

int c = 7;

System.out.println(a + b + c);

String37

System.out.println(a + (b + c));

String10

 

Using parentheses causes the (b + c) to evaluate first so the rightmost
+ operator functions as the addition operator given that both operands
are int values. The key point here is that within the parentheses the
left-hand operand is not a String. If it were then the + operator would
perform String concatenation

 

use the **increment or decrement operators on a final variable**.
Because final variables can't be changed the increment and decrement
operators can't be used with them and any attempt to do so will result
in a compiler error.

 

 

 

 

 

 

 

 

 

 

 

 

 

 

OCJP 2

Wednesday, January 27, 2016

14:40

 

**The String Class**

 

In Java, strings are objects. As with other objects, you can create an
instance of a string with the new keyword, as follows:

String s = new String();

This line of code creates a new object of class String and assigns it to
the reference variable s.

The Java Virtual Machine (JVM) took the value of string s (which was
"abcdef") and tacked " more stuff" onto the end giving us the value
"abcdef more stuff". Since strings are immutable the JVM couldn't stuff
this new value into the old String referenced by s so it created a new
String object gave it the value "abcdef more stuff" and made s refer to
it. At this point in our example we have two String objects: the first
one we created with the value "abcdef" and the second one with the value
"abcdef more stuff". Technically there are now three String objects
because the literal argument to concat " more stuff" is itself a new
String object. First and third are lost.

 

To make Java more memory efficient the JVM sets aside a special area of
memory called the String constant pool. When the compiler encounters a
String literal it checks the pool to see if an identical String already
exists. If a match is found the reference to the new literal is directed
to the existing String and no new String literal object is created. (The
existing String simply has an additional reference.). If several
reference variables refer to the same String without even knowing it, it
would be very bad if any of them could change the String's value. (Hence
immutable)

 

**The StringBuilder Class**

 

The java.lang.StringBuilder class should be used when you have to make a
lot of modifications to strings of characters. objects of type
StringBuilder can be modified over and over again without leaving behind
a great effluence of discarded String objects.

 

The StringBuilder class was added in Java 5. It has exactly the same API
as the StringBuffer class, except StringBuilder is not thread-safe. In
other words, its methods are not synchronized. Oracle recommends that
you use StringBuilder instead of StringBuffer whenever possible, because
StringBuilder will run faster (and perhaps jump higher).

 

**Arrays**

 

Constructing an array means creating the array object on the heap (where
all objects live)—that is doing a new on the array type. To create an
array object Java must know how much space to allocate on the heap so
you must specify the size of the array at creation time. The size of the
array is the number of elements the array will hold.

 

Arrays of object types can be constructed in the same way:

Thread\[\] threads = new Thread\[5\]; // no Thread objects created!

> // one Thread array created

Remember that, despite how the code appears, the Thread constructor is
not being invoked. We're not creating a Thread instance, but rather a
single Thread array object. After the preceding statement, there are
still no actual Thread objects!. The preceding code produces just one
object (the array assigned to the reference variable named threads). The
single object referenced by threads holds five Thread reference
variables but no Thread objects have been created or assigned to those
references.

 

So a two-dimensional array of type int is really an object of type int
array (int \[\]) with each element in that array holding a reference to
another int array. The second dimension holds the actual int primitives.
The following code declares and constructs a two-dimensional array of
type int:

int\[\]\[\] myArray = new int\[3\]\[\];

Notice that only the first brackets are given a size. That's acceptable
in Java since the JVM needs to know only the size of the object assigned
to the variable myArray.

 

"an array of five strings " even though what we really mean is "an array
of five references to String objects." Then the big question becomes
whether or not those references are actually pointing (oops this is Java
we mean referring) to real String objects or are simply null. Remember a
reference that has not had an object assigned to it is a null reference.
And if you actually try to use that null reference by say applying the
dot operator to invoke a method on it you'll get the infamous
NullPointerException

 

![](media/image1.png){width="6.0in" height="3.2708333333333335in"}

 

 

Dog puppy = new Dog("Frodo");

Dog\[\] myDogs = {puppy, new Dog("Clover"), new Dog("Aiko")};

 

![](media/image2.png){width="6.0in" height="2.8333333333333335in"}

 

 

If the declared array type is a class, you can put objects of any
subclass of the declared type into the array. For example, if Subaru is
a subclass of Car, you can put both Subaru objects and Car objects into
an array of type Car. If the array is declared as an interface type, the
array elements can refer to any instance of any class that implements
the declared interface. The bottom line is this: Any object that passes
the IS-A test for the declared array type can be assigned to an element
of that array.

 

It's tempting to assume that because a variable of type byte, short, or
char can be explicitly promoted and assigned to an int, an array of any
of those types could be assigned to an int array. You can't do that in
Java. Arrays that hold object references, as opposed to primitives,
aren't as restrictive. Just as you can put a Honda object in a Car array
(because Honda extends Car), you can assign an array of type Honda to a
Car array reference variable

 

When you assign an array to a previously declared array reference the
array you're assigning must be in the same dimension as the reference
you're assigning it to. For example a two-dimensional array of int
arrays cannot be assigned to a regular int array reference

 

**ArrayLists**

 

The ArrayList maintained its order. Generics, but what's important to
know is that this is how you tell the compiler and the JVM that for this
particular ArrayList that you want only Strings to be allowed. What this
means is that if the compiler can tell that you're trying to add a
"not-a- String" object to this ArrayList your code won't compile

 

*Object Copy*

 

when we invoke getName() we do in fact return a copy just like Java
always does. But we're not returning a copy of the StringBuilder object;
we're returning a copy of the reference variable that points to (I know)
the one-and-only StringBuilder object we ever built. So at the point
that getName() returns we have one StringBuilder object and two
reference variables pointing to it (s and s2). For the purpose of the
OCA exam the key point is this: When encapsulating a mutable object like
a StringBuilder or an array or an ArrayList if you want to let outside
classes have a copy of the object you must actually copy the object and
return a reference variable to the object that is a copy. If all you do
is return a copy of the original object's reference variable you DO NOT
have encapsulation.

 

**Switch**

the switch can only check for equality. This means that the other
relational operators such as greater than are rendered unusable in a
case. It's also illegal to have more than one case label using the same
value .Strings are case-sensitive, DOES NOT match.

case constants are evaluated from the top down, and the first case
constant that matches the switch's expression is the execution entry
point. In other words once a case constant is matched the Java Virtual
Machine (JVM) will execute the associated code block and ALL subsequent
code blocks (barring a break statement) too. This dropping down is
actually called "**fall-through** " because of the way execution falls
from one case to the next

 

**Exception handling**

Exception handling works by transferring the execution of a program to
an appropriate exception handler when an exception occurs. To do this we
use the try and catch keywords. The try is used to define a block of
code in which exceptions may occur. This block of code is called a
"guarded region" (which really means "risky code goes here"). One or
more catch clauses match a specific exception (or group of
exceptions—more on that later) to a block of code that handles it. Once
control jumps to

the catch block, it never returns to complete the balance of the try
block.

It is illegal to use a try clause without either a catch clause or a
finally clause.

 

**Using finally**

Although try and catch provide a terrific mechanism for trapping and
handling exceptions, we are left with the problem of how to clean up
after ourselves if an exception occurs. Because execution transfers out
of the try block as soon as an exception is thrown, we can't put our
cleanup code at the bottom of the try block and expect it to be executed
if an exception occurs. Almost as bad an idea would be placing our
cleanup code in each of the catch blocks

 

Exception handlers are a poor place to clean up after the code in the
try block because each handler then requires its own copy of the cleanup
code. If for example you allocated a network socket or opened a file
somewhere in the guarded region each exception handler would have to
close the file or release the socket. That would make it too easy to
forget to do cleanup and also lead to a lot of redundant code. To
address this problem Java offers the finally block. A finally block
encloses code that is always executed at some point after the try block
whether an exception was thrown or not. Even if there is a return
statement in the try block the finally block executes right after the
return statement is encountered and before the return executes!. If the
try block executes with no exceptions the finally block is executed
immediately after the try block completes. If there was an exception
thrown the finally block executes immediately after the proper catch
block completes.

 

finally clauses are not required. If you don't write one your code will
compile and run just fine. In fact if you have no resources to clean up
after your try block completes you probably don't need a finally clause.
Also because the compiler doesn't even require catch clauses sometimes
you'll run across code that has a try block immediately followed by a
finally block. Such code is useful when the exception is going to be
passed back to the calling method. Using a finally block allows the
cleanup code to execute even when there isn't a catch clause.

 

**Propagating Uncaught Exceptions**

 

the call stack is the chain of methods that your program executes to get
to the current method. If your program starts in method main() and
main() calls method a(), which calls method b(), which in turn calls
method c(), the call stack consists of the following:

c

b

a

main

The method at the very top of the stack trace would be the method you
were currently executing. If we move back down the call stack, we're
moving from the current method to the previously called method

 

You can keep throwing an exception down through the methods on the
stack. But what happens when you get to the main() method at the bottom?
You can throw the exception out of main() as well. This results in the
JVM halting and the stack trace will be printed to the output

 

**Defining Exceptions**

 

Every exception is an instance of a class that has class Exception in
its inheritance hierarchy. In other words, exceptions are always some
subclass of java.lang.Exception.

When an exception is thrown, an object of a particular Exception subtype
is instantiated and handed to the exception handler as an argument to
the catch clause.

 

All exception classes are subtypes of class Exception. This class
derives from the class Throwable (which derives from the class Object).

 

![](media/image3.png){width="6.0in" height="3.3854166666666665in"}

As you can see there are two subclasses that derive from Throwable:
**Exception and Error**. Classes that derive from Error represent
unusual situations that are not caused by program errors and indicate
things that would not normally happen during program execution such as
the JVM running out of memory. Generally your application won't be able
to recover from an Error so you're not required to handle them. If your
code does not handle them (and it usually won't) it will still compile
with no trouble. Although often thought of as exceptional conditions
Errors are technically not exceptions because they do not derive from
class Exception. In general, an exception represents something that
happens not as a result of a programming error, but rather because some
resource is not available or some other condition required for correct
execution is not present

 

printStackTrace() method prints the most recently entered method first
and continues down, printing the name of each method as it works its way
down the call stack (this is called "unwinding the stack")

 

When an exception is thrown Java will try to find (by looking at the
available catch clauses from the top down) a catch clause for the
exception type. If it doesn't find one it will search for a handler for
a supertype of the exception. If it does not find a catch clause that
matches a supertype for the exception then the exception is propagated
down the call stack. This process is called **"exception matching".**
The handlers for the most specific exceptions must always be placed
above those for more general exceptions. If one Exception class is not a
subtype or supertype of the other, then the order in which the catch
clauses are placed doesn't matter.

 

**Throws**

the exceptions that a method can throw must be declared (unless the
exceptions are subclasses of RuntimeException). The list of thrown
exceptions is part of a method's public interface. The throws keyword is
used as follows to list the exceptions that a method can throw.

 

Suppose your method doesn't directly throw an exception but calls a
method that does. You can choose not to handle the exception yourself
and instead just declare it as though it were your method that actually
throws the exception. If you do declare the exception that your method
might get from another method and you don't provide a try/catch for it
then the method will propagate back to the method that called your
method and will either be caught there or continue on to be handled by a
method further down the stack. Any method that might throw an exception
(unless it's a subclass of RuntimeException) must declare the exception.
That includes methods that aren't actually throwing it directly but are
"ducking" and letting the exception pass down to the next method in the
stack. If you "duck" an exception it is just as if you were the one
actually throwing the exception.

 

Each method must either handle all checked exceptions by supplying a
catch clause or list each unhandled checked exception as a thrown
exception.

An object of type RuntimeException may be thrown from any method without
being specified as part of the method's public interface (and a handler
need not be present). And even if a method does declare a
RuntimeException the calling method is under no obligation to handle or
declare it. RuntimeException Error and all of their subtypes are
unchecked exceptions and unchecked exceptions do not have to be
specified or handled

 

Runtime exceptions are referred to as unchecked exceptions. All other
exceptions are checked exceptions and they don't derive from
java.lang.RuntimeException. A checked exception must be caught somewhere
in your code. If you invoke a method that throws a checked exception but
you don't catch the checked exception somewhere your code will not
compile. That's why they're called checked exceptions: the compiler
checks to make sure that they're handled or declared

 

To create your own exception, you simply subclass Exception (or one of
its subclasses).

Just as you can throw a new exception from a catch clause, you can also
throw the same exception you just caught. All other catch clauses
associated with the same try are ignored; if a finally block exists, it
runs, and the exception is thrown back to the calling method (the next
method down the call stack).

 

If you throw a checked exception from a catch clause, you must also
declare that exception! In other words, you must handle and declare, as
opposed to handle or declare.

 

 

 

 

[**Checked and Unchecked Exceptions in
Java**](http://techblog.bozho.net/checked-and-unchecked-exceptions-in-java/)

 

Java has two types of exceptions – checked and unchecked. In short –
checked are meant for cases when the developer can reasonably recover
from the exception, while unchecked exceptions are programming errors
that can’t be dealt with

 

**Assertions**

assertions let you test your assumptions during development, without the
expense (in both your time and program overhead) of writing exception
handlers for exceptions that you assume will never happen once the
program is out of development and fully deployed. Assertions let you
test your assumptions during development but the assertion code
basically evaporates when the program is deployed leaving behind no
overhead or debugging code to track down and remove. Not only do
assertions let your code stay cleaner and tighter but because assertions
are inactive unless specifically "turned on" (enabled) the code will run
as though it were not present.

 

Assertions come in two flavors: really simple and simple, as follows:

Really simple:

private void doStuff() {

assert (y &gt; x);

// more code assuming y is greater than x

}

Simple:

private void doStuff() {

assert (y &gt; x): "y is " + y + " x is " + x;

// more code assuming y is greater than x

}

The difference between the two is that the simple version adds a second
expression separated from the first (boolean expression) by a colon—this
expression's string value is added to the stack trace. Both versions
throw an immediate AssertionError, but the simple version gives you a
little more debugging help,

 

You **enable assertions** at runtime with

java -ea com.geeksanonymous.TestClass

or

java -enableassertions com.geeksanonymous.TestClass

The preceding command-line switches tell the JVM to run with assertions
enabled.

 

You must also know the command-line switches for **disabling
assertions**:

java -da com.geeksanonymous.TestClass

or

java -disableassertions com.geeksanonymous.TestClass

 

The command-line switches for assertions can be used in various ways:

■ With no arguments (as in the preceding examples) Enables or disables
assertions in all classes, except for the system classes.

■ With a package name Enables or disables assertions in the package
specified and in any packages below this package in the same directory
hierarchy (more on that in a moment).

■ With a class name Enables or disables assertions in the class
specified.

 

 

you’re never supposed to handle an assertion failure. That means you
shouldn’t catch it with a catch clause and attempt to recover. Legally
however AssertionError is a subclass of Throwable so it can be caught.
But just don’t do it! If you’re going to try to recover from something
it should be an exception. To discourage you from trying to substitute
an assertion for an exception the AssertionError doesn’t provide access
to the object that generated it.

 

Java 7 made this nice and easy with a feature called **multi-catch**:

try {

// access the database and write to a file

} catch (SQLException | IOException e) {

handleErrorCase(e);

}

You can't use the variable name multiple times in a multi-catch. The
following won't compile:

catch(Exception1 e1 | Exception2 e2)

It makes sense that this example doesn't compile. After all, the code in
the exception handler needs to know which variable name to refer to.

catch(Exception1 e | Exception2 e)

 

With multi-catch, you have to make sure a given exception can only match
one type. multi-catch is only for exceptions in different inheritance
hierarchies.

catch(IOException | Exception e)

That's right. It won't compile because IOException is a subclass of
Exception. Which means it is redundant and the compiler won't accept it.

 

**try-with-resources**

 

Java 7 introduced a new feature called Automatic Resource Management
using "try-with-resources"

 

try (Reader reader = new BufferedReader(new FileReader(file))) { // note
the new syntax

// read from file

} catch (IOException e) { log(); throw e;}

No finally left at all! We don't even mention closing the reader.
Automatic Resource Management takes care of it for us. We start out by
declaring the reader inside the try declaration. The parentheses are
new. Think of them as a for loop in which we declare a loop index
variable that is scoped to just the loop. Here the reader is scoped to
just the try block. Not the catch block; just the try block.

 

The try-with-resources statement is logically calling a finally block to
close the reader. And just to make this even trickier, you can add your
own finally block to try-with-resources as well. Both will get called

 

Since the syntax is inspired from the for loop, we get to use a
semicolon when declaring multiple resources in the try. For example:

try (MyResource mr = MyResource.createResource(); // first resource

MyThingy mt = mr.createThingy()) { // second resource

// do stuff

}

 

Our declaration calls methods. Remember that the try-with-resources is
just Java code. It is just restricted to only be declarations. This
means if you want to do anything more than one statement long, you'll
need to put it into a method.

 

**AutoCloseable and Closeable**

 

Because Java is a statically typed language, it doesn't let you declare
just any type in a try-with-resources statement

 

AutoCloseable only has one method to implement. Let's take a look at the
simplest code we can write using this interface:

public class MyResource implements AutoCloseable {

public void close() {

// take care of closing the resource

}

}

There's also an interface called Closeable, which is similar to
AutoCloseable but with some key differences

Closeable allows implementors to throw only an IOException or a
RuntimeException. AutoCloseable allows any Exception at all to be
thrown.

For classes that implement AutoCloseable the implementation is required
to be idempotent. Which means you can call close() all day and nothing
will happen the second time and beyond. It will not attempt to close the
resource again and it will not blow up. For classes that implement
Closeable there is no such guarantee.

 

**Dates**

Calendar method you should know for the exam is the roll() method. The
roll() method acts like the add() method, except that when a part of a
Date gets incremented or decremented, larger parts of the Date will not
get incremented or decremented.

 

**Regex**

In general, a regex search runs from left to right, and once a source's
character has been used in a match, it cannot be reused.

 

■ \\d A digit (0–9)

\\D A non-digit (anything BUT 0–9)

■ \\s A whitespace character (e.g. space, \\t, \\n, \\f, \\r)

\\S A non-whitespace character

■ \\w A word character (letters (a–z and A–Z), digits, or the "\_"
\[underscore\])

\\W A non-word character (everything else)

■ \\b A word "boundary" (ends of the string and between \\w and not
\\w—more soon)

\\B A non-word "boundary" (between two \\w's or two not \\w's)

■ \[abc\] Searches only for a's, b's, or c's

■ \[a-f\] Searches only for a, b, c, d, e, or f characters

■ \[a-fA-F\] Searches for the first six letters of the alphabet, both
cases.

■ \* Zero or more occurrences

■ ? Zero or one occurrence

■ + One or more occurrences

 

The \^ is the negation symbol in regex

the "." (dot) metacharacter. When you see this character in a regex
expression, it means "any character can serve here."

 

You'll use the overloaded, static compile() method (which takes String
expression) to create an instance of Pattern. The find() method returns
true if it gets a match and remembers the start position of the match.
If find() returns true, you can call the start() method to get the
starting position of the match, and you can call the group() method to
get the string that represents the actual bit of source data that was
matched.

 

**Tokenizing with Scanner**

 

The java.util.Scanner class is the Cadillac of tokenizing. When you need
to do some serious tokenizing, look no further than Scanner—this beauty
has it all. In addition to the basic tokenizing capabilities provided by
String.split(), the Scanner class offers the following features:

■ Scanners can be constructed using files, streams, or strings as a
source.

■ Tokenizing is performed within a loop so that you can exit the process
at any point.

■ Tokens can be converted to their appropriate primitive types
automatically.

 

 

**Formatting with printf() and format()**

 

Behind the scenes, the format() method uses the java.util.Formatter
class to do the heavy formatting work

 

**File I/O**

 

**FileReader** :This class is used to read character files. Its read()
methods are fairly low-level, allowing you to read single characters,
the whole stream of characters, or a fixed number of characters.
FileReaders are usually wrapped by higher-level objects such as
BufferedReaders, which improve performance and provide more convenient
ways to work with the data.

**BufferedReader** This class is used to make lower-level Reader classes
like FileReader more efficient and easier to use. Compared to
FileReaders, BufferedReaders read relatively large chunks of data from a
file at once and keep this data in a buffer. When you ask for the next
character or line of data, it is retrieved from the buffer, which
minimizes the number of times that time-intensive, file-read operations
are performed

 

**Console** This new Java 6 convenience class provides methods to read
input from the console and write formatted output to the console. The
Console class makes it easy to accept input from the command line, both
echoed and nonechoed (such as a password), and makes it easy to write
formatted output to the command line.

On the input side the methods you'll have to understand are readLine and
readPassword. The readLine method returns a string containing whatever
the user keyed in—that's pretty intuitive. However the readPassword
method doesn't return a string; it returns a character array. Here's the
reason for this: Once you've got the password you can verify it and then
absolutely remove it from memory. If a string was returned it could
exist in a pool somewhere in memory and perhaps some nefarious hacker
could find it.

 

**flush() and close()**. When you write data out to a stream some amount
of buffering will occur and you never know for sure exactly when the
last of the data will actually be sent. You might perform many write
operations on a stream before closing it and invoking the flush() method
guarantees that the last of the data you thought you had already written
actually gets out to the file. Whenever you're done using a file either
reading it or writing to it you should invoke the close() method. When
you are doing file I/O you're using expensive and limited operating
system resources and so when you're done invoking close() will free up
those resources.

 

 

**OO and Design Patterns**

 

good OO design calls for loose coupling and shuns tight coupling, and
good OO design calls for high cohesion and shuns low cohesion. As with
most OO design discussions, the goals for an application are

■ Ease of creation

■ Ease of maintenance

■ Ease of enhancement

 

Coupling is the degree to which one class knows about another class. If
the only knowledge that class A has about class B is what class B has
exposed through its interface, then class A and class B are said to be
loosely coupled. If, on the other hand, class A relies on parts of class
B that are not part of class B's interface, then the coupling between
the classes is tighter

 

The term cohesion is used to indicate the degree to which a class has a
single, well-focused purpose. The more focused a class is, the higher
its cohesiveness.

The key benefit of high cohesion is that such classes are typically much
easier to maintain (and less frequently changed) than classes with low
cohesion. Another

benefit of high cohesion is that classes with a well-focused purpose
tend to be more reusable than other classes

 

**design pattern**

design pattern as "a general reusable solution to a commonly occurring
problem within a given context.

One "feature" of the above implementation is that it creates the Show
object before we need it. This is called eager initialization which is
good if the object isn't expensive to create or we know it will be
needed for every run of the program. Sometimes however we want to create
the object only on the first use. This is called lazy initialization

 

The singleton code here assumes you are only running one thread at a
time. It is NOT thread-safe. Think about if this were a web site and two
users managed to be booking a seat at the exact same time. If
getInstance() were running at the exact same time it would be possible
for both of them to see that INSTANCE was null and create a new Show at
the same time. There are a few ways to solve this. One is to add
synchronized to the getInstance() method. This works but comes with a
small performance hit

 

 

 

OCJP 3

Friday, January 29, 2016

16:34

 

**Generics and Collections**

 

Override **toString**() when you want a mere mortal to be able to read
something meaningful about the objects of your class. Code can call
toString() on your object when it wants to read useful details about
your object. When you pass an object reference to the
System.out.println() method for example the object's toString() method
is called

 

If you don't override a class's **equals**() method you won't be able to
use those objects as a key in a hashtable and you probably won't get
accurate Sets such that there are no conceptual duplicates

 

![](media/image4.png){width="6.0in" height="4.583333333333333in"}

Collections come in four basic flavors:

■ Lists Lists of things (classes that implement List)

■ Sets Unique things (classes that implement Set)

■ Maps Things with a unique ID (classes that implement Map)

■ Queues Things arranged by the order in which they are to be processed

 

An implementation class can be unsorted and unordered, ordered but
unsorted, or both ordered and sorted. But an implementation can never be
sorted but unordered

 

**Ordered** When a collection is ordered it means you can iterate
through the collection in a specific (not random) order. A Hashtable
collection is not ordered. Although the Hashtable itself has internal
logic to determine the order (based on hashcodes and the implementation
of the collection itself) you won't find any order when you iterate
through the Hashtable. An ArrayList however keeps the order established
by the elements' index position (just like an array). LinkedHashSet
keeps the order established by insertion so the last element inserted is
the last element in the LinkedHashSet (as opposed to an ArrayList where
you can insert an element at a specific index position). Finally there
are some collections that keep an order referred to as the natural order
of the elements and those collections are then not just ordered but also
sorted

 

**Sorted** A sorted collection means that the order in the collection is
determined according to some rule or rules known as the sort order. A
sort order has nothing to do with when an object was added to the
collection or when was the last time it was accessed or what "position"
it was added at. Sorting is done based on properties of the objects
themselves. You put objects into the collection and the collection will
figure out what order to put them in based on the sort order. A
collection that keeps an order (such as any List which uses insertion
order) is not really considered sorted unless it sorts using some kind
of sort order. Most commonly the sort order used is something called the
natural order.

 

**ArrayList** Think of this as a growable array. It gives you fast
iteration and fast random access. To state the obvious: It is an ordered
collection (by index), but not

sorted

 

**Vector:** A Vector is basically the same as an ArrayList, but Vector
methods are synchronized for thread safety. the synchronized methods add
a performance hit you might not need. And if you do need thread safety
there are utility methods in class Collections that can help. Vector is
the only class other than ArrayList to implement RandomAccess.

 

**LinkedList** A LinkedList is ordered by index position like ArrayList
except that the elements are doubly linked to one another. This linkage
gives you new methods (beyond what you get from the List interface) for
adding and removing from the beginning or end which makes it an easy
choice for implementing a stack or queue

 

**HashSet** A HashSet is an unsorted unordered Set. It uses the hashcode
of the object being inserted so the more efficient your hashCode()
implementation the better access performance you'll get. Use this class
when you want a collection with no duplicates and you don't care about
order when you iterate through it.

 

**LinkedHashSet** A LinkedHashSet is an ordered version of HashSet that
maintains a doubly linked List across all elements. Use this class
instead of HashSet when you care about the iteration order. When you
iterate through a HashSet the order is unpredictable while a
LinkedHashSet lets you iterate through the elements in the order in
which they were inserted

 

**TreeSet** The TreeSet is one of two sorted collections (the other
being TreeMap). It uses a Red-Black tree structure (but you knew that)
and guarantees that the elements will be in ascending order according to
natural order. Optionally you can construct a TreeSet with a constructor
that lets you give the collection your own rules for what the order
should be (rather than relying on the ordering defined by the elements'
class) by using a Comparator.

 

**HashMap** The HashMap gives you an unsorted unordered Map. When you
need a Map and you don't care about the order when you iterate through
it then HashMap is the way to go; the other maps add a little more
overhead. Where the keys land in the Map is based on the key's hashcode
so like HashSet the more efficient your hashCode() implementation the
better access performance you'll get

 

**Hashtable** Like Vector Hashtable has existed from prehistoric Java
times. For fun don't forget to note the naming inconsistency: HashMap
vs. Hashtable. Anyway just as Vector is a synchronized counterpart to
the sleeker more modern ArrayList Hashtable is the synchronized
counterpart to HashMap. Remember that you don't synchronize a class so
when we say that Vector and Hashtable are synchronized we just mean that
the key methods of the class are synchronized. Another difference though
is that while HashMap lets you have null values as well as one null key
a Hashtable doesn't let you have anything that's null.

 

**LinkedHashMap** Like its Set counterpart, LinkedHashSet, the
LinkedHashMap collection maintains insertion order (or, optionally,
access order). Although it will

be somewhat slower than HashMap for adding and removing elements, you
can expect faster iteration with a LinkedHashMap.

 

**TreeMap** You can probably guess by now that a TreeMap is a sorted
Map. And you already know that by default this means "sorted by the
natural order of the elements." Like TreeSet TreeMap lets you define a
custom sort order (via a Comparator) when you construct a TreeMap that
specifies how the elements should be compared to one another when
they're being ordered.

 

**PriorityQueue** This class is new as of Java 5. Since the LinkedList
class has been enhanced to implement the Queue interface basic queues
can be handled with a LinkedList. The purpose of a PriorityQueue is to
create a "priority-in priority out" queue as opposed to a typical FIFO
queue. A PriorityQueue's elements are ordered either by natural ordering
(in which case the elements that are sorted first will be accessed
first) or according to a Comparator. In either case the elements'
ordering represents their relative priority.

 

![](media/image5.png){width="6.0in" height="3.8645833333333335in"}

The **Comparable** interface is used by the Collections.sort() method
and the java.util.Arrays.sort() method to sort Lists and arrays of
objects, respectively. To implement Comparable, a class must implement a
single method, compareTo().

 

The **Comparator** interface gives you the capability to sort a given
collection any number of different ways. The other handy thing about the
Comparator interface is that you can use it to sort instances of any
class even classes you can't modify—unlike the Comparable interface,
which forces you to change the class whose instances you want to sort.
The Comparator interface is also very easy to implement, having only one
method, compare(). Here's a small class that can be used to sort a List
of DVDInfo instance

 

![](media/image6.png){width="5.958333333333333in" height="2.71875in"}

**Searching Arrays and Collections**

 

When searching through collections or arrays, the following rules apply:

■ Searches are performed using the binarySearch() method.

■ Successful searches return the int index of the element being
searched.

■ Unsuccessful searches return an int index that represents the
insertion point. The insertion point is the place in the
collection/array where the element would be inserted to keep the
collection/array properly sorted. Because positive return values and 0
indicate successful searches, the binarySearch() method uses negative
numbers to indicate insertion points. Since 0 is a valid result for a
successful search, the first available insertion point is -1. Therefore,
the actual insertion point is represented as (-(insertion point) -1).

■ The collection/array being searched must be sorted before you can
search it.

■ If you attempt to search an array or collection that has not already
been sorted, the results of the search will not be predictable.

■ If the collection/array you want to search was sorted in natural
order, it must be searched in natural order.

■ If the collection/array you want to search was sorted using a
Comparator, it must be searched using the same Comparator

 

The Arrays.asList() method copies an array into a List. The API says
"Returns a fixed-size list backed by the specified array. (Changes to
the returned list 'write through' to the array.)" When you use the
asList() method the array and the List become joined at the hip. ***When
you update one of them the other is updated automatically.***

 

***If you attempt to add an element to a set that already exists in the
set, the duplicate element will not be added, and the add() method will
return false***

 

 

The idea of polling is that we want both to retrieve and remove an
element from either the beginning or the end of a collection. In the
case of TreeSet,

pollFirst() returns and removes the first entry in the set, and
pollLast() returns and removes the last. Similarly, TreeMap now provides
pollFirstEntry() and pollLastEntry() to retrieve and remove key/value
pairs.

 

Unlike basic queue structures that are first-in first-out by default a
**PriorityQueue** orders its elements using a user-defined priority. The
priority can be as simple as natural ordering (in which for instance an
entry of 1 would be a higher priority than an entry of 2). In addition a
PriorityQueue can be ordered using a Comparator which lets you define
any ordering you want. Queues have a few methods not found in other
collection interfaces: peek() poll() and offer().

 

**Generics**

 

Arrays in Java have always been type-safe—an array declared as type
String (String \[\]) can't accept Integers (or ints), Dogs, or anything
other than Strings.

The biggest challenge for the Java engineers in adding generics to the
language (and the main reason it took them so long) was how to deal with
legacy code built without generics. The Java engineers obviously didn't
want to break everyone's existing Java code so they had to find a way
for Java classes with both type-safe (generic) and nontype-safe
(nongeneric/pre–Java 5) collections to still work together.

 

List&lt;Parent&gt; myList = new ArrayList&lt;Child&gt;();

No, it doesn't work. There's a very simple rule here—the type of the
variable declaration must match the type you pass to the actual object
type. If you declare

List&lt;Foo&gt; foo, then whatever you assign to the foo reference MUST
be of the generic type &lt;Foo&gt;. Not a subtype of &lt;Foo&gt;. Not a
supertype of &lt;Foo&gt;. Just &lt;Foo&gt;.

These are wrong:

List&lt;Object&gt; myList = new ArrayList&lt;JButton&gt;(); // NO!

List&lt;Number&gt; numbers = new ArrayList&lt;Integer&gt;(); // NO!

// remember that Integer is a subtype of Number

 

In other words, polymorphism applies here to only the "base" type. And
by "base," we mean the type of the collection class itself— the class
that can be customized with a type. In this code,

List&lt;JButton&gt; myList = new ArrayList&lt;JButton&gt;();

List and ArrayList are the base type and JButton is the generic type. So
an ArrayList can be assigned to a List, but a collection of
&lt;JButton&gt; cannot be assigned to a reference of &lt;Object&gt;,
even though JButton is a subtype of Object.

 

a method that takes, say, an ArrayList&lt;Animal&gt; will NOT be able to
accept a collection of any Animal subtype! That means
ArrayList&lt;Dog&gt; cannot be passed into a method with an argument of
ArrayList&lt;Animal&gt;, even though we already know that this works
just fine with plain old arrays.

 

***Why no polymorphism in Generics***

 

The reason it is dangerous to pass a collection (array or ArrayList) of
a subtype into a method that takes a collection of a supertype is
because you might add

something. And that means you might add the WRONG thing! This is
probably really obvious, but just in case (and to reinforce), let's walk
through some scenarios.

The first one is simple:

public void foo() {

Dog\[\] dogs = {new Dog(), new Dog()};

addAnimal(dogs); // no problem, send the Dog\[\] to the method

}

public void addAnimal(Animal\[\] animals) {

animals\[0\] = new Dog(); // ok, any Animal subtype works

}

 

This is no problem. We passed a Dog\[\] into the method and added a Dog
to the array (which was allowed since the method parameter was type
Animal\[\], which

can hold any Animal subtype). But what if we changed the calling code to

public void foo() {

Cat\[\] cats = {new Cat(), new Cat()};

addAnimal(cats); // no problem, send the Cat\[\] to the method

}

and the original method stays the same:

public void addAnimal(Animal\[\] animals) {

animals\[0\] = new Dog(); // Eeek! We just put a Dog

// in a Cat array!

}

The compiler thinks it is perfectly fine to add a Dog to an Animal\[\]
array, since a Dog can be assigned to an Animal reference. The problem
is that if you passed in an

array of an Animal subtype (Cat, Dog, or Bird), the compiler does not
know. The compiler does not realize that out on the heap somewhere is an
array of type Cat\[\],

not Animal\[\], and you're about to try to add a Dog to it. To the
compiler, you have passed in an array of type Animal, so it has no way
to recognize the problem.

THIS is the scenario we're trying to prevent, regardless of whether it's
an array or an ArrayList. The difference is that the compiler lets you
get away with it for

arrays, but not for generic collections.

 

The reason the compiler won't let you pass an ArrayList&lt;Dog&gt; into
a method that takes an ArrayList&lt;Animal&gt; is because within the
method, that parameter is of type

ArrayList&lt;Animal&gt;, and that means you could put any kind of Animal
into it. There would be no way for the compiler to stop you from putting
a Dog into a List that was originally declared as &lt;Cat&gt; but is now
referenced from the &lt;Animal&gt; parameter.

 

In other words, at runtime, the JVM KNOWS the type of arrays, but does
NOT know the type of a collection. All the generic type information is
removed during compilation

 

public void addAnimal(List&lt;? extends Animal&gt; animals)

By saying &lt;? extends Animal&gt;, we're saying, "I can be assigned a
collection that is a subtype of List and typed for &lt;Animal&gt; or
anything that extends Animal. But still we cannot add Dog to the list
inside the method.

 

**there is only ONE wildcard keyword that represents both interface
implementations and subclasses. And that keyword is extends.**

 

However, there is another scenario where you can use a wildcard AND
still add to the collection, but in a safe way—the keyword super

public void addAnimal(List&lt;? super Dog&gt; animals)

 

There IS a huge difference. List&lt;?&gt;, which is the wildcard
&lt;?&gt; without the keywords extends or super, simply means "any
type." So that means any type of List can be assigned to the argument.
That could be a List of &lt;Dog&gt;, &lt;Integer&gt;, &lt;JButton&gt;,
&lt;Socket&gt;, whatever. And using the wildcard alone, without the
keyword super (followed by a type), means that you cannot ADD anything
to the list referred to as List&lt;?&gt;

 

List&lt;Object&gt; is completely different from List&lt;?&gt;.
List&lt;Object&gt; means that the method can take ONLY a
List&lt;Object&gt;. Not a List&lt;Dog&gt; or a List&lt;Cat&gt;. It does,
however, mean that you can add to the list, since the compiler has
already made certain that you're passing only a valid List&lt;Object&gt;
into the method

 

 

the API tells you when a parameterized type is expected. For example,
this is the API declaration for thejava.util.List interface:

public interface List&lt;E&gt;

The &lt;E&gt; is a placeholder for the type you pass in. The List
interface is behaving as a generic "template" (sort of like C++
templates), and when you write your code,

you change it from a generic List to a List&lt;Dog&gt; or
List&lt;Integer&gt;, and so on.

The E, by the way, is only a convention. Any valid Java identifier would
work here, but E stands for "Element," and it's used when the template
is a collection. The

other main convention is T (stands for "type"), used for, well, things
that are NOT collections

Now that you've seen the interface declaration for List, what do you
think the add() method looks like?

boolean add(E o)

In other words, whatever E is when you declare the List, that's what you
can add to it

 

 

Imagine you want to create a method that takes an instance of any type,
instantiates an ArrayList of that type, and adds the instance to the
ArrayList. The class itself doesn't need to be generic; basically, we
just want a utility method that we can pass a type to and that can use
that type to construct a type-safe collection. Using a generic method,
we can declare the method without a specific type and then get the type
information based on the type of the object passed to the method.

 

import java.util.\*;

public class CreateAnArrayList {

public &lt;T&gt; void makeArrayList(T t) { // take an object of an

// unknown type and use a

// "T" to represent the type

List&lt;T&gt; list = new ArrayList&lt;T&gt;(); // now we can create the

// list using "T"

list.add(t);

}

}

In the preceding code, if you invoke the makeArrayList() method with a
Dog instance, the method will behave as though it looked like this all
along:

public void makeArrayList(Dog t) {

List&lt;Dog&gt; list = new ArrayList&lt;Dog&gt;();

list.add(t);

}

 

The strangest thing about generic methods is that you must declare the
type variable BEFORE the return type of the method. The &lt;T&gt; before
void simply defines what T is before you use it as a type in the
argument. You MUST declare the type like that unless the type is
specified for the class

 

***Inner classes ***

Inner classes let you define one class within another. They provide a
type of scoping for your classes, since you can make one class a member
of another class. Just

as classes have member variables and methods, a class can also have
member classes

one of the key benefits of an inner class is the "special relationship"
an inner class instance shares with an instance of the outer class. That
"special relationship" gives code in the inner class access to members
of the enclosing (outer) class, as if the inner class were part of the
outer class. In fact, that's exactly what it means: The inner class is a
part of the outer class. Not just a "part," but a full-fledged,
card-carrying member of the outer class. Yes, an inner class instance
has access to all members of the outer class, even those marked private.

 

a regular inner class cannot have static declarations of any kind. The
only way you can access the inner class is through a live instance of
the outer class! In other words, only at runtime, when there's already
an instance of the outer class to tie the inner class instance to

 

To create an instance of an inner class, you must have an instance of
the outer class to tie to the inner class. There are no exceptions to
this rule: An inner class instance can never stand alone without a
direct relationship to an instance of the outer class.

 

Within an inner class code, the this reference refers to the instance of
the inner class, as you'd probably expect, since this always refers to
the currently executing

object. But what if the inner class code wants an explicit reference to
the outer class instance that the inner instance is tied to? In other
words, how do you reference the "outer this"? To reference the "outer
this" (the outer class instance) from within the inner class code, use
NameOfOuterClass.this

 

A method-local inner class can be instantiated only within the method
where the inner class is defined. In other words, no other code running
in any other method—inside or outside the outer class—can ever
instantiate the method-local inner class. Like regular inner class
objects, the method-local inner class object shares a special
relationship with the enclosing (outer) class object and can access its
private (or any other) members. However, the inner class object cannot
use the local variables of the method the inner class is in. Think about
it. The local variables of the method live on the stack and exist only
for the lifetime of the method. You already know that the scope of a
local variable is limited to the method the variable is declared in.
When the method ends, the stack frame is blown away and the variable is
history. But even after the method completes, the inner class object
created within it might still be alive on the heap if, for example, a
reference to it was passed into some other code and then stored in an
instance variable. Because the local variables aren't guaranteed to be
alive as long as the method-local inner class object is, the inner class
object can't use them. Unless the local variables are marked final!

 

 

 

 

OCJP 4

Friday, January 29, 2016

19:05

 

**Threads**

 

An instance of Thread is just… an object. Like any other object in Java,
it has variables and methods, and lives and dies on the heap. But a
thread of execution is an individual process (a "lightweight" process)
that has its own call stack. In Java, there is one thread per call
stack—or, to think of it in reverse, one call stack per thread.

The main() method, which starts the whole ball rolling, runs in one
thread, called (surprisingly) the main thread .main() is the first
method on the stack—the method at the bottom. But as soon as you create
a new thread, a new stack materializes and methods called from that
thread run in a call stack that's separate from the main() call stack.
That second new call stack is said to run concurrently with the main
thread

 

always write the code that needs to be run in a separate thread in a
run() method. The run() method will call other methods, of course, but
the thread of execution—the new call stack—always begins by invoking
run().

 

You can define and instantiate a thread in one of two ways:

■ Extend the java.lang.Thread class.

■ Implement the Runnable interface.

 

you're free to overload the run() method in your Thread subclass. The
overloaded run(String s) method will be ignored by the Thread class
unless you call it yourself. The Thread class expects a run() method
with no arguments and it will execute this method for you in a separate
call stack after the thread has been started. With a run(String s)
method the Thread class won't call the method for you and even if you
call the method directly yourself execution won't happen in a new thread
of execution with a separate call stack. It will just happen in the same
call stack as the code that you made the call from just like any other
normal method call.

 

If you extended the Thread class, instantiation is dead simple (we'll
look at some additional overloaded constructors in a moment):

MyThread t = new MyThread();

If you implement Runnable instantiation is only slightly less simple. To
have code run by a separate thread you still need a Thread instance. But
rather than combining both the thread and the job (the code in the
run()method) into one class you've split it into two classes—the Thread
class for the thread-specific code and your Runnable implementation
class for your job-that-should-be-run-by-a-thread code. (Another common
way to think about this is that the Thread is the "worker " and the
Runnable is the "job" to be done.)

First you instantiate your Runnable class:

MyRunnable r = new MyRunnable();

Next, you get yourself an instance of java.lang.Thread (somebody has to
run your job…), and you give it your job!

Thread t = new Thread(r); // Pass your Runnable to the Thread

If you create a thread using the no-arg constructor, the thread will
call its own run() method when it's time to start working

You can pass a single Runnable instance to multiple Thread objects so
that the same Runnable becomes the target of multiple threads

 

When a thread has been instantiated but not started (in other words the
start() method has not been invoked on the Thread instance) the thread
is said to be in the new state. At this stage the thread is not yet
considered alive. Once the start() method is called the thread is
considered alive (even though the run() method may not have actually
started executing yet). A thread is considered dead (no longer alive)
after the run() method completes. The isAlive() method is the best way
to determine if a thread has been started but has not yet completed its
run() method

 

So what happens after you call start()?

■ A new thread of execution starts (with a new call stack).

■ The thread moves from the new state to the runnable state.

■ When the thread gets a chance to execute, its target run() method will
run.

Be sure you remember the following: You start a Thread, not a Runnable.
You call start() on a Thread instance, not on a Runnable instance

 

A thread is done being a thread when its target run() method completes.
When a thread completes its run() method, the thread ceases to be a
thread of execution. The stack for that thread dissolves, and the thread
is considered dead

 

Once a thread has been started, it can never be started again. If you
have a reference to a Thread and you call start(), it's started. If you
call start() a second time, it will cause an exception (an
IllegalThreadStateException, which is a kind of RuntimeException,

 

*The Thread Scheduler *

The thread scheduler is the part of the JVM (although most JVMs map Java
threads directly to native threads on the underlying OS) that decides
which thread should run at any given moment and also takes threads out
of the run state. Assuming a single processor machine only one thread
can actually run at a time. Only one stack can ever be executing at one
time. And it's the thread scheduler that decides which thread—of all
that are eligible—will actually run. When we say eligible we really mean
in the runnable state. Any thread in the runnable state can be chosen by
the scheduler to be the one and only running thread. If a thread is not
in a runnable state then it cannot be chosen to be the currently running
thread.

 

*The order in which runnable threads are chosen to run is not
guaranteed.*

Although we don't control the thread scheduler (we can't, for example,
tell a specific thread to run), we can sometimes influence it.

Thread Class: sleep() yield() join() setpriority()

Object Class : wait() notify() notifyAll()

 

*States of thread*

 

■ New This is the state the thread is in after the Thread instance has
been created but the start() method has not been invoked on the thread.
It is a live Thread object, but not yet a thread of execution. At this
point, the thread is considered not alive.

 

■ Runnable This is the state a thread is in when it's eligible to run
but the scheduler has not selected it to be the running thread. A thread
first enters the runnable state when the start() method is invoked, but
a thread can also return to the runnable state after either running or
coming back from a blocked, waiting, or sleeping state. When the thread
is in the runnable state, it is considered alive.

 

■ Running This is it. The "big time." Where the action is. This is the
state a thread is in when the thread scheduler selects it from the
runnable pool to be the currently executing process. A thread can
transition out of a running state for several reasons, including because
"the thread scheduler felt like it. There are several ways to get to the
runnable state, but only one way to get to the running state: The
scheduler chooses a thread from the runnable pool.

 

■ Waiting/blocked/sleeping This is the state a thread is in when it's
not eligible to run. The thread is still alive, but is currently not
eligible to run. In other words, it is not runnable, but it might return
to a runnable state later if a particular event occurs

The important point is that one thread does not tell another thread to
block. Some methods may look like they tell another thread to block, but
they don't.

t.sleep(); or t.yield();

But those are actually static methods of the Thread class—they don't
affect the instance t; instead, they are defined to always affect the
thread that's currently executing

 

■ Dead A thread is considered dead when its run() method completes. It
may still be a viable Thread object, but it is no longer a separate
thread of execution. Once a thread is dead, it can never be brought back
to life!

 

 

![](media/image7.png){width="4.260416666666667in" height="1.875in"}

Just because a thread's sleep() expires and it wakes up this does not
mean it will return to running! Remember when a thread wakes up it
simply goes back to the runnable state. So the time specifi ed in
sleep() is the minimum duration in which the thread won't run but it is
not the exact duration in which the thread won't run. So you can't for
example rely on the sleep() method to give you a perfectly accurate
timer. Although in many applications using sleep() as a timer is
certainly good enough you must know that a sleep() time is not a
guarantee that the thread will start running again as soon as the time
expires and the thread wakes

 

In most JVMs however the scheduler does use thread priorities in one
important way: If a thread enters the runnable state and it has a higher
priority than any of the threads in the pool and a higher priority than
the currently running thread the lower-priority running thread usually
will be bumped back to runnable and the highestpriority thread will be
chosen to run. In other words at any given time the currently running
thread usually will not have a priority that is lower than any of the
threads in the pool. In most cases the running thread will be of equal
or greater priority than the highest-priority threads in the pool.

 

What yield() is supposed to do is make the currently running thread head
back to runnable to allow other threads of the same priority to get
their turn. So the intention is to use yield() to promote graceful
turn-taking among equal-priority threads. In reality though the yield()
method isn't guaranteed to do what it claims and even if yield() does
cause a thread to step out of running and back to runnable there's no
guarantee the yielding thread won't just be chosen again over all the
others!

 

The join( ) Method

The non-static join() method of class Thread lets one thread "join onto
the end" of another thread. If you have a thread B that can't do its
work until another thread A has completed its work, then you want thread
B to "join" thread A. This means that thread B will not become runnable
until A has finished (and entered the dead state).

 

 

**Synchronization and Locks**

 

How does synchronization work? With locks. Every object in Java has a
built-in lock that only comes into play when the object has synchronized
method code. When we enter a synchronized non-static method we
automatically acquire the lock associated with the current instance of
the class whose code we're executing (the this instance). Acquiring a
lock for an object is also known as getting the lock or locking the
object locking on the object or synchronizing on the object. We may also
use the term monitor to refer to the object whose lock we're acquiring

 

Since there is only one lock per object if one thread has picked up the
lock no other thread can pick up the lock until the first thread
releases (or returns) the lock. This means no other thread can enter the
synchronized code (which means it can't enter any synchronized method of
that object) until the lock has been released. Typically releasing a
lock means the thread holding the lock (in other words the thread
currently in the synchronized method) exits the synchronized method. At
that point the lock is free until some other thread enters a
synchronized method on that object

 

■ Only methods (or blocks) can be synchronized, not variables or
classes.

■ Each object has just one lock.

■ Not all methods in a class need to be synchronized. A class can have
both synchronized and non-synchronized methods.

■ If a class has both synchronized and non-synchronized methods,
multiple threads can still access the class's non-synchronized methods!

■ If a thread goes to sleep, it holds any locks it has—it doesn't
release them.

■ A thread can acquire more than one lock. For example, a thread can
enter a synchronized method, thus acquiring a lock, and then immediately
invoke a synchronized method on a different object, thus acquiring that
lock as well. As the stack unwinds, locks are released again. Also, if a
thread acquires a lock and then attempts to call a synchronized method
on that same object, no problem. The JVM knows that this thread already
has the lock for this object, so the thread is free to call other
synchronized methods on the same object, using the lock the thread
already has.

■ You can synchronize a block of code rather than a method.

 

When you synchronize a method the object used to invoke the method is
the object whose lock must be acquired. But when you synchronize a block
of code you specify which object's lock you want to use as the lock so
you could for example use some third-party object as the lock for this
piece of code. That gives you the ability to have more than one lock for
code synchronization within a single object.

Or you can synchronize on the current instance (this) as in the previous
code. Since that's the same instance that synchronized methods lock on
it means that you could always replace a synchronized method with a
non-synchronized method containing a synchronized block.

 

**static methods can be synchronized.** There is only one copy of the
static data you're trying to protect so you only need one lock per class
to synchronize static methods—a lock for the whole class. There is such
a lock; every class loaded in Java has a corresponding instance of
java.lang.Class representing that class. It's that java.lang.Class
instance whose lock is used to protect the static methods of the class
(if they're synchronized).

 

If a thread tries to enter a synchronized method and the lock is already
taken the thread is said to be blocked on the object's lock. Essentially
the thread goes into a kind of pool for that particular object and has
to sit there until the lock is released and the thread can again become
runnable/running. Just because a lock is released doesn't mean any
particular thread will get it. There might be three threads waiting for
a single lock for example and there's no guarantee that the thread that
has waited the longest will get the lock first.

 

■ Threads calling non-static synchronized methods in the same class will
only block each other if they're invoked using the same instance. That's
because they each lock on this instance, and if they're called using two
different instances, they get two locks, which do not interfere with
each other.

■ Threads calling static synchronized methods in the same class will
always block each other—they all lock on the same Class instance.

 

You don't need to worry about local variables— each thread gets its own
copy of a local variable. Two threads executing the same method at the
same time will use different copies of the local variables and they
won't bother each other. However you do need to worry about static and
nonstatic fields if they contain data that can be changed.

 

When a class has been carefully synchronized to protect its data (using
the rules just given or using more complicated alternatives), we say the
class is "**thread-safe**"

For example StringBuffer and StringBuilder are nearly identical classes
except that all the methods in StringBuffer are synchronized when
necessary while those in StringBuilder are not. Generally this makes
StringBuffer safe to use in a multithreaded environment while
StringBuilder is not.

 

The thing to realize here is that in a "thread-safe" class like the one
returned by synchronizedList() each individual method is synchronized.
So names.size() is synchronized and names.remove(0) is synchronized. But
nothing prevents another thread from doing something else to the list in
between those two calls.

 

**Deadlock** occurs when two threads are blocked, with each waiting for
the other's lock. Neither can run until the other gives up its lock, so
they'll sit there forever.

 

threads can interact with one another to communicate about—among other
things—their locking status. The Object class has three methods wait()
notify() and notifyAll() that help threads communicate the status of an
event that the threads care about

wait(), notify(), and notifyAll() must be called from within a
synchronized context! A thread can't invoke a wait or notify method on
an object unless it owns that object's lock

 

 

**Concurrency**

The java.util.concurrent package provides high-level APIs that support
many common concurrent programming use cases.

 

java.util.concurrent.atomic package provide variables whose values can
be modified atomically. An atomic operation is one that, for all intents
and purposes, appears to happen all at once. The
java.util.concurrent.atomic package provides several classes for
different data types, such as AtomicInteger , AtomicLong , AtomicBoolean
, and AtomicReference etc.

 

The reason this implementation is now thread-safe is something called
CAS. CAS stands for Compare And Swap. Most modern CPUs have a set of CAS
instructions. A basic outline of what is happening now is as follows:

1\. The value stored in count is copied to a temporary variable.

2\. The temporary variable is incremented.

3\. Compare the value currently in count with the original value. If it
is unchanged, then swap the old value for the new value.

Step 3 happens atomically. If step 3 finds that some other thread has
already

modified the value of count , then repeat steps 1–3 until we increment
the field without interference. The central method in a class like
AtomicInteger is the boolean compareAndSet(int expect, int update)
method, which provides the CAS behavior. Other atomic methods delegate
to the compareAndSet method.

 

So why would you use these newer locking classes? The
java.util.concurrent.locks package provides

■ The ability to duplicate traditional synchronized blocks.

■ Nonblock scoped locking—obtain a lock in one method and release it in
another (this can be dangerous, though).

■ Multiple wait / notify / notifyAll pools per lock—threads can select
which pool ( Condition ) they wait on.

■ The ability to attempt to acquire a lock and take an alternative
action if locking fails.

■ An implementation of a multiple-reader, single-writer lock.

 

The java.util.concurrent.locks.Lock interface provides the outline of
the new form of locking provided by the java.util.concurrent.locks
package. Like any interface, the Lock interface requires an
implementation to be of any real use. The
java.util.concurrent.locks.**ReentrantLock** class provides that
implementation

 

Lock lock = new ReentrantLock();

lock.lock();

// blocks until acquired

try {

// do work here

} finally {

// to ensure we unlock

lock.unlock();

// must manually release

}

It is recommended that you always follow the lock() method with a try -
finally block, which releases the lock.One of the very powerful features
is the ability to attempt (and fail) to acquire a lock. With traditional
synchronization, once you hit a synchronized block, your thread either
immediately acquires the lock or blocks until it can.

 

Lock lock = new ReentrantLock();

boolean locked = lock.tryLock(); // try without waiting

if (locked) {

try {

// work

} finally {

// to ensure we unlock

lock.unlock();

}

}

 

 

 

The ability to quickly fail to acquire the lock turns out to be
powerful. You can process a different resource (lock) and come back to
the failed lock later instead of just waiting for a lock to be released
and thereby making more efficient use of system resources. There is also
a variation of the tryLock method that allows you to specify an amount
of time you are willing to wait to acquire the lock:

 

 

Lock lock = new ReentrantLock();

try {

boolean locked = lock.tryLock(3, TimeUnit.SECONDS);

if (locked) {

try {

// work

} finally {

// to ensure we unlock

lock.unlock();

}

}

} catch (InterruptedException ex) {

// handle

}

 

 

Another benefit of the tryLock method is **deadlock avoidance**. With
traditional synchronization, you must acquire locks in the same order
across all threads. A ReentrantLock has an internal counter that keeps
track of the number of times it has been locked/unlocked, and it is an
error to unlock without a corresponding successful lock operation. If a
thread attempts to release a

lock that it does not own, an IllegalMonitorStateException will be
thrown With traditional locking, using synchronized code blocks and
attempting to obtain locks in the reverse order could lead to deadlock.

 

It is remotely possible that this example could lead to **livelock**.
Imagine if thread A always acquires lock1 at the same time that thread B
acquires lock2 . Each thread's attempt to acquire the second lock would
always fail, and you'd end up repeating forever, or at least until you
were lucky enough to have one thread fall behind the other. You can
avoid livelock in this scenario

by introducing a short random delay with Thread.sleep(int) any time you
fail to acquire both locks

 

A **Condition** provides the equivalent of the traditional wait , notify
, and notifyAll methods. The traditional wait and notify methods allow
developers to implement an await/signal pattern. You use an await/signal
pattern when you would use locking, but with the added stipulation of
trying to avoid spinning (endless checking if it is okay to do
something). The java.util.concurrent.locks.Condition interface is the
modern replacement for the wait and notify methods.

 

Lock lock = new ReentrantLock();

Condition blockingPoolA = lock.newCondition();

 

When your thread reaches a point where it must delay until another
thread performs an activity, you "await" the completion of that other
activity. Before calling await , you must have locked the Lock used to
produce the Condition . It is possible that the awaiting thread may be
interrupted and you must handle the possible InterruptedException . When
you call the await method, the Lock associated with the Condition is
released. Before the await method returns, the lock will be reacquired.
In order to use a Condition , a thread must first acquire a Lock .

 

 

lock.lock();

try {

blockingPoolA.await(); // "wait" here

// lock will be reacquired

// work

} catch (InterruptedException ex) {

// interrupted during await()

} finally {

// to ensure we unlock

lock.unlock();

// must manually release

}

 

In another thread, you perform the activity that the first thread was
waiting on and then signal that first thread to resume (return from the
await method)

 

lock.lock();

try {

// work

blockingPoolA.signalAll(); // wake all awaiting

// threads

} finally {

lock.unlock();

// now an awoken thread can run

}

 

The signalAll() method causes all threads awaiting on the same Condition
to wake up. You can also use the signal() method to wake up a single
awaiting thread. Remember that "waking up" is not the same thing as
proceeding. Each awoken thread will have to reacquire the Lock before
continuing.

 

One advantage of a Condition over the traditional wait/notify operations
is that multiple Condition s can exist for each Lock . A Condition is
effectively a waiting/ blocking pool for threads.

 

Lock lock = new ReentrantLock();

Condition blockingPoolA = lock.newCondition();

Condition blockingPoolB = lock.newCondition();

 

By having multiple conditions, you are effectively categorizing the
threads waiting on a lock and can, therefore, wake up a subset of the
waiting threads. Conditions can also be used when you can't use a
BlockingQueue to coordinate the activities of two or more threads.

 

To allow multiple threads to concurrently read the high score list or
allow a single thread to add a new score, you could use a
**ReadWriteLock** .A ReentrantReadWriteLock is not actually a Lock ; it
implements the ReadWriteLock interface. What a ReentrantReadWriteLock
does is produce two specialized Lock instances, one to a read lock and
the other to a write lock.

 

ReentrantReadWriteLock rwl =

new ReentrantReadWriteLock();

Lock readLock = rwl.readLock();

Lock writeLock = rwl.writeLock();

 

These two locks are a matched set—one cannot be held at the same time as
the other (by different threads). What makes these locks unique is that
multiple threads can hold the read lock at the same time, but only one
thread can hold the write lock at a time.This example shows how a
non-thread-safe collection (an ArrayList ) can be made thread-safe,
allowing concurrent reads but exclusive access by a writing thread:

 

 

public class MaxValueCollection {

private List&lt;Integer&gt; integers = new ArrayList&lt;&gt;();

private ReentrantReadWriteLock rwl =

new ReentrantReadWriteLock();

public void add(Integer i) {

rwl.writeLock().lock(); // one at a time

try {

integers.add(i);

} finally {

rwl.writeLock().unlock();

}

}

public int findMax() {

rwl.readLock().lock(); // many at once

try {

return Collections.max(integers);

} finally {

rwl.readLock().unlock();

}

}

}

 

 

**Concurrent Collections**

A traditional java.util.List implementation such as java.util.ArrayList
is not thread-safe. Concurrent threads can safely read from an ArrayList
and possibly even modify the elements stored in the list, but if any
thread modifies the structure of the list (add or remove operation),
then unpredictable behavior can occur.

 

To make a collection thread-safe, you could surround all the code that
accessed the collection in synchronized blocks or use a method such as
Collections. synchronizedList(new ArrayList()) . Using synchronization
to safeguard a collection creates a performance bottleneck and reduces
the liveness of your application. The java.util.concurrent package
provides several types of

collections that are thread-safe but do not use coarse-grained
synchronization

 

The **copy-on-write collections** from the java.util.concurrent package
implement one of several mechanisms to make a collection thread-safe. By
using the copy-on-write collections, you eliminate the need to implement
synchronization or locking when manipulating a collection using multiple
threads. The CopyOnWriteArrayList is a List implementation that can be
used

concurrently without using traditional synchronization semantics. As its
name implies, a CopyOnWriteArrayList will never modify its internal
array of data. Any mutating operations on the List (add, set, remove,
etc.) will cause a new modified copy of the array to be created, which
will replace the original read-only array. The read-only nature of the
underlying array in a CopyOnWriteArrayList allows it to be safely shared
with multiple threads. Remember that read-only (immutable) objects are
always thread-safe.

 

The essential thing to remember with a copy-on-write collection is that
a thread that is looping through the elements in a collection must keep
a reference to the same unchanging elements throughout the duration of
the loop; this is achieved with the use of an Iterator . Basically, you
want to keep using the old, unchanging collection that you began a loop
with. When you use list.iterator() , the returned Iterator will always
reference the collection of elements as it was when list.iterator() was
called, even if another thread modifies the collection. Any mutating
methods called on a copy-on-write–based Iterator or ListIterator (such
as add, set, or remove) will throw an UnsupportedOperationException . A
for-each loop uses an Iterator when executing, so it is safe to use with
a copy-on-write collection, unlike a traditional for loop.

** **

** **

The java.util.concurrent package provides two copy-on-write–based
collections: **CopyOnWriteArrayList and CopyOnWriteArraySet** . Use the
copy-on-write collections when your data sets remain relatively small
and the number of read operations and traversals greatly outnumber
modifications to the collections. Modifications to the collections (not
the elements within)

are expensive because the entire internal array must be duplicated for
each modification

 

A thread-safe collection does not make the elements stored within the
collection thread-safe. Just because a collection that contains elements
is thread-safe does not mean the elements themselves can be safely
modifi ed by multiple threads. You might have to use atomic variables,
locks, synchronized code blocks, or immutable (read- only) objects to
make the objects referenced by a collection thread-safe.

 

**Concurrent Collections**

** **

The concurrent collections include

■ ConcurrentHashMap

■ ConcurrentLinkedDeque

■ ConcurrentLinkedQueue

■ ConcurrentSkipListMap

■ ConcurrentSkipListSet

 

Be aware that an Iterator for a concurrent collection is weakly
consistent; it can return elements from the point in time the Iterator
was created or later. This means that while you are looping through a
concurrent collection, you might observe elements that are being
inserted by other threads. In addition, you may observe only some of the
elements that another thread is inserting with methods such as addAll
when concurrently reading from the collection. Similarly, the size
method may produce inaccurate results. Imagine attempting to count the
number of people in a checkout line at a grocery store. While you are
counting the people in line, some people may join the line and others
may leave. Your count might end up close but not exact by the time you
reach the end. This is the type of behavior you might see with a weakly
consistent collection. The benefit to this type of behavior is that it
is permissible for multiple threads to concurrently read and write a
collection without having to create multiple internal copies of the
collection, as is the case in a copy-on-write collection. If your
application cannot deal with these inconsistencies, you might have to
use a copy-on-write collection

 

The ConcurrentHashMap and ConcurrentSkipListMap classes implement the
ConcurrentMap interface. A ConcurrentMap enhances a Map by adding the
atomic putIfAbsent , remove , and replace methods. For example, the
putIfAbsent method is equivalent to performing the following code as an
atomic operation:

 

if (!map.containsKey(key))

return map.put(key, value);

else

return map.get(key);

 

ConcurrentSkipListMap and ConcurrentSkipListSet are sorted.

ConcurrentSkipListMap keys and ConcurrentSkipListSet elements require
the use of the Comparable or Comparator interfaces to enable ordering.

 

**Blocking Queues**

** **

The copy-on-write and the concurrent collections are centered on the
idea of multiple threads sharing data. Sometimes, instead of shared data
(objects), you need to transfer data between two threads. A
BlockingQueue is a type of shared collection that is used to exchange
data between two or more threads while causing one or more of the
threads to wait until the point in time when the data can be exchanged.
One use case of a BlockingQueue is called the producer-consumer problem.
In a producer-consumer scenario, one thread produces data, then adds it
to a queue, and another thread must consume the data from the queue. A
queue provides the means for the producer and the consumer to exchange
objects. The java.util.concurrent package provides several BlockingQueue
implementations. They include

■ ArrayBlockingQueue

■ LinkedBlockingDeque

■ LinkedBlockingQueue

■ PriorityBlockingQueue

■ DelayQueue

■ LinkedTransferQueue

■ SynchronousQueue

 

A blocking collection, depending on the method being called, may cause a
thread to block until another thread calls a corresponding method on the
collection. For example, if you attempt to remove an element by calling
take() on any BlockingQueue that is empty, the operation will block
until another thread inserts an element. Do n't call a blocking
operation in a thread unless it is safe for that thread to block.

 

**add(E e)** Insert an object. Returns true if object added, false if
duplicate objects are not allowed. Throws an IllegalStateException if
the queue is bounded and full. **offer(E e)** Insert an object. Returns
true if object added, false if the queue is bounded and full. **put(E
e)** Insert an object. Returns void . If needed, will block until space
in the queue becomes available. **offer(E e, long timeout, TimeUnit
unit)** Insert an object. Returns false if the object was not able to be
inserted before the time indicated by the second and third parameters.
**remove(Object o)** Remove an object. Returns true if an equal object
was found in the queue and removed; otherwise, returns false .
**poll(long timeout, Remove an object. TimeUnit unit)** Removes the
first object in the queue (the head) and returns it. If the timeout
expires before an object can be removed because the queue is empty, a
null will be returned. **take()** Remove an object. Removes the first
object in the queue (the head) and returns it, blocking if needed until
an object becomes available. **poll()** Remove an object. Removes the
first object in the queue (the head) and returns it or returns null if
the queue is empty. **element()** Retrieves an object. Gets the head of
the queue without removing it. Throws a NoSuchElementException if the
queue is empty. **peek()**Retrieves an object. Gets the head of the
queue without removing it. Returns a null if the queue is empty.

 

 

ArrayBlockingQueue , LinkedBlockingDeque , and LinkedBlockingQueue

support a **bounded** capacity and will block on put(e) and similar
operations if the collection is full. LinkedBlockingQueue is optionally
bounded, depending on the constructor you use.

BlockingQueue&lt;Integer&gt; bq = new ArrayBlockingQueue&lt;&gt;(1);

try {

bq.put(42);

bq.put(43); // blocks until previous value is removed

} catch (InterruptedException ex) {

// log and handle

}

 

A **SynchronousQueue** is a special type of bounded blocking queue; it
has a capacity of zero. Having a zero capacity, the first thread to
attempt either an insert or remove operation on a SynchronousQueue will
block until another thread performs the opposite operation. You use a
SynchronousQueue when you need threads to meet up and exchange an
object.

 

A **DelayQueue** is useful when you have objects that should not be
consumed until a specific time. The elements added to a DelayQueue will
implement the java.util.concurrent.Delayed interface which defines a
single method: public long getDelay(TimeUnit unit) . The elements of a
DelayQueue can only be taken once their delay has expired

 

A **LinkedTransferQueue** (new to Java 7) is a superset of
ConcurrentLinkedQueue , SynchronousQueue , and LinkedBlockingQueue . It
can function as a concurrent Queue implementation similar to
ConcurrentLinkedQueue . It also supports unbounded blocking (consumption
blocking) similar to LinkedBlockingQueue via the take() method. Like a
SynchronousQueue , a LinkedTransferQueue can be used to make two threads
rendezvous to exchange an object. Unlike a SynchronousQueue , a
LinkedTransferQueue has internal capacity, so the transfer(E) method is
used to block until the inserted object (and any previously inserted
objects) is consumed by another thread. In other words, a
LinkedTransferQueue might do almost everything you need from a
Queue.Because a LinkedTransferQueue implements the BlockingQueue ,
TransferQueue , and Queue interfaces, it can be used to showcase all the
different methods that can be used to add and remove elements using the
various types of queues. Creating a LinkedTransferQueue is easy. Because
LinkedTransferQueue is not bound by size, a limit to the number of
elements CANNOT be supplied to its constructor.

 

**Executors**

 

Executors (and the ThreadPools used by them) help meet two of the same
needs that Thread s do:

1\. Creating and scheduling some Java code for execution and

2\. Optimizing the execution of that code for the hardware resources you
have

available

 

With traditional threading, you handle needs 1 and 2 yourself. With
Executor s, you handle need 1, but you get to use an off-the-shelf
solution for need 2. The java. util.concurrent package provides several
different off-the-shelf solutions

 

In a way, an Executor is an alternative to starting new threads. Using
Thread s directly can be considered low-level multithreading, while
using Executor s can be considered high-level multithreading.

 

Do you own a computer that can concurrently run 10,000 threads or 1,000
or even 100? Probably not—this is a trick question. A quad-core CPU
(with four processors per unit) might be able to execute two threads per
core for a total of eight concurrently executing threads. You can start
10,000 threads, but not all of them will be running at the same time.
The underlying operating system's task scheduler rotates the threads so
that they each get a slice of time on a processor. Ten thousand threads
all competing for a turn on a processor wouldn't make for a very
responsive system. Threads would either have to wait so long for a turn
or get such small turns (or both) that performance would suffer.

In addition, each thread consumes system resources. It takes processor
cycles to perform a context switch (saving the state of a thread and
resuming another thread), and each thread consumes system memory for its
stack space. Stack space is used for temporary storage and to keep track
of where a thread returns to after completing a method call. Depending
on a thread's behavior, it might be possible to lower the cost (in RAM)
of creating a thread by reducing a thread's stack size.

 

To reduce a thread's stack size, the Oracle JVM supports using the
nonstandard- Xss1024k option to the java command. Note that decreasing
the value too far can result in some threads throwing exceptions when
performing certain tasks, such as making a large number of recursive
method calls.

 

Another limiting factor in being able to run 10,000 threads in an
application has to do with the underlying limits of the OS. Operating
systems typically have limits on the number of threads an application
can create. These limits can prevent a buggy application from spawning
countless threads and making your system unresponsive. If you have a
legitimate need to run 10,000 threads, you will probably have to consult
your operating system's documentation to discover possible limits and
configuration options

 

The task scheduler is itself a software program. The more CPU cycles
spent scheduling and preempting threads, the less processor time you
have to execute your application threads.

 

If we want to adjust the number of threads that are started, we need to
decouple the tasks that are to be performed (our Runnable instances)
from our thread creation and starting. This is where a java.util.
concurrent.Executor can help. The basic usage looks something like this:

Runnable r = new MyRunnableTask();

Executor ex = // details to follow

ex.execute(r);

 

You can easily create your own implementations of an Executor with
custom behaviors. As you'll see soon, several implementations are
provided in the standard Java SE libraries.

 

import java.util.concurrent.Executor;

public class SameThreadExecutor implements Executor {

@Override

public void execute(Runnable command) {

command.run(); // caller waits

}

}

The following Executor implementation would use a new thread for each
task:

import java.util.concurrent.Executor;

public class NewThreadExecutor implements Executor {

@Override

public void execute(Runnable command) {

Thread t = new Thread(command);

t.start();

}

}

This example shows how an Executor implementation can be put to use:

Runnable r = new MyRunnableTask();

Executor ex = new NewThreadExecutor(); // choose Executor

ex.executor(r);

 

By coding to the Executor interface, the submission of tasks is
decoupled from the execution of tasks. The result is that you can easily
modify how threads are used to execute tasks in your applications

 

Several Executor implementations are supplied as part of the standard
Java libraries. The Executor instances returned by Executors are
actually of type ExecutorService (which extends Executor ). An
ExecutorService provides management capability and can return Future
references that are used to obtain the result of executing a task
asynchronously.

 

A **cached thread pool** will create new threads as they are needed and
reuse threads that have become free. Threads that have been idle for 60
seconds are removed from the pool. Watch out! Without some type of
external limitation, a cached thread pool may be used to create more
threads than your system can handle.

 

A **fixed thread pool** is constructed using a numeric argument (4 in
the preceding example) that specifies the number of threads used to
execute tasks. This type of pool will probably be the one you use the
most because it prevents an application from overloading a system with
too many threads. Tasks that cannot be executed immediately are placed
on an unbounded queue for later execution

 

 

Both Executors.newCachedThreadPool() and Executors
.newFixedThreadPool(4) return objects of type java.util.concurrent
.ThreadPoolExecutor (which implements ExecutorService and Executor ).
You will typically use the Executors factory methods instead of creating
ThreadPoolExecutor instances directly, but you can cast the fixed or
cached thread pool ExecutorService references if you need access to the
additional methods. The following example shows how you could
dynamically adjust the thread count of a pool at runtime:

ThreadPoolExecutor tpe =
(ThreadPoolExecutor)Executors.newFixedThreadPool(4);

tpe.setCorePoolSize(8);

tpe.setMaximumPoolSize(8);

 

 

A **single thread pool** uses a single thread to execute tasks. Tasks
that cannot be executed immediately are placed on an unbounded queue for
later execution. Unlike a fixed thread pool executor with a size of 1, a
single thread executor prevents any adjustments to the number of threads
in the pool.

 

In addition to the three basic ExecutorService behaviors outlined
already, the Executors class has factory methods to produce a
S**cheduledThreadPoolExecutor** . A ScheduledThreadPoolExecutor enables
tasks to be executed after a delay or at repeating intervals.

 

The java.util.concurrent.**Callable** interface serves the same purpose
as the Runnable interface, but provides more flexibility. Unlike the
Runnable interface, a Callable may return a result upon completing
execution and may throw a checked exception. An ExecutorService can be
passed a Callable instead of a Runnable .

 

The primary benefit of using a Callable is the ability to return a
result. Because an ExecutorService may execute the Callable
asynchronously (just like a Runnable ), you need a way to check the
completion status of a Callable and obtain the result later. A
java.util.concurrent.**Future** is used to obtain the status and result
of a Callable . Without a Future , you'd have no way to obtain the
result of a completed Callable and you might as well use a Runnable
(which returns void) instead of a Callable .

 

**Submitting a Callable to an ExecutorService returns a Future
reference.**

When you use the Future to obtain the Callable 's result, you will have
to handle two possible exceptions:

 

■ InterruptedException : Raised when the thread calling the Future 's
get() method is interrupted before a result can be returned

■ ExecutionException : Raised when an exception was thrown during the
execution of the Callable 's call() method

 

I/O activities in your Runnable and Callable instances can be a serious
bottleneck. In preceding examples, the use of System.out.println() will
cause I/O activity. If this wasn't a trivial example being used to
demonstrate Callable and ExecutorService , you would probably want to
avoid repeated calls to println() in the Callable . One possibility
would be to use StringBuilder to concatenate all output strings and have
a single println() call before the call() method returns. Another
possibility would be to use a logging framework (see java.util.logging )
in place of any println() calls.

 

**ThreadLocalRandom** is a new way in Java 7 to create random numbers.
Math. random() and shared Random instances are thread-safe, but suffer
from contention when used by multiple threads. A ThreadLocalRandom is
unique to a thread and will perform better because it avoids any
contention. ThreadLocalRandom also provides several convenient methods
such as nextInt(int,int) that allow you to specify the range of possible
values returned.

 

 

An **ExecutorService should be shut down** once it is no longer needed
to free up system resources and to allow graceful application shutdown.
Because the threads in an ExecutorService may be nondaemon threads, they
may prevent normal application termination. In other words, your
application stays running after completing its main method.

 

 

What if you need to fill up a 100,000,000-element array with randomly
generated values? The **Fork-Join Framework** makes it easier to tackle
big tasks like this, while leveraging all of the CPUs in a system.

 

The **Fork-Join ExecutorService** implementation is java.util.concurrent
.ForkJoinPool . You will typically submit a single task to a
ForkJoinPool and await its completion. The ForkJoinPool and the task
itself work together to divide and conquer the problem. Any problem that
can be recursively divided can be solved using Fork-Join. 

ForkJoinPool fjPool = new ForkJoinPool();

The no-arg ForkJoinPool constructor creates an instance that will use
the Runtime.availableProcessors() method to determine the level of
parallelism. The level of parallelism determines the number of threads
that will be used by the ForkJoinPool . There is also a ForkJoinPool(int
parallelism) constructor that allows you to override the number of
threads that will be used.

 

With the Fork-Join Framework, a java.util.concurrent.ForkJoinTask
instance (actually a subclass—more on that later) is created to
represent the task that should be accomplished. This is different from
other executor services that primarily used either Runnable or Callable
.

 

**JDBC**

 

There are three important concepts when working with a database:

■ Creating a connection to the database

■ Creating a statement to execute in the database

■ Getting back a set of data that represents the results

 

The purpose of JDBC is to provide an application programming interface
(API) for Java developers to write Java applications that can access and
manipulate relational databases and use SQL to perform CRUD operations.

 

One of the driving forces behind JDBC was to provide a standard way to
access relational databases, but JDBC can also be used to access file
systems and object-oriented data sources. The key is that the API
provides an abstract view of a database connection, statements, and
result sets. These concepts are represented in the API as interfaces in
the java.sql package: Connection ,

Statement , and ResultSet , respectively.

 

The java.sql.Connection interface defines the contract for an object
that represents the connection with a relational database system.The
Statement interface provides an abstraction of the functionality needed
to get a SQL statement to execute on a database, and a ResultSet
interface is an abstraction functionality needed to process a result set
(the table of data) that is

returned from the SQL query when the query involves a SQL SELECT
statement.

 

One important class for JDBC is the java.sql.**DriverManager** class.
This concrete class is used to interact with a JDBC driver and return
instances of Connection objects to you. The DriverManager class is so
named because it manages which JDBC driver implementation you get when
you request an instance of a Connection through the getConnection()
method.

 

When you invoke the DriverManager 's getConnection() method, you are
asking the DriverManager to try passing the first string in the
statement, the driver URL, along with the username and password to each
of the driver classes registered with the DriverManager in turn. If one
of the driver classes recognizes the URL string, and the username and
password are accepted, the driver returns an instance of a Connection
object. If, however, the URL is incorrect, or the username and/or
password are not correct, then the method will throw a SQLException .

 

First, one or more JDBC drivers, in a JAR or ZIP file, are included in
the classpath of your application. The DriverManager class uses a
service provider mechanism to search the classpath for any JAR or ZIP
files that contain a file named java.sql.Driver in the META-INF/services
folder of the driver jar or zip. This is simply a text file that
contains the full name of the class that the vendor used to implement
the jdbc.sql.Driver interface.The DriverManager will then attempt to
load the class it found in the java. sql.Driver file using the class
loader:

Class.forName("org.apache.derby.jdbc.ClientDriver");

When the driver class is loaded, its static initialization block is
executed. Per the JDBC specification, one of the first activities of a
driver instance is to "self-register" with the DriverManager class by
invoking a static method on DriverManager .

 

Now, when your application invokes the DriverManager.getConnection()
method and passes a JDBC URL, username, and password to the method, the
DriverManager simply invokes the connect() method on the registered
Driver . If the connection was successful, the method returns a
Connection object instance to DriverManager , which, in turn, passes
that back to you.

 

If there is more than one registered driver, the DriverManager calls
each of the drivers in turn and attempts to get a Connection object from
them. The first driver that recognizes the JDBC URL and successfully
creates a connection using the username and password will return an
instance of a Connection object.

 

The JDBC URL is what is used to determine which driver implementation to
use for a given Connection . Think of the JDBC URL (uniform resource
locator) as a way to narrow down the universe of possible drivers to one
specific connection.

 

jdbc:derby://localhost:1521/BookSellerDB

The first part, jdbc , simply identifies that this is a JDBC URL (versus
HTTP or something else). The second part indicates that driver vendor is
derby driver. The third part indicates that the database is on the
localhost of this machine, 127.0.0.1), at port 1521 , and the final part
indicates that we are interested in the BookSellerDB database.

 

Unfortunately, other than a requirement that the JDBC URL begin with
"jdbc," there is very little standard about a JDBC URL. Vendors may
modify the URL to define characteristics for a particular driver
implementation.

 

Since a **DataSource** instance is typically obtained through a Java
Naming and Directory Interface (JNDI) lookup, it is more often used in
Java applications where there is a container that supports JNDI—for
example, a Java EE application server

 

From a Connection object, we can create an instance of a **Statement**
object (or, to be precise, using the Connection instance we received
from the DriverManager , we can get an instance of an object that
implements the Statement interface). Because not all SQL statements
return results, the Statement object provides several different methods
to execute SQL commands. Some SQL commands do not return a result set,
but instead return an integer status.

 

When a query returns a result set, an instance of a class that
implements the **ResultSet** interface is returned. The ResultSet object
represents the results of the query—all of the data in each row on a
per-column basis. Again, as a reminder, how data in a ResultSet are
stored is entirely up to the JDBC driver vendor. It is possible that the
JDBC driver caches the entire set of results in memory all at once, or
that it uses internal buffers and gets only a few rows at a time. From
your point of view as the user of the data, it really doesn't matter
much. Using the methods defined in the ResultSet interface, you can read
and manipulate the data, and that's all that matters. One important
thing to keep in mind is that a ResultSet is a copy of the data from the
database from the instance in time when the query was executed. Unless
you are the only person using the database, you need to always assume
that the underlying database table or tables that the ResultSet came
from could be changed by some other user or application.

 

 

Using **ResultSetMetaData** , you can get important information about
the results returned from the query, including the number of columns,
the table name, the column name, and the column class name—the Java
class that is used to represent this column when the column is returned
as an Object

 

There are three ResultSet cursor types:

■ TYPE\_FORWARD\_ONLY : The default value for a ResultSet —the cursor
moves forward only through a set of results.

■ TYPE\_SCROLL\_INSENSITIVE : A cursor position can be moved in the
result forward or backward, or positioned to a particular cursor
location. Any changes made to the underlying data—the database
itself—are not reflected in the result set. In other words, the result
set does not have to "keep state" with the database. This type is
generally supported by databases.

■ TYPE\_SCROLL\_SENSITIVE : A cursor can be changed in the results
forward or backward, or positioned to a particular cursor location. Any
changes made to the underlying data are reflected in the open result
set. As you can imagine, this is difficult to implement, and is
therefore not implemented in a database or JDBC driver very often. JDBC
provides two options for data concurrency with a result set:

■ CONCUR\_READ\_ONLY :This is the default value for result set
concurrency. Any open result set is read-only and cannot be modified or
changed.

■ CONCUR\_UPDATABLE : A result set can be modified through the ResultSet
methods while the result set is open.

 

 

boolean **next**(): Moves the cursor to the next row in the ResultSet .
Returns false if the cursor is positioned beyond the last row.

 

boolean **previous**() Moves the cursor backward one row. Returns false
if the cursor is positioned before the first row.

 

boolean **absolute**(int row) Moves the cursor to an absolute position
in the ResultSet . Rows are numbered from 1. Moving to row 0 moves the
cursor to before the first row. Moving to negative row numbers starts
from the last row and works backward. Returns false if the cursor is
positioned beyond the last row or before the first row.

 

boolean **relative**(int row) Moves the cursor to a position relative to
the current position. Invoking relative(1) moves forward one row;
invoking relative(-1) moves backward one row. Returns false if the
cursor is positioned beyond the last row or before the first row.

 

boolean **first**() Moves the cursor to the first row in the ResultSet

 

boolean **last**() Moves the cursor to the last row in the ResultSet .
Returns false if there are no rows in the ResultSet (empty result set).

  

void **beforeFirst**() Moves the cursor to before the first row in the
ResultSet .

void **afterLast**() Moves the cursor to after the last row in the
ResultSet .

 

■ isBeforeFirst() :True if the cursor is positioned before the first row

■ isAfterLast() : True if the cursor is positioned after the last row

■ isFirst() : True if the cursor is on the first row

■ isLast() : True if the cursor is on the last row

 

 

If you have casually used JDBC, or are new to JDBC, you may be surprised
to know that a ResultSet object can do more than just provide the
results of a query to your application. Besides just returning the
results of a query, a ResultSet object may be used to modify the
contents of a database table, including update existing rows, delete
existing rows, and add new rows.

 

When you create a Statement with concurrency set to CONCUR\_UPDATABLE,
you can modify the data in a result set and then apply your changes back
to the database without having to issue another query.

 

In addition to the getXXXX methods we looked at for ResultSet , methods
that get column values as integers, Date objects, String s, etc., there
is an equivalent updateXXXX method for each type. And, just like the
getXXXX methods, the updateXXXX methods can take either a String column
name or an integer column index.

 

void **updateRow**() Updates the database with the contents of the
current row of this ResultSet .

 

void **deleteRow**() Deletes the current row from the ResultSet and the
underlying database.

 

void **cancelRowUpdates**() Cancels any updates made to the current row
of this ResultSet object. This method will effectively undo any changes
made to the ResultSet row. If the updateRow() method was called before
cancelRowUpdates , this method will have no effect.

 

void **moveToInsertRow**() Moves the cursor to a special row in the
ResultSet set aside for performing an insert. You need to move to the
insert row before updating the columns of the row with update methods
and calling insertRow() .

 

void **insertRow**() Inserts the contents of the insert row into the
database. Note that this method does not change the current ResultSet ,
so the ResultSet should be read again if you want the ResultSet to be
consistent with the contents of the database.

 

void **moveToCurrentRow**() Moves the cursor back to the current row
from the insert row. If the cursor was not on the insert row, this
method has no effect.

 

 

**Exceptions and Warnings**

** **

public String **getMessage**() This method is actually inherited from
java. lang.Exception , which SQLException extends from. But this method
returns the detailed reason why the exception was thrown

 

public String **getSQLState**() The String returned by getSQLState
provides a specific code and related message. SQLState messages are
defined by the X/Open and SQL:2003 standards; however, it is up to the
implementation to use these values.

 

 

public SQLException **getNextException**() One of the interesting
aspects of SQLException is that the exception thrown could be the result
of more than one issue. Fortunately, JDBC simply tacks each exception
onto the next in a process called chaining. Typically, the most severe
exception is thrown last, so it is the first exception in the chain.

 

SQLWarning **getWarnings**() throws SQLException This method gets the
first SQLWarning object or returns null if there are no warnings for
this Connection , Statement , or ResultSet object. A SQLException is
thrown if the method is called on a closed object.

 

 

It is also a good practice to minimize the number of times you close and
re-create Connection objects. As a rule, creating the connection to the
database and passing the username and password credentials for
authentication is a relatively expensive process, so performing the
activity once for every SQL query would not result in highly performing
code. In fact, typically, database connections are created in a pool,
and connection instances are handed out to applications as needed

 

A resource declared in the **try -with-resource** statement must
implement the AutoCloseable interface. One of the changes for JDBC in
Java SE 7 (JDBC 4.1) was the modification of the API so that Connection
, Statement , and ResultSet all implement the AutoCloseable interface
and support automatic resource management.

 

String url, user, pwd; // These are populated somewhere else

try (Connection conn = DriverManager.getConnection(url, user, pwd)){

Statement stmt = conn.createStatement();

ResultSet rs = stmt.executeQuery("SELECT \* FROM Customer");

// ... process the results

// ...

if (rs != null && stmt != null) {

rs.close();

// Attempt to close the ResultSet

stmt.close();

// Attempt to close the Statement

}

} catch (SQLException se) {

out.println("SQLException: " + se);

}

 

Note that when more than one resource is declared in the try
-with-resources statement, the resources are closed in the reverse order
of their declaration—so stmt.close() will be called first, followed by
conn.close() .

 

It probably makes sense that if there is an exception thrown from the
try block, the exception will be caught by the catch statement, but what
happens to exceptions thrown as a result of closing the resources in the
try -with-resources statement? Any exceptions thrown as a result of
closing resources at the end of the try block are suppressed if there
was also an exception thrown in the try block. These exceptions can be
retrieved from the exception thrown by calling the getSuppressed()
method on the exception thrown

 

A **PreparedStatement** can improve the performance of a frequently
executed query because the SQL part of the statement is precompiled in
the database.When a SQL string is sent to a database, the string goes
through a number of processing steps. First, the string is parsed and
all of the SQL keywords are checked for proper syntax. Next, the table
and column names are checked against the schema to make sure they all
exist (and are properly spelled). Next, the database creates an
execution plan for the query, choosing between several options for the
best overall performance. Finally, the chosen execution plan is run.

 

 

The steps leading up to the execution of a query plan can be done in
advance using a PreparedStatement object. Parameters can be passed to a
PreparedStatement , and these are inserted into the query just before
execution. This is why PreparedStatement is a good choice for a
frequently executed SQL statement.

 

Databases also provide the capability for developers to write small
programs directly to the database. Each program is named, compiled, and
stored in the database itself. These named programs are generally
developed and added to the database when the tables are created. There
are three types of these small programs: procedures, functions, and
triggers. Because triggers are only invoked by the database itself and
are not accessible by SQL queries or directly from an external
application,

 

The advantage of stored procedures and functions is that they are
completely self-contained. You can think of a stored procedure as a
method for a database. You call the stored procedure using its name and
pass it arguments.

 

The CallableStatement is used to execute a named stored procedure or
function. Unlike prepared statements, stored procedures and functions
must exist before a CallableStatement can be executed on them. Like
PreparedStatement s, parameters can be passed to stored procedures and
functions.

 

PreparedStatement objects are obtained from a Connection object in the
same way that Statement objects are obtained, but through the
prepareStatement() method instead of a createStatement() method. There
are several forms of the prepareStatement method, including those that
take the result set type and result set concurrency, just like Statement
, so a ResultSet returned from a PreparedStatement can be scrollable and
updatable as well.

 

To create a PreparedStatement object instance, you pass a String query
to the prepareStatement() method. The string passed as an argument is a
parameterized query. Thus, the PreparedStatement object instance is
constructed before the final query is executed, allowing you to modify
the parameters of the query without having to construct a new Statement
object every time.Parameters passed into the query are referred to as IN
parameters

 

the power of a PreparedStatement is that once the object is created with
the parameterized query, the query is precompiled. When bind parameters
are passed in the query, the query is stored in its post-plan state in
the database. When parameters are received, the database simply has to
substitute them into the plan and execute the query.

 

The **CallableStatement** extends the PreparedStatement interface to
support calling a stored procedure or function using JDBC. By the way,
the only difference between a stored procedure and a function is that a
function is designed to return an argument.

 

Stored procedures offer a number of advantages over straight SQL
queries. Most stored procedure languages are fairly sophisticated and
support variables, branching, looping, and if-then-else constructs. A
stored procedure can execute any SQL statement, so a single stored
procedure can perform a number of operations in a single execution.

 

One use case for a stored procedure is to encapsulate specific tables in
the database. Just like a Java class can encapsulate data by making a
field private and then only providing access to the field through a
method, a stored procedure can be used to prevent a user from having
access to the data in a table directly.

 

 There are two drawbacks to stored procedures. First, stored procedures
are typically developed in a proprietary, database-specific language,
requiring a developer to learn yet another set of commands and syntax.
Second, once in the database, how they were written and what they
actually do can be difficult to figure out since they are "compiled"
into the database

 

Because stored procedures can be a proprietary language with a unique
syntax, the JDBC API provides JDBC-specific escape syntax for executing
stored procedures and functions. The JDBC driver takes care of
converting the JDBC syntax to the database format. This syntax has two
forms: one form for functions that return a result, and another form for
stored procedures that do not return a result.

 

 

**RowSet** is a ResultSet . The RowSet interface extends the ResultSet
interface. RowSet objects fall into two categories: those that are
**connected** to the database and therefore stay in sync with the data
in the database, and those that can be **disconnected** from a database
and synchronized with the database later. A connected RowSet provides
you with the opportunity to keep state synchronized with data in a
database table—so you might use a connected RowSet object to keep a
shopping cart or other type of cache without needing to translate
changes in your cart object into SQL update or insert queries. A
disconnected RowSet is created with some initial state read from the
database and can then be disconnected and passed to other objects and
later synchronized with the database with changes

Note there is no magic associated with data synchronization—a RowSet is
a ResultSet , and therefore has the ability to update, remove, and
insert new rows in the database. The difference between a ResultSet and
RowSet is that a RowSet can maintain state so that when the underlying
ResultSet object is changed, the data changes are reflected in the
database—either synchronously, in the case of a connected RowSet , or
asynchronously, in the case of a disconnected RowSet .

 

A RowSet registers for an event by adding an instance of a class that
implements the RowSetListener interface, which has three event methods
that are invoked when one of the following events occurs on an instance
of a RowSet object:

■ A change in the cursor location

■ A change to a row in this RowSet (inserted, updated, or deleted)

■ A change to the RowSet contents (a new RowSet )

 

 

**JDBC Transaction**

** **

■ All transactions are in auto-commit mode unless explicitly disabled.

■ Transactions have varying levels of isolation—that is, what data is
visible to the code executing in a transaction.

■ JDBC supports the idea of a savepoint. A savepoint is a point within a
transaction where the work that occurred up until that point is valid. A
savepoint is useful when there are conditions in a transaction that you
wish to preserve even if other parts of the transaction fail.

 

When a SQL statement requires a transaction, the JDBC driver or database
creates a transaction and commits the transaction when the statement
ends. In order for you to control transactions with JDBC, you must first
turn off this auto-commit mode:

 

when you turn off auto-commit mode, you also explicitly begin a
transaction. A transaction includes all of the SQL queries you execute
until either

■ You explicitly commit the current transaction.

■ You explicitly roll back the current transaction.

■ There is a failure that forces an automatic rollback.

 

 

we start a transaction on a Connection object by turning auto-commit off
(false). This means that Connection can only have one transaction active
at any one time. And without going into a lot of details about the
different transaction models, this means that **transactions in JDBC are
flat**. A flat transaction can include a number of different SQL
statements, but there is only one transaction, and it only has one
beginning and one end

 

The other point is that as soon as the commit() method returns, we have
started another transaction. Now what happens to our database if we
don't invoke the commit() method? Well, because invoking commit()
changes the database, and JDBC is required to make sure that any
statements are completely executed, the driver will not perform a commit
implicitly, and the driver and database simply roll back the transaction
as if nothing happened.

 

One thing that is important to remember when using transactions is that
it is extremely rare for an application to have only one user. As a
result, there is a strong likelihood that two users will attempt to
access the same data at the same time. An important aspect of
transactions is isolation level—the visibility of one transaction to the
changes being made by another

transaction. Most databases (and therefore their drivers) have some
default isolation level, and you can determine what isolation support is
availableusing DatabaseMetaData and set the isolation level using the
Connection setTransactionIsolation() method. However, choosing the
appropriate isolation level is an important task because with too little
isolation, you run the risk of incorrect results, and with too much
isolation, application performance suffers. Typically, you would work
with your DBA to learn what the default isolation level is for your
database and whether customizing the level would be appropriate for your
application.

 

A **savepoint** is some point in a transaction where you want to place a
virtual marker, indicating that everything is good up until this point.
Rather than roll back the entire transaction, the application may place
a savepoint on the order (for some limited amount of time) to allow the
customer to decide if they want either the order all at once or a
partial shipment now of the available titles and the rest later. If the
customer agrees to receive a partial shipment, the transaction could
then continue from the savepoint and ship part of the order.

 

In the JDBC API, a Savepoint is an object returned by a Connection in a
transaction. A Savepoint object can be named or unnamed (created with a
String name or not). The benefit of a Savepoint is that it represents a
point in a transaction that you can roll back to.

 

■ When you set Savepoint A and then later set Savepoint B, if you roll
back to Savepoint A, you automatically release and invalidate Savepoint
B.

■ Support for Savepoints is not required, but you can check to see if
your JDBC driver and database support Savepoints using the
DatabaseMetaData .supportsSavePoints() method, which will return true if
Savepoints are supported.

■ Because a Savepoint is an actual point-in-time state of a transaction
context, the number of Savepoints supported by your JDBC driver and
database may be limited. For example, the Java DB database does support
Savepoints, but only one per transaction.

 

The bad news is that there is no method to determine the number of
Savepoints supported by your JDBC driver and database. The good news is
that if you only get one, you can reuse it. Connection provides a
releaseSavepoint() method, which takes a Savepoint object. After the
Savepoint is released, you can set another Savepoint, sort of like
moving your pebble forward in hopscotch!

 

 

Hashing Passwords

Friday, February 19, 2016

14:12

 

How to Safely Store Your Users' Passwords in 2016

February 15, 2016 12:13 pm by [P.I.E.
Staff](https://paragonie.com/blog/author/p-i-e-staff)

[Security
Engineering](https://paragonie.com/blog/category/security-engineering)

If you are unfamiliar with cryptography concepts or the vocabulary it
uses, or especially you are looking for guidance on "password
encryption", please read [this page
first](https://paragonie.com/blog/2015/08/you-wouldnt-base64-a-password-cryptography-decoded).

We've previously said that [even security advice should carry an
expiration
date](https://paragonie.com/blog/2015/06/guide-securing-your-business-s-online-presence-for-non-experts).
So unlike most of our past blog posts, this page should be considered a
living document: As requirements change and new attacks are discovered,
we will update it accordingly.

**Semantic point:** Don't store the password, store a hash of the
password. ([Obligatory](http://howtosafelystoreapassword.com/).)

Modern, Secure, Salted Password Hashing Made Simple

**The Problem**: You want people to be able to create a unique user
account, with a password, which they will use to access your
application. How can you safely implement this feature?

**Easiest Solution**: [Use
libsodium](https://paragonie.com/blog/2015/09/how-to-safely-implement-cryptography-in-any-application),
which provides a secure password hashing API in most languages. As of
version 1.0.8 it uses
the [scrypt](https://en.wikipedia.org/wiki/Scrypt) algorithm, but in the
next release (1.0.9) it will also offer **Argon2**, the most recent,
carefully-selected algorithm from the [Password Hashing
Competition](https://password-hashing.net/). Libsodium offers [bindings
for most programming
languages](https://download.libsodium.org/doc/bindings_for_other_languages/index.html).

-   [Libsodium documentation](https://download.libsodium.org/doc/)

-   [Libsodium source code](https://github.com/jedisct1/libsodium)

**Note:** There is a published [attack on
Argon2i](http://permalink.gmane.org/gmane.comp.security.phc/3606), the
recommended variant of Argon2 for general purpose password hashing. The
practical implications aren't severe, but it may lead to a new variant
("Argon2x" perhaps, since it would presumably use XOR instead of
overwriting memory to mitigate these attacks) being christened and
recommended.

If you, for whatever reason, cannot reconcile your requirements with
installing libsodium, you have other options. In preparing this blog
post, our security team has investigated several password hashing
libraries in multiple programming languages. What follows is our current
recommendations for secure password storage with example code.

-   [PHP](https://paragonie.com/blog/2016/02/how-safely-store-password-in-2016#php)

-   [Java](https://paragonie.com/blog/2016/02/how-safely-store-password-in-2016#java)

-   [C\# (.NET)](https://paragonie.com/blog/2016/02/how-safely-store-password-in-2016#csharp)

-   [Ruby](https://paragonie.com/blog/2016/02/how-safely-store-password-in-2016#ruby)

-   [Python](https://paragonie.com/blog/2016/02/how-safely-store-password-in-2016#python)

-   [Node.js](https://paragonie.com/blog/2016/02/how-safely-store-password-in-2016#nodejs)

Acceptable Password Hashing Algorithms

Although there is disagreement about how to rank them, cryptography
experts agree that these algorithms are the only ones you should be
using to store passwords in 2016:

-   **Argon2**, the [Password Hashing Competition
    > winner](https://password-hashing.net/).

-   **bcrypt**

-   **scrypt**

-   The other Password Hashing Competition finalists
    > (**Catena**, **Lyra2**, **Makwa**, and **yescrypt**)

-   **PBKDF2** (nearly everyone except FIPS agrees [PBKDF2 is the worst
    > of the acceptable
    > options](http://www.openwall.com/presentations/PHDays2014-Yescrypt/mgp00004.html),
    > but is still acceptable)

Secure Password Storage in PHP

First, make sure you're using a [supported version of
PHP](https://secure.php.net/supported-versions.php). If you are,
then [the PHP password
API](https://secure.php.net/manual/en/ref.password.php) will be
available for use. If you aren't, consider upgrading. If you can't,
check
out [password\_compat](https://github.com/ircmaxell/password_compat).

\$hash = password\_hash(\$userPassword, PASSWORD\_DEFAULT);

[password\_hash()](https://secure.php.net/password_hash) takes care of
salting the hash, transparently. You can, however, specify your
own[cost](http://security.stackexchange.com/a/3993/43688). The absolute
minimum value you should consider using is 10. 12 is good, provided your
hardware supports it. The default cost parameter is 10.

\$hash = password\_hash(\$userPassword, PASSWORD\_DEFAULT, \['cost'
=&gt; 12\]);

Verifying a password against a stored hash is incredibly simple:

**if** (password\_verify(\$userPassword, \$hash)) {\
*// Login successful.*\
**if** (password\_needs\_rehash(\$userPassword, PASSWORD\_DEFAULT,
\['cost' =&gt; 12\])) {\
*// Recalculate a new password\_hash() and overwrite the one we stored
previously*\
}\
}

As of PHP 7, PASSWORD\_DEFAULT still uses bcrypt. In a future version,
it may migrate to Argon2.

Alternative: Scrypt Password Hashing in PHP

If you aren't using libsodium (which we strongly recommend that
you *do* use!), you can still get scrypt hashes in PHP through [Dominic
Black's Scrypt PHP
Extension](https://github.com/DomBlack/php-scrypt) from PECL.

*\# If you don't have PECL installed, get that first.*\
pecl install scrypt\
echo "extension=scrypt.so" &gt; /etc/php5/mods-available/scrypt.ini\
php5enmod scrypt

Next, grab a copy of [the bundled PHP
wrapper](https://github.com/DomBlack/php-scrypt/blob/master/scrypt.php) and
include it in your project.

*\# Hashing*\
\$hash = \\Password::hash(\$userProvidedPassword);\
*\# Validation*\
**if** (\\Password::check(\$userProvidedPassword, \$hash)) {\
// Logged **in** successfully.\
}

Secure Password Storage in Java

Your best bet for secure password hashing in a Java application, outside
libsodium, is [jBCrypt](https://github.com/jeremyh/jBCrypt), which
provides the bcrypt password hashing algorithm.

String hash = BCrypt.hashpw(userProvidedPassword, BCrypt.gensalt());

Verifying a bcrypt hash in Java:

**if** (BCrypt.checkpw(userProvidedPassword, hash)) {\
*// Login successful.*\
}

Alternative: Scrypt Password Hashing in Java

There is a [Java implementation of
scrypt](https://github.com/wg/scrypt), but it requires you to specify
the parameters rather than providing sane defaults.

*\# Calculating a hash*\
**int** N = 16384;\
**int** r = 8;\
**int** p = 1;\
String hashed = SCryptUtil.scrypt(passwd, N, r, p);

*\# Validating a hash*\
**if** (SCryptUtil.check(passwd, hashed)) {\
// Login successful\
}

Secure Password Storage in C\# (.NET)

We recommend [Martin Steel's BCrypt.NET
fork](https://github.com/martinsteel/Bcrypt.NET) overSystem.Security.Cryptography.Rfc2898DeriveBytes,
which is PBKDF2-SHA1. (We're not saying PBKDF2-SHA1 is unsafe, but that
bcrypt is preferable to it.)

*// Calculating a hash*\
string hash = BCrypt.HashPassword(usersPassword, BCrypt.GenerateSalt());

*// Validating a hash*\
**if** (BCrypt.Verify(usersPassword, hash)) {\
*// Login successful*\
}

Alternative: Scrypt Password Hashing in C\# (.NET)

There is an [Scrypt package in
NuGET](https://github.com/viniciuschiele/Scrypt) as well.

*// This is necessary:*\
ScryptEncoder encoder = **new** ScryptEncoder();\
*// Calculating a hash*\
SecureString hashedPassword = encoder.Encode(usersPassword);\
*// Validating a hash*\
**if** (encoder.Compare(usersPassword, hashedPassword)) {\
*// Login successful*\
}

Secure Password Storage in Ruby

From the author of ["Use bcrypt. Use bcrypt. Use
bcrypt..."](https://codahale.com/how-to-safely-store-a-password/) comes
a [Ruby gem for bcrypt password
hashing](https://github.com/codahale/bcrypt-ruby).

require "bcrypt"

*\# Calculating a hash*\
my\_password = BCrypt::Password.create(usersPassword)\
*\# Validating a hash*\
**if** my\_password == usersPassword\
*\# Login successful*

Beware that, as of this writing, this library is not
following [cryptography coding best
practices](https://cryptocoding.net/index.php/Coding_rules#Compare_secret_strings_in_constant_time).
Consider applying [this
patch](https://github.com/codahale/bcrypt-ruby/pull/119/files) until
they get around to merging it.

Alternative: Scrypt Hashing in Ruby

There is also a [Ruby gem for scrypt password
hashing](https://github.com/pbhogan/scrypt).

require "scrypt"

*\# Calculating a hash*\
password = SCrypt::Password.create(usersPassword)\
*\# Validating a hash*\
**if** password == usersPassword\
*\# Login successful*

Secure Password Storage in Python

You can't go wrong with the [bcrypt Python
package](https://pypi.python.org/pypi/bcrypt/2.0.0) (also
on [github](https://github.com/pyca/bcrypt)):

**import** bcrypt\
**import** hmac

*\# Calculating a hash*\
password = b"correct horse battery staple"\
hashed = bcrypt.hashpw(password, bcrypt.gensalt())\
*\# Validating a hash (don't use ==)*\
**if** (hmac.compare\_digest(bcrypt.hashpw(password, hashed), hashed)):\
*\# Login successful*

Python developers generally
prefer [passlib](https://pypi.python.org/pypi/passlib) ([Bitbucket](https://bitbucket.org/ecollins/passlib/wiki/Home)),
although its API is named incorrectly ("encrypt" instead of "hash"):

**from** passlib.hash **import** bcrypt

*\# Calculating a hash*\
hash = bcrypt.encrypt(usersPassword, rounds=12)

*\# Validating a hash*\
**if** bcrypt.verify(usersPassword, hash):\
*\# Login successful*

Alternative: Scrypt Hashing in Python

Currently the only sane scrypt implementation in Python that we could
find (outside libsodium) is the [django-scrypt
package](https://pypi.python.org/pypi/django-scrypt). Still on the
look-out for more.

Secure Password Storage in Node.js

There are two secure implementations of bcrypt in Node.js,
although [bcrypt](https://www.npmjs.com/package/bcrypt) ([Github](https://github.com/ncb000gt/node.bcrypt.js))
seems to be the preferred one. We're making extensive use
of [Promises](https://gist.github.com/joepie91/791640557e3e5fd80861) to
greatly simplify error handling in the examples below:

**var** Promise = **require**("bluebird");\
**var** bcrypt = Promise.promisifyAll(**require**("bcrypt"));

**function** **addBcryptType**(err) {\
*// Compensate for \`bcrypt\` not using identifiable error types*\
err.type = "bcryptError";\
**throw** err;\
}

*// Calculating a hash:*\
Promise.**try**(**function**() {\
**return** bcrypt.hashAsync(usersPassword,
10).**catch**(addBcryptType);\
}).then(**function**(hash) {\
*// Store hash in your password DB.*\
});

*// Validating a hash:*\
*// Load hash from your password DB.*\
Promise.**try**(**function**() {\
**return** bcrypt.compareAsync(usersPassword,
hash).**catch**(addBcryptType);\
}).then(**function**(valid) {\
**if** (valid) {\
*// Login successful*\
} **else** {\
*// Login wrong*\
}\
});

*// You would handle errors something like this, but only at the
top-most point where it makes sense to do so:*\
Promise.**try**(**function**() {\
*// Generate or compare a hash here*\
}).then(**function**(result) {\
*// ... some other stuff ...*\
}).**catch**({type: "bcryptError"}, **function**(err) {\
*// Something went wrong with bcrypt*\
});

Alternative: Scrypt Hashing in Node.js

We recommend [scrypt for
humans](https://www.npmjs.com/package/scrypt-for-humans) ([Github](https://github.com/joepie91/scrypt-for-humans)),
a developer-friendly node-scrypt wrapper that's easy to use and hard to
misuse.

**var** Promise = **require**("bluebird");\
**var** scrypt = **require**("scrypt-for-humans");

*// Calculating a hash:*\
Promise.**try**(**function**() {\
**return** scrypt.hash(usersPassword);\
}).then(**function**(hash) {\
*// Store hash for long term use*\
});

*// Validating a hash:*\
Promise.**try**(**function**() {\
**return** scrypt.verifyHash(usersPassword, hash);\
}).then(**function**() {\
*// Login successful*\
}).**catch**(scrypt.PasswordError, **function**(err) {\
*// Login failed*\
});

(Example code made better by Sven Slootweg, the scrypt-for-humans
maintainer.)

Frequently Asked Questions

Where's Argon2?

Argon2 hasn't matured long enough to recommend *yet* (this opinion is
mostly due to an [attack on
Argon2i](http://permalink.gmane.org/gmane.comp.security.phc/3606) that
may or may not lead to their team recommending a new variant). As soon
as it has, libsodium will house a stable and usable implementation, so
our recommendation for libsodium covers that.

Where's PBKDF2?

Although PBKDF2 is more widely available than bcrypt or scrypt, it
doesn't offer the GPU resistance that we need from a password hashing
function. If you must use PBKDF2, make sure you use at
least100,000 iterations and a SHA2 family hash function.

Why prioritize bcrypt over scrypt?

On a technical level, they're vastly different, but for practical
purposes they're morally equivalent. The real weakness is in not using
an acceptable password hashing function at all. If you can use either of
these two, use it. They're both fine.

Our choice for bcrypt as the default was simply: In PHP (which
represents a little over 80% of the Internet), the easiest choice for
developers to implement in their applications is bcrypt (via the
password hashing API that shipped with PHP 5.5). Using scrypt requires
root access and the ability to install PHP extensions via PECL.

Why choose scrypt over bcrypt:

-   Bcrypt [truncates after 72 characters](https://3v4l.org/3G7mX).

-   Bcrypt [truncates on NUL bytes](https://3v4l.org/b3tOW).

-   (These aren't bugs in the PHP implementation. They're bugs in the
    > algorithm itself.)

Why choose bcrypt over scrypt:

-   Scrypt's memory hardness [isn't
    > perfect](http://blog.ircmaxell.com/2014/03/why-i-dont-recommend-scrypt.html)

-   Scrypt requires about 1000 times the memory as bcrypt for the same
    > security against GPU attacks

If you have to choose between the two for password hashing, you really
can't go wrong until Argon2 is ready for production. If you choose
bcrypt, however, passing a base64-encoded SHA-384 hash to bcrypt is
probably a good move:

-   base64\_encode(hash('sha384', \$password, true)) is 64 characters,
    > which nearly fills up the 72 character keyspace

<!-- -->

-   A base64-encoded hash is guaranteed to not contain NUL bytes

-   Two passwords with the same 72 character prefix but differ after the
    > 73rd character will, with overwhelming likelihood, produce
    > different SHA-384 hashes

-   SHA-384 has about 192 bits of birthday collision resistance

-   SHA-384 is also the largest SHA-2 family hash function that is
    > resistant to [length extension
    > attacks](https://blog.skullsecurity.org/2012/everything-you-need-to-know-about-hash-length-extension-attacks)

The above construction may invite theoretical concerns about entropy
reduction (i.e. 72 characters of raw binary without any NUL bytes comes
out to about 573 bits of possible entropy, but a SHA-384 hash outputs
are clearly limited to 384 bits).

A birthday SHA-384 collision still
requires 21922192 guesses. 21922192 is large enough to fall
under [boring
cryptography](http://cr.yp.to/talks/2015.10.05/slides-djb-20151005-a4.pdf),
barring any new attacks.

I'm not using bcrypt/scrypt. How should I migrate my legacy hashes?

The most straightforward approach to migrating your legacy hashes from,
e.g. MD5, to bcrypt/scrypt is to follow this strategy (which was first
introduced to us in a Reddit discussion
by [NeoThermic](https://www.reddit.com/r/PHP/comments/3lwxlw/hash_and_verify_passwords_in_php_the_right_way/cva6y6p)):

1.  Add a column to your user accounts table,
    > called legacy\_password (or equivalent).

2.  Calculate the bcrypt/scrypt/Argon2 hash of **the existing password
    > hashes** and store them in the database.

3.  Modify your authentication code to handle the legacy flag.

When a user attempts to login, first check if the legacy\_password flag
is set. If it is, first pre-hash their password with your old password
hashing algorithm, then use this prehashed value in place of their
password. Afterwards, *recalculate* the bcrypt hash and store the new
hash in the database, disabling the legacy\_password flag in the
process. A very loose example in PHP 7+ follows:

*/\*\*\
\* This is example code. Please feel free to use it for reference but
don't just copy/paste it.\
\*\
\* @param string \$username Unsafe user-supplied data: The username\
\* @param string \$password Unsafe user-supplied data: The password\
\* @return int The primary key for that user account\
\* @throws InvalidUserCredentialsException\
\*/*\
**public** **function** **authenticate**(string \$username, string
\$password): **int**\
{\
*// Database lookup*\
\$stmt = \$this-&gt;db-&gt;prepare("SELECT userid, passwordhash,
legacy\_password FROM user\_accounts WHERE username = ?");\
\$stmt-&gt;execute(\[\$username\]);\
\$stored = \$stmt-&gt;fetch(PDO::FETCH\_ASSOC);\
**if** (!\$stored) {\
*// No such user, throw an exception*\
**throw** **new** InvalidUserCredentialsException();\
}\
**if** (\$stored\['legacy\_password'\]) {\
*// This is the legacy password upgrade code*\
**if** (password\_verify(legacy\_hashing\_algorithm(\$password),
\$stored\['passwordhash'\])) {\
\$newhash = password\_hash(\$password, PASSWORD\_DEFAULT);\
\$stmt = \$this-&gt;db-&gt;prepare("UPDATE user\_accounts SET
passwordhash = ?, legacy\_password = FALSE WHERE userid = ?");\
\$stmt-&gt;execute(\[\$newhash, \$stored\['userid'\]\]);\
\
*// Return the user ID (integer)*\
**return** \$stored\['userid'\];\
}\
} **elseif** (password\_verify(\$password, \$stored\['passwordhash'\]))
{\
*// This is the general purpose upgrade code e.g. if a future version of
PHP upgrades to Argon2*\
**if** (password\_needs\_rehash(\$stored\['passwordhash'\],
PASSWORD\_DEFAULT)) {\
\$newhash = password\_hash(\$password, PASSWORD\_DEFAULT);\
\$stmt = \$this-&gt;db-&gt;prepare("UPDATE user\_accounts SET
passwordhash = ? WHERE userid = ?");\
\$stmt-&gt;execute(\[\$newhash, \$stored\['userid'\]\]);\
}\
*// Return the user ID (integer)*\
**return** \$stored\['userid'\];\
}\
*// When all else fails, throw an exception*\
**throw** **new** InvalidUserCredentialsException();\
}

Usage:

**try** {\
\$userid = \$this-&gt;authenticate(\$username, \$password);\
*// Update the session state*\
*// Redirect to the post-authentication landing page*\
} **catch** (InvalidUserCredentialsException \$e) {\
*// Log the failure*\
*// Redirect to the login form*\
}

Proactively upgrading legacy hashes is a security win over an
opportunistic strategy (rehashing when the user logs in, but leave the
insecure hashes in the database for inactive users): With a proactive
strategy, if your server gets compromised before everyone logs in again,
their passwords are already using an acceptable algorithm (bcrypt, in
the example code).

The above example code is also available
in [Bcrypt-SHA-384](https://gist.github.com/paragonie-scott/66469d391deef2e3b875) flavor.

What about password managers?

Password managers are a different beast. We're talking about server-side
password validation. You should [definitely use a password
manager](https://paragonie.com/blog/2015/06/guide-securing-your-business-s-online-presence-for-non-experts).

 

From
&lt;<https://paragonie.com/blog/2016/02/how-safely-store-password-in-2016>&gt;

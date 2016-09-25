 

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

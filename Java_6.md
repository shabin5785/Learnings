 

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

 

Wednesday, August 05, 2015

11:27

 

An exceptional condition is a problem that prevents the continuation of
the current method or scope. It’s important to distinguish an
exceptional condition from a normal problem, in which you have enough
information in the current context to somehow cope with the difficulty.
With an exceptional condition, you cannot continue processing because
you don’t have the information necessary to deal with the problem in the
current context. All you can do is jump out of the current context and
relegate that problem to a higher context. This is what happens when you
throw an exception. When you throw an exception, several things happen.
First, the exception object is created in the same way that any Java
object is created: on the heap, with new. Then the current path of
execution (the one you couldn’t continue) is stopped and the reference
for the exception object is ejected from the current context. At this
point the exception-handling mechanism takes over and begins to look for
an appropriate place to continue executing the program. This appropriate
place is the exception handler, whose job is to recover from the problem
so the program can either try another tack or just continue.

 

Exceptions allow you to (if nothing else) force the program to stop and
tell you what went wrong, or (ideally) force the program to deal with
the problem and return to a stable state.

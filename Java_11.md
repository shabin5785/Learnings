 

Wednesday, August 05, 2015

11:00

 

The java.util library has a reasonably complete set of container classes
to solve this problem, the basic types of which are List, Set, Queue,
and Map. These types of objects are also known as **collection**
classes. Among their other characteristics—Set, for example, holds only
one object of each value, and Map is an associative array that lets you
associate objects with other objects—the Java container classes will
automatically resize themselves.

 

**Generics and type-safe containers**

One of the problems of using pre-Java SE5 containers was that the
compiler allowed you to insert an incorrect type into a container. For
example, consider a container of Apple objects, using the basic
workhorse container, ArrayList. ArrayList also has a method size( ) to
let you know how many elements have been added, so that you don’t
inadvertently index off the end and cause an error. In this example,
Apples and Oranges are placed into the container, then pulled out.
Normally, the Java compiler will give you a warning because the example
does not use generics. The classes Apple and Orange are distinct; they
have nothing in common except that they are both Objects. Since
ArrayList holds Objects, you can not only add Apple objects into this
container using the ArrayList method add( ), but you can also add Orange
objects without complaint at either compile time or run time. When you
go to fetch out what you think are Apple objects using the ArrayList
method get( ), you get back a reference to an Object that you must cast
to an Apple. At run time, when you try to cast the Orange object to an
Apple, you’ll get an error in the form of the aforementioned exception.

 

Applying predefined generic classes is usually straightforward. For
example, to define an ArrayList intended to hold Apple objects, you say
ArrayList&lt;Apple&gt; instead of just ArrayList. The angle brackets
surround the type parameters (there may be more than one), which specify
the type(s) that can be held by that instance of the container. **With
generics, you’re prevented, at compile time**, from putting the wrong
type of object into a container. Also notice that the cast is no longer
necessary when fetching items back out from the List. Since the List
knows what type it holds, it does the cast for you when you call get().

 

You are not limited to putting the exact type of object into a container
when you specify that type as a generic parameter. Upcasting works the
same with generics as it does with other types. Thus, you can add a
subtype of Apple to a container that is specified to hold Apple objects

 

**Collection**: a sequence of individual elements with one or more rules
applied to them. A List must hold the elements in the way that they were
inserted, a Set cannot have duplicate elements, and a Queue produces the
elements in the order determined by a queuing discipline

 

**Map**: a group of key-value object pairs, allowing you to look up a
value using a key. An ArrayList allows you to look up an object using a
number, so in a sense it associates numbers to objects. A map allows you
to look up an object using another object. It’s also called an
associative array, because it associates objects with other objects, or
a dictionary, because you look up a value object using a key object just
like you look up a definition using a word.: a group of key-value object
pairs, allowing you to look up a value using a key. An ArrayList allows
you to look up an object using a number, so in a sense it associates
numbers to objects. A map allows you to look up an object using another
object. It’s also called an associative array, because it associates
objects with other objects, or a dictionary, because you look up a value
object using a key object just like you look up a definition using a
word.

 

It’s also possible to use the output of Arrays.asList( ) directly, as a
List, but the underlying representation in this case is the array, which
cannot be resized. If you try to add( ) or delete( ) elements in such a
list, that would attempt to change the size of an array, so you’ll get
an "Unsupported Operation" error at run time.

 

A limitation of Arrays.asList( ) is that it takes a best guess about the
resulting type of the List, and doesn’t pay attention to what you’re
assigning it to. it’s possible to insert a "hint" in the middle of
Arrays.asList( ), to tell the compiler what the actual target type
should be for the resulting List type produced by Arrays.asList( ).
(Page 303)

 

**ArrayList and LinkedList** are both types of List, and you can see
from the output that they both hold elements in the same order in which
they are inserted. The difference between the two is not only
performance for certain types of operations, but also that a LinkedList
contains more operations than an ArrayList

 

**Why not sorted list **

Because all lists are already sorted by its order.

You can "resort" them with another ordering
using java.util.Collections.sort().

EDIT:

Lists as data structures are based in what is interesting is the
ordering in which the items where inserted.

Sets do not have that information.

If you want to order by addition time, use List. If you want to order by
other criteria, use SortedSet

 

From
&lt;<http://stackoverflow.com/questions/8725387/why-is-there-no-sortedlist-in-java>&gt;

 

 

 

**HashSet, TreeSet and LinkedHashSet** are types of Set. The output
shows that a Set will only hold one of each identical item, but it also
shows that the different Set implementations store the elements
differently. If storage order is important, you can use a TreeSet, which
keeps the objects in ascending comparison order, or a LinkedHashSet,
which keeps the objects in the order in which they were added

 

A **Map** (also called an associative array) allows you to look up an
object using a key, like a simple database. The associated object is
called a value

 

***List***

Lists promise to maintain elements in a particular sequence. The List
interface adds a number of methods to Collection that allow insertion
and removal of elements in the middle of a List.

 

•The basic ArrayList, which excels at randomly accessing elements, but
is slower when inserting and removing elements in the middle of a List.

•The LinkedList, which provides optimal sequential access, with
inexpensive insertions and deletions from the middle of the List. A
LinkedList is relatively slow for random access, but it has a larger
feature set than the ArrayList

 

The subList( ) method allows you to easily create a slice out of a
larger list, and this naturally produces a true result when passed to
containsAll( ) for that larger list. It’s also interesting to note that
order is unimportant—you can see in output lines 11 and 12 that calling
the intuitively named Collections.sort( ) and Collections.shuffle( ) on
sub doesn’t affect the outcome of containsAll( ). subList( ) produces a
list backed by the original list. Therefore, changes in the returned
list are reflected in the original list, and vice versa

 

***Iterator***

 

The concept of an Iterator (another design pattern) can be used to
achieve this abstraction. An iterator is an object whose job is to move
through a sequence and select each object in that sequence without the
client programmer knowing or caring about the underlying structure of
that sequence. In addition, an iterator is usually what’s called a
lightweight object: one that’s cheap to create

 

1.Ask a Collection to hand you an Iterator using a method called
iterator( ). That Iterator will be ready to return the first element in
the sequence.

2.Get the next object in the sequence with next( ).

3.See if there are any more objects in the sequence with hasNext( ).

4.Remove the last element returned by the iterator with remove( ).

 

**ListIterator**

The ListIterator is a more powerful subtype of Iterator that is produced
only by List classes. While Iterator can only move forward, ListIterator
is bidirectional. It can also produce the indexes of the next and
previous elements relative to where the iterator is pointing in the
list, and it can replace the last element that it visited using the set(
) method. You can produce a ListIterator that points to the beginning of
the List by calling listIterator( ), and you can also create a
ListIterator that starts out pointing to an index n in the list by
calling listIterator(n).

 

***LinkedList***

The LinkedList also implements the basic List interface like ArrayList
does, but it performs certain operations (insertion and removal in the
middle of the List) more efficiently than does ArrayList. Conversely, it
is less efficient for random-access operations. LinkedList also adds
methods that allow it to be used as a stack, a Queue or a double-ended
queue (deque).

getFirst( ) and element( ) are identical—they return the head (first
element) of the list without removing it, and throw
NoSuchElementException if the List is empty. peek( ) is a slight
variation of those two that returns null if the list is empty

 

***Stack***

A stack is sometimes referred to as a "last-in, first-out" (LIFO)
container. It’s sometimes called a pushdown stack, because whatever you
"push" on the stack last is the first item you can "pop" off of the
stack.

 

***Set***

A Set refuses to hold more than one instance of each object value. If
you try to add more than one instance of an equivalent object, the Set
prevents duplication. Set has the same interface as Collection, so there
isn’t any extra functionality like there is in the two different types
of List. Instead, the Set is exactly a Collection—it just has different
behavior. A Set determines membership based on the "value" of an object.
**HashSet** uses hashing for speed. The order maintained by a HashSet is
different from a TreeSet or a LinkedHashSet, since each implementation
has a different way of storing elements. TreeSet keeps elements sorted
into a red-black tree data structure, whereas HashSet uses the hashing
function. LinkedHashSet also uses hashing for lookup speed, but appears
to maintain elements in insertion order using a linked list.

 

***Map***

Maps, like arrays and Collections, can easily be expanded to multiple
dimensions; you simply make a Map whose values are Maps

 

***Queue***

A queue is typically a “first-in, first-out" (FIFO) container. That is,
you put things in at one end and pull them out at the other, and the
order in which you put them in will be the same order in which they come
out. Queues are commonly used as a way to reliably transfer objects from
one area of a program to another. Queues are especially important in
concurrent programming. offer( ) is one of the Queue-specific methods;
it inserts an element at the tail of the queue if it can, or returns
false

 

***PriorityQueue***

First-in, first-out (FIFO) describes the most typical queuing
discipline. A queuing discipline is what decides, given a group of
elements in the queue, which one goes next. First-in, first-out says
that the next element should be the one that was waiting the longest.
Apriority queue says that the element that goes next is the one with the
greatest need (the highest priority).

When you offer( ) an object onto a PriorityQueue, that object is sorted
into the queue.5 The default sorting uses the natural order of the
objects in the queue, but you can modify the order by providing your own
Comparator. The PriorityQueue ensures that when you call peek( ), poll(
) or remove( ), the element you get will be the one with the highest
priority

 

**Collection** is the root interface that describes what is common for
all sequence containers. implementing Collection also means providing an
iterator( ) method: In addition, the java.utiLAbstractCollection class
provides a default implementation for a Collection, so that you can
create a new subtype of AbstractCollection without unnecessary code
duplication. So if I write a method that takes a Collection, that method
can be applied to any type that implements Collection—and this allows a
new class to choose to implement Collection in order to be used with my
method

 

![](media/image1.png){width="9.875in" height="4.114583333333333in"}

 

 

The dotted boxes represent interfaces, and the solid boxes are regular
(concrete) classes. The dotted lines with hollow arrows indicate that a
particular class is implementing an interface. The solid arrows show
that a class can produce objects of the class the arrow is pointing to

Pattern & Description

Tuesday, September 01, 2015

09:57

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  1   **Creational Patterns**
      
      These design patterns provide a way to create objects while hiding the creation logic, rather than instantiating objects directly using new opreator. This gives program more flexibility in deciding which objects need to be created for a given use case.
  --- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  2   **Structural Patterns**
      
      These design patterns concern class and object composition. Concept of inheritance is used to compose interfaces and define ways to compose objects to obtain new functionalities.

  3   **Behavioral Patterns**
      
      These design patterns are specifically concerned with communication between objects.

  4   **J2EE Patterns**
      
      These design patterns are specifically concerned with the presentation tier. These patterns are identified by Sun Java Center.
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

Creational patterns

 

A creational pattern abstracts the process of instantiation, separating
how objects are created, composed, and represented from the code that
relies on them. Class creational patterns use inheritance to vary the
classes that are instantiated, and object creational patterns delegate
instantiation to other objects.

 

**Abstract factory:** This pattern provides an interface to encapsulate
a group of individual factories that have a common theme without
specifying their concrete classes.

 

**Builder**: Separates the construction of a complex object from its
representation, enabling the same construction process to create various
representations. Abstracting the steps of object construction allows
different implementations of the steps to construct different
representations of the objects.

 

**Factory method**: Defines an interface for creating an object, but
lets subclasses decide which class to instantiate. This pattern lets a
class defer instantiation to subclasses. Dependency injection is a
related pattern.

 

**Lazy initialization**: This pattern gives us a way to delay object
creation, database lookup, or another expensive process until the first
time the result is needed.

 

**Multiton**: Expands on the singleton concept to manage a map of named
class instances as key-value pairs, and provides a global point of
access to them.

 

**Object pool:** Keep a set of initialized objects ready to use, rather
than be allocated and destroyed on demand. The intent is to avoid
expensive resource acquisition and reclamation by recycling objects that
are no longer in use.

 

**Prototype**: Specifies the kinds of objects to create using a
prototypical instance, then create new objects by copying this
prototype. The prototypical instance is cloned to generate new objects.

 

**Resource acquisition is initialization**: This pattern ensures that
resources are automatically and properly initialized and reclaimed by
tying them to the lifespan of suitable objects. Resources are acquired
during object initialization, when there is no chance of them being used
before they are available, and released with the destruction of the same
objects, which is guaranteed to take place even in the case of errors.

 

**Singleton**: Ensures that a class has only one instance and provides a
global point of access to this instance.

 

 

Structural patterns

 

A structural pattern teaches us how to compose classes and objects to
form larger structures. A structural class pattern relies on inheritance
to compose a resulting interface or implementation (for example,
multiple inheritance mixes two or more classes into one class). A
structural object pattern composes various objects to obtain new
functionality;

 

**Adapter**: Converts a class's interface into another interface that
clients expect. An adapter lets classes work together that otherwise
couldn't due to incompatible interfaces. It does so by providing its
interface to clients while using the original class interfaces
internally. Adapter is also known as the Wrapper pattern.

 

**Bridge**: Decouples an abstraction from its implementation, which lets
the two vary independently. The bridge uses encapsulation, aggregation,
and can also use inheritance to separate responsibilities into different
classes.

 

**Composite**: Composes objects into tree structures that represent
part-whole hierarchies. Composite lets clients treat individual objects
and compositions of objects uniformly.

 

**Decorator**: Dynamically attaches additional responsibilities to an
object while maintaining the same interface. Decorators provide a
flexible alternative to subclassing for extending functionality.

 

**Facade**: Provides a unified interface to a set of interfaces in a
subsystem. Facade defines a higher-level interface that makes the
subsystem easier to use. Facades can wrap poorly-designed APIs in a
single well-defined API.

 

**Flyweight**: Uses sharing to support large numbers of similar objects
efficiently. A flyweight is an object that minimizes memory use by
sharing as much data as possible with other similar objects. It offers a
way to use objects in large numbers when a simple repeated
representation would result in an unacceptable amount of allocated
memory.

 

**Front controller**: Provides a centralized entry point for handling
requests. This pattern relates to the design of Web applications.

Module: Implements the concept of software modules, defined by modular
programming, in a programming language that does not support or only
partly supports modules.

 

**Proxy**: Provides a surrogate or placeholder object for another
object. This proxy controls access to the other object.

 

Behavioral patterns

 

Behavioral patterns focus on algorithms and the assignment of
responsibilities between objects. They address object or class patterns
as well as the communication patterns between them. A behavioral class
pattern uses inheritance to distribute behavior among classes. In
contrast, a behavioral object pattern uses object composition.

 

**Blackboard**: This is a generalization of the Observer pattern that
supports multiple readers and writers. The Blackboard pattern
communicates information systemwide.

 

**Chain of responsibility**: Avoids coupling the sender of a request to
its receiver by giving more than one object a chance to handle the
request. This pattern chains together receiving objects and passes a
request along the chain until an object handles the request.

 

**Command**: Uses an object to encapsulate all information needed to
call a method at a later time. This information includes the method
name, the object that owns the method, and values for the method
parameters. A client instantiates the command object and provides the
information required to call the method. The invoker decides when the
method should be called. Finally, the receiver is an instance of the
class that contains the method's code.

 

**Interpreter**: Given a language, defines a representation for its
grammar along with an interpreter that uses the representation to
interpret sentences in the language.

 

**Iterator**: Enables developers to access the elements of an aggregate
object sequentially without exposing its underlying representation.

 

**Mediator**: Defines an object that encapsulates how a set of objects
interact. Mediator promotes loose coupling by keeping objects from
referring to each other explicitly, and it lets you vary their
interaction independently.

 

**Memento**: Without violating encapsulation, captures and externalizes
an object's internal state so that the object can be subsequently
restored to this state.

 

**Null Object**: Avoids null references by providing a default object.

 

**Observer**: Defines a one-to-many dependency between objects where a
state change in one object results in all of its dependents being
notified and updated automatically. Observer is also known as the
Publish-subscribe pattern.

 

**Servant**: Defines functionality for a group of classes without
defining that functionality in each of those classes. A servant is a
class whose instance (or the class itself) provides methods that perform
a desired service, while objects for which (or with whom) the servant
does something are passed to servant methods as parameters.

 

**Specification**: Recombines business rules by chaining the business
rules together using Boolean logic.

 

**State**: Allows an object to alter its behavior when its internal
state changes. The object will appear to change its class.

 

**Strategy**: Defines a family of algorithms, encapsulates each one, and
makes them interchangeable. Strategy lets the algorithm vary
independently from clients that use it.

 

**Template method**: Defines the skeleton of an algorithm in an
operation, deferring some steps to subclasses. Template method lets
subclasses redefine certain steps of an algorithm without changing the
algorithm's structure.

 

**Visitor**: Represents an operation to be performed on the elements of
an object structure. Visitor lets you define a new operation without
changing the classes of the elements on which it operates.

 

>  

Concurrency patterns

 

Finally, a concurrency pattern addresses some aspect of multithreaded
programming. One well-known pattern in this category is
Producer-consumer, in which a producer thread stores an item in a shared
buffer and a consumer thread retrieves this item. The producer thread
must not store another item in this buffer until the previous item has
been consumed, and the consumer thread must not consume a non-existent
item.

 

 

**Active object**: Decouples method execution from method invocation for
objects in which each object resides in its own thread of control. The
goal is to introduce concurrency, by using asynchronous method
invocation and a scheduler for handling requests

 

**Balking**: Only executes an action on an object when the object is in
a particular state. For example, an object reads a file and provides
methods to access file content. When the file is not open and an attempt
is made to call a method to access content, the object "balks" at the
request.

 

**Binding properties:** Combines multiple observers to force properties
in different objects to be synchronized or coordinated in some way.

 

**Double-checked locking**: Reduces the overhead of acquiring a lock by
first testing the locking criterion (the "lock hint") without actually
acquiring the lock. The lock is acquired only when the locking criterion
check indicates that locking is required.

 

**Event-based asynchronous**: A concurrency pattern for the asynchronous
invocation of an object's potentially long-running methods.

 

**Guarded suspension:** Manages operations that require both a lock to
be acquired and a precondition to be satisfied before the operation can
be executed.

 

**Lock**: A mechanism to temporarily make some aspect of an object
unmodifiable or to suppress unneeded update notifications.

 

**Messaging design pattern (MDP)**: Allows the interchange of
information (that is, messages) between components and applications.

 

**Monitor object**: An object whose methods are subject to mutual
exclusion, thus preventing multiple objects from erroneously trying to
use it at the same time.

 

**Reactor**: An event-handling pattern for handling service requests
delivered concurrently to a service handler by one or more inputs. The
service handler then demultiplexes the incoming requests and dispatches
them synchronously to the associated request handlers.

 

**Read-write lock**: A lock that allows concurrent read access to an
object, but requires exclusive access for write operations.

 

**Scheduler**: A concurrency pattern used to explicitly control when
threads may execute single-threaded code; for example, multiple threads
wanting to write data to the same file.

 

**Thread pool**: A concurrency pattern in which a number of threads are
created to perform various tasks, which are usually organized in a
queue. Typically, there are many more tasks than threads. Thread Pool
can be considered a special case of the Object Pool creational pattern.

 

**Thread-specific storage**: A concurrency pattern in which static or
global memory is localized to a thread. Each thread has its own copy of
this memory.

 

 

 

Factory Pattern

Tuesday, September 01, 2015

10:20

 

In Factory pattern, we create object without exposing the creation logic
to the client and refer to newly created object using a common
interface.

 

We're going to create a Shape interface and concrete classes
implementing the Shape interface. A factory class ShapeFactory is
defined as a next step.FactoryPatternDemo, our demo class will use
ShapeFactory to get a Shape object. It will pass information (CIRCLE /
RECTANGLE / SQUARE) to ShapeFactory to get the type of object it needs.

 

> ![](media/image1.jpg){width="6.645833333333333in"
> height="3.3854166666666665in"}

 

 

Step 1

Create an interface.

*Shape.java*

public interface Shape {\
void draw();\
}

Step 2

Create concrete classes implementing the same interface.

*Rectangle.java*

public class Rectangle implements Shape {

@Override\
public void draw() {\
System.out.println("Inside Rectangle::draw() method.");\
}\
}

*Square.java*

public class Square implements Shape {

@Override\
public void draw() {\
System.out.println("Inside Square::draw() method.");\
}\
}

*Circle.java*

public class Circle implements Shape {

@Override\
public void draw() {\
System.out.println("Inside Circle::draw() method.");\
}\
}

Step 3

Create a Factory to generate object of concrete class based on given
information.

*ShapeFactory.java*

public class ShapeFactory {\
        \
//use getShape method to get object of type shape\
public Shape getShape(String shapeType){\
if(shapeType == null){\
return null;\
}                \
if(shapeType.equalsIgnoreCase("CIRCLE")){\
return new Circle();\
\
} else if(shapeType.equalsIgnoreCase("RECTANGLE")){\
return new Rectangle();\
\
} else if(shapeType.equalsIgnoreCase("SQUARE")){\
return new Square();\
}\
\
return null;\
}\
}

Step 4

Use the Factory to get object of concrete class by passing an
information such as type.

*FactoryPatternDemo.java*

public class FactoryPatternDemo {

public static void main(String\[\] args) {\
ShapeFactory shapeFactory = new ShapeFactory();

//get an object of Circle and call its draw method.\
Shape shape1 = shapeFactory.getShape("CIRCLE");

//call draw method of Circle\
shape1.draw();

//get an object of Rectangle and call its draw method.\
Shape shape2 = shapeFactory.getShape("RECTANGLE");

//call draw method of Rectangle\
shape2.draw();

//get an object of Square and call its draw method.\
Shape shape3 = shapeFactory.getShape("SQUARE");

//call draw method of circle\
shape3.draw();\
}\
}

 

 

 

Abstract Factory Pattern

Tuesday, September 01, 2015

10:22

 

In Abstract Factory pattern an interface is responsible for creating a
factory of related objects without explicitly specifying their classes.
Each generated factory can give the objects as per the Factory pattern.

 

Implementation

We are going to create a Shape and Color interfaces and concrete classes
implementing these interfaces. We create an abstract factory class
AbstractFactory as next step. Factory classes ShapeFactory and
ColorFactory are defined where each factory extends AbstractFactory. A
factory creator/generator class FactoryProducer is created.
AbstractFactoryPatternDemo, our demo class uses FactoryProducer to get a
AbstractFactory object. It will pass information (CIRCLE / RECTANGLE /
SQUARE for Shape) to AbstractFactory to get the type of object it needs.
It also passes information (RED / GREEN / BLUE for Color) to
AbstractFactory to get the type of object it needs.

 

> ![](media/image2.jpg){width="7.458333333333333in"
> height="4.552083333333333in"}

 

Step 1

Create an interface for Shapes.

*Shape.java*

public interface Shape {\
void draw();\
}

Step 2

Create concrete classes implementing the same interface.

*Rectangle.java*

public class Rectangle implements Shape {

@Override\
public void draw() {\
System.out.println("Inside Rectangle::draw() method.");\
}\
}

*Square.java*

public class Square implements Shape {

@Override\
public void draw() {\
System.out.println("Inside Square::draw() method.");\
}\
}

*Circle.java*

public class Circle implements Shape {

@Override\
public void draw() {\
System.out.println("Inside Circle::draw() method.");\
}\
}

Step 3

Create an interface for Colors.

*Color.java*

public interface Color {\
void fill();\
}

Step4

Create concrete classes implementing the same interface.

*Red.java*

public class Red implements Color {

@Override\
public void fill() {\
System.out.println("Inside Red::fill() method.");\
}\
}

*Green.java*

public class Green implements Color {

@Override\
public void fill() {\
System.out.println("Inside Green::fill() method.");\
}\
}

*Blue.java*

public class Blue implements Color {

@Override\
public void fill() {\
System.out.println("Inside Blue::fill() method.");\
}\
}

Step 5

Create an Abstract class to get factories for Color and Shape Objects.

*AbstractFactory.java*

public abstract class AbstractFactory {\
abstract Color getColor(String color);\
abstract Shape getShape(String shape) ;\
}

Step 6

Create Factory classes extending AbstractFactory to generate object of
concrete class based on given information.

*ShapeFactory.java*

public class ShapeFactory extends AbstractFactory {\
        \
@Override\
public Shape getShape(String shapeType){\
\
if(shapeType == null){\
return null;\
}                \
\
if(shapeType.equalsIgnoreCase("CIRCLE")){\
return new Circle();\
\
}else if(shapeType.equalsIgnoreCase("RECTANGLE")){\
return new Rectangle();\
\
}else if(shapeType.equalsIgnoreCase("SQUARE")){\
return new Square();\
}\
\
return null;\
}\
\
@Override\
Color getColor(String color) {\
return null;\
}\
}

*ColorFactory.java*

public class ColorFactory extends AbstractFactory {\
        \
@Override\
public Shape getShape(String shapeType){\
return null;\
}\
\
@Override\
Color getColor(String color) {\
\
if(color == null){\
return null;\
}                \
\
if(color.equalsIgnoreCase("RED")){\
return new Red();\
\
}else if(color.equalsIgnoreCase("GREEN")){\
return new Green();\
\
}else if(color.equalsIgnoreCase("BLUE")){\
return new Blue();\
}\
\
return null;\
}\
}

Step 7

Create a Factory generator/producer class to get factories by passing an
information such as Shape or Color

*FactoryProducer.java*

public class FactoryProducer {\
public static AbstractFactory getFactory(String choice){\
\
if(choice.equalsIgnoreCase("SHAPE")){\
return new ShapeFactory();\
\
}else if(choice.equalsIgnoreCase("COLOR")){\
return new ColorFactory();\
}\
\
return null;\
}\
}

Step 8

Use the FactoryProducer to get AbstractFactory in order to get factories
of concrete classes by passing an information such as type.

*AbstractFactoryPatternDemo.java*

public class AbstractFactoryPatternDemo {\
public static void main(String\[\] args) {

//get shape factory\
AbstractFactory shapeFactory = FactoryProducer.getFactory("SHAPE");

//get an object of Shape Circle\
Shape shape1 = shapeFactory.getShape("CIRCLE");

//call draw method of Shape Circle\
shape1.draw();

//get an object of Shape Rectangle\
Shape shape2 = shapeFactory.getShape("RECTANGLE");

//call draw method of Shape Rectangle\
shape2.draw();\
\
//get an object of Shape Square\
Shape shape3 = shapeFactory.getShape("SQUARE");

//call draw method of Shape Square\
shape3.draw();

//get color factory\
AbstractFactory colorFactory = FactoryProducer.getFactory("COLOR");

//get an object of Color Red\
Color color1 = colorFactory.getColor("RED");

//call fill method of Red\
color1.fill();

//get an object of Color Green\
Color color2 = colorFactory.getColor("Green");

//call fill method of Green\
color2.fill();

//get an object of Color Blue\
Color color3 = colorFactory.getColor("BLUE");

//call fill method of Color Blue\
color3.fill();\
}\
}

 

 

 

 

 

Singleton Pattern

Tuesday, September 01, 2015

10:31

 

This pattern involves a single class which is responsible to create an
object while making sure that only single object gets created. This
class provides a way to access its only object which can be accessed
directly without need to instantiate the object of the class.

 

Implementation

We're going to create a SingleObject class. SingleObject class have its
constructor as private and have a static instance of itself.
SingleObject class provides a static method to get its static instance
to outside world. SingletonPatternDemo, our demo class will use
SingleObject class to get a SingleObject object.

 

> ![](media/image3.jpg){width="3.9895833333333335in"
> height="4.177083333333333in"}

 

 

Step 1

Create a Singleton Class.

*SingleObject.java*

public class SingleObject {

//create an object of SingleObject\
private static SingleObject instance = new SingleObject();

//make the constructor private so that this class cannot be\
//instantiated\
private SingleObject(){}

//Get the only object available\
public static SingleObject getInstance(){\
return instance;\
}

public void showMessage(){\
System.out.println("Hello World!");\
}\
}

Step 2

Get the only object from the singleton class.

*SingletonPatternDemo.java*

public class SingletonPatternDemo {\
public static void main(String\[\] args) {

//illegal construct\
//Compile Time Error: The constructor SingleObject() is not visible\
//SingleObject object = new SingleObject();

//Get the only object available\
SingleObject object = SingleObject.getInstance();

//show the message\
object.showMessage();\
}\
}

 

 

 

Builder Pattern

Tuesday, September 01, 2015

10:32

 

A Builder class builds the final object step by step. This builder is
independent of other objects.

 

Implementation

We have considered a business case of fast-food restaurant where a
typical meal could be a burger and a cold drink. Burger could be either
a Veg Burger or Chicken Burger and will be packed by a wrapper. Cold
drink could be either a coke or pepsi and will be packed in a bottle. We
are going to create an Item interface representing food items such as
burgers and cold drinks and concrete classes implementing the Item
interface and a Packing interface representing packaging of food items
and concrete classes implementing the Packing interface as burger would
be packed in wrapper and cold drink would be packed as bottle. We then
create a Meal class having ArrayList of Item and a MealBuilder to build
different types of Meal objects by combining Item. BuilderPatternDemo,
our demo class will use MealBuilder to build a Meal.

 

> ![](media/image4.jpg){width="5.833333333333333in" height="4.25in"}

 

Step 1

Create an interface Item representing food item and packing.

*Item.java*

public interface Item {\
public String name();\
public Packing packing();\
public float price();        \
}

*Packing.java*

public interface Packing {\
public String pack();\
}

Step 2

Create concrete classes implementing the Packing interface.

*Wrapper.java*

public class Wrapper implements Packing {

@Override\
public String pack() {\
return "Wrapper";\
}\
}

*Bottle.java*

public class Bottle implements Packing {

@Override\
public String pack() {\
return "Bottle";\
}\
}

Step 3

Create abstract classes implementing the item interface providing
default functionalities.

*Burger.java*

public abstract class Burger implements Item {

@Override\
public Packing packing() {\
return new Wrapper();\
}

@Override\
public abstract float price();\
}

*ColdDrink.java*

public abstract class ColdDrink implements Item {

@Override\
        public Packing packing() {\
return new Bottle();\
        }

@Override\
        public abstract float price();\
}

Step 4

Create concrete classes extending Burger and ColdDrink classes

*VegBurger.java*

public class VegBurger extends Burger {

@Override\
public float price() {\
return 25.0f;\
}

@Override\
public String name() {\
return "Veg Burger";\
}\
}

*ChickenBurger.java*

public class ChickenBurger extends Burger {

@Override\
public float price() {\
return 50.5f;\
}

@Override\
public String name() {\
return "Chicken Burger";\
}\
}

*Coke.java*

public class Coke extends ColdDrink {

@Override\
public float price() {\
return 30.0f;\
}

@Override\
public String name() {\
return "Coke";\
}\
}

*Pepsi.java*

public class Pepsi extends ColdDrink {

@Override\
public float price() {\
return 35.0f;\
}

@Override\
public String name() {\
return "Pepsi";\
}\
}

Step 5

Create a Meal class having Item objects defined above.

*Meal.java*

import java.util.ArrayList;\
import java.util.List;

public class Meal {\
private List&lt;Item&gt; items = new ArrayList&lt;Item&gt;();        

public void addItem(Item item){\
items.add(item);\
}

public float getCost(){\
float cost = 0.0f;\
\
for (Item item : items) {\
cost += item.price();\
}                \
return cost;\
}

public void showItems(){\
\
for (Item item : items) {\
System.out.print("Item : " + item.name());\
System.out.print(", Packing : " + item.packing().pack());\
System.out.println(", Price : " + item.price());\
}                \
}        \
}

Step 6

Create a MealBuilder class, the actual builder class responsible to
create Meal objects.

*MealBuilder.java*

public class MealBuilder {

public Meal prepareVegMeal (){\
Meal meal = new Meal();\
meal.addItem(new VegBurger());\
meal.addItem(new Coke());\
return meal;\
}

public Meal prepareNonVegMeal (){\
Meal meal = new Meal();\
meal.addItem(new ChickenBurger());\
meal.addItem(new Pepsi());\
return meal;\
}\
}

Step 7

BuiderPatternDemo uses MealBuider to demonstrate builder pattern.

*BuilderPatternDemo.java*

public class BuilderPatternDemo {\
public static void main(String\[\] args) {\
\
MealBuilder mealBuilder = new MealBuilder();

Meal vegMeal = mealBuilder.prepareVegMeal();\
System.out.println("Veg Meal");\
vegMeal.showItems();\
System.out.println("Total Cost: " + vegMeal.getCost());

Meal nonVegMeal = mealBuilder.prepareNonVegMeal();\
System.out.println("\\n\\nNon-Veg Meal");\
nonVegMeal.showItems();\
System.out.println("Total Cost: " + nonVegMeal.getCost());\
}\
}

 

 

 

Prototype Pattern

Tuesday, September 01, 2015

10:35

 

This pattern involves implementing a prototype interface which tells to
create a clone of the current object. This pattern is used when creation
of object directly is costly. For example, an object is to be created
after a costly database operation. We can cache the object, returns its
clone on next request and update the database as and when needed thus
reducing database calls.

 

Implementation

We're going to create an abstract class Shape and concrete classes
extending the Shape class. A class ShapeCache is defined as a next step
which stores shape objects in a Hashtable and returns their clone when
requested. PrototypPatternDemo, our demo class will use ShapeCache class
to get a Shape object.

 

> ![](media/image5.jpg){width="5.833333333333333in"
> height="3.8333333333333335in"}

 

Step 1

Create an abstract class implementing *Clonable* interface.

*Shape.java*

public abstract class Shape implements Cloneable {\
\
private String id;\
protected String type;\
\
abstract void draw();\
\
public String getType(){\
return type;\
}\
\
public String getId() {\
return id;\
}\
\
public void setId(String id) {\
this.id = id;\
}\
\
public Object clone() {\
Object clone = null;\
\
try {\
clone = super.clone();\
\
} catch (CloneNotSupportedException e) {\
e.printStackTrace();\
}\
\
return clone;\
}\
}

Step 2

Create concrete classes extending the above class.

*Rectangle.java*

public class Rectangle extends Shape {

public Rectangle(){\
type = "Rectangle";\
}

@Override\
public void draw() {\
System.out.println("Inside Rectangle::draw() method.");\
}\
}

*Square.java*

public class Square extends Shape {

public Square(){\
type = "Square";\
}

@Override\
public void draw() {\
System.out.println("Inside Square::draw() method.");\
}\
}

*Circle.java*

public class Circle extends Shape {

public Circle(){\
type = "Circle";\
}

@Override\
public void draw() {\
System.out.println("Inside Circle::draw() method.");\
}\
}

Step 3

Create a class to get concrete classes from database and store them in
a *Hashtable*.

*ShapeCache.java*

import java.util.Hashtable;

public class ShapeCache {\
        \
private static Hashtable&lt;String, Shape&gt; shapeMap = new
Hashtable&lt;String, Shape&gt;();

public static Shape getShape(String shapeId) {\
Shape cachedShape = shapeMap.get(shapeId);\
return (Shape) cachedShape.clone();\
}

// for each shape run database query and create shape\
// shapeMap.put(shapeKey, shape);\
// for example, we are adding three shapes\
\
public static void loadCache() {\
Circle circle = new Circle();\
circle.setId("1");\
shapeMap.put(circle.getId(),circle);

Square square = new Square();\
square.setId("2");\
shapeMap.put(square.getId(),square);

Rectangle rectangle = new Rectangle();\
rectangle.setId("3");\
shapeMap.put(rectangle.getId(), rectangle);\
}\
}

Step 4

*PrototypePatternDemo* uses *ShapeCache* class to get clones of shapes
stored in a*Hashtable*.

*PrototypePatternDemo.java*

public class PrototypePatternDemo {\
public static void main(String\[\] args) {\
ShapeCache.loadCache();

Shape clonedShape = (Shape) ShapeCache.getShape("1");\
System.out.println("Shape : " + clonedShape.getType());                

Shape clonedShape2 = (Shape) ShapeCache.getShape("2");\
System.out.println("Shape : " + clonedShape2.getType());                

Shape clonedShape3 = (Shape) ShapeCache.getShape("3");\
System.out.println("Shape : " +
clonedShape3.getType());                \
}\
}

 

 

 

Adapter Pattern

Tuesday, September 01, 2015

10:37

This pattern involves a single class which is responsible to join
functionalities of independent or incompatible interfaces. A real life
example could be a case of card reader which acts as an adapter between
memory card and a laptop. You plugin the memory card into card reader
and card reader into the laptop so that memory card can be read via
laptop.

 

Implementation

We have a MediaPlayer interface and a concrete class AudioPlayer
implementing the MediaPlayer interface. AudioPlayer can play mp3 format
audio files by default. We are having another interface
AdvancedMediaPlayer and concrete classes implementing the
AdvancedMediaPlayer interface. These classes can play vlc and mp4 format
files. We want to make AudioPlayer to play other formats as well. To
attain this, we have created an adapter class MediaAdapter which
implements the MediaPlayer interface and uses AdvancedMediaPlayer
objects to play the required format. AudioPlayer uses the adapter class
MediaAdapter passing it the desired audio type without knowing the
actual class which can play the desired format. AdapterPatternDemo, our
demo class will use AudioPlayer class to play various formats.

 

> ![](media/image6.jpg){width="5.833333333333333in" height="4.03125in"}

 

Step 1

Create interfaces for Media Player and Advanced Media Player.

*MediaPlayer.java*

public interface MediaPlayer {\
public void play(String audioType, String fileName);\
}

*AdvancedMediaPlayer.java*

public interface AdvancedMediaPlayer {        \
public void playVlc(String fileName);\
public void playMp4(String fileName);\
}

Step 2

Create concrete classes implementing
the *AdvancedMediaPlayer* interface.

*VlcPlayer.java*

public class VlcPlayer implements AdvancedMediaPlayer{\
@Override\
public void playVlc(String fileName) {\
System.out.println("Playing vlc file. Name: "+
fileName);                \
}

@Override\
public void playMp4(String fileName) {\
//do nothing\
}\
}

*Mp4Player.java*

public class Mp4Player implements AdvancedMediaPlayer{

@Override\
public void playVlc(String fileName) {\
//do nothing\
}

@Override\
public void playMp4(String fileName) {\
System.out.println("Playing mp4 file. Name: "+
fileName);                \
}\
}

Step 3

Create adapter class implementing the *MediaPlayer* interface.

*MediaAdapter.java*

public class MediaAdapter implements MediaPlayer {

AdvancedMediaPlayer advancedMusicPlayer;

public MediaAdapter(String audioType){\
\
if(audioType.equalsIgnoreCase("vlc") ){\
advancedMusicPlayer = new VlcPlayer();                        \
\
}else if (audioType.equalsIgnoreCase("mp4")){\
advancedMusicPlayer = new Mp4Player();\
}        \
}

@Override\
public void play(String audioType, String fileName) {\
\
if(audioType.equalsIgnoreCase("vlc")){\
advancedMusicPlayer.playVlc(fileName);\
}\
else if(audioType.equalsIgnoreCase("mp4")){\
advancedMusicPlayer.playMp4(fileName);\
}\
}\
}

Step 4

Create concrete class implementing the *MediaPlayer* interface.

*AudioPlayer.java*

public class AudioPlayer implements MediaPlayer {\
MediaAdapter mediaAdapter;

@Override\
public void play(String audioType, String fileName) {                

//inbuilt support to play mp3 music files\
if(audioType.equalsIgnoreCase("mp3")){\
System.out.println("Playing mp3 file. Name: " +
fileName);                        \
}\
\
//mediaAdapter is providing support to play other file formats\
else if(audioType.equalsIgnoreCase("vlc") ||
audioType.equalsIgnoreCase("mp4")){\
mediaAdapter = new MediaAdapter(audioType);\
mediaAdapter.play(audioType, fileName);\
}\
\
else{\
System.out.println("Invalid media. " + audioType + " format not
supported");\
}\
}\
}

Step 5

Use the AudioPlayer to play different types of audio formats.

*AdapterPatternDemo.java*

public class AdapterPatternDemo {\
public static void main(String\[\] args) {\
AudioPlayer audioPlayer = new AudioPlayer();

audioPlayer.play("mp3", "beyond the horizon.mp3");\
audioPlayer.play("mp4", "alone.mp4");\
audioPlayer.play("vlc", "far far away.vlc");\
audioPlayer.play("avi", "mind me.avi");\
}\
}

 

 

 

Bridge Pattern

Tuesday, September 01, 2015

10:41

 

This pattern involves an interface which acts as a bridge which makes
the functionality of concrete classes independent from interface
implementer classes. Both types of classes can be altered structurally
without affecting each other. We are demonstrating use of Bridge pattern
via following example in which a circle can be drawn in different colors
using same abstract class method but different bridge implementer
classes.

 

Implementation

We have a DrawAPI interface which is acting as a bridge implementer and
concrete classes RedCircle, GreenCircle implementing the DrawAPI
interface. Shape is an abstract class and will use object of DrawAPI.
BridgePatternDemo, our demo class will use Shape class to draw different
colored circle.

 

> ![](media/image7.jpg){width="5.833333333333333in"
> height="3.0520833333333335in"}

 

Step 1

Create bridge implementer interface.

*DrawAPI.java*

public interface DrawAPI {\
public void drawCircle(int radius, int x, int y);\
}

Step 2

Create concrete bridge implementer classes implementing
the *DrawAPI* interface.

*RedCircle.java*

public class RedCircle implements DrawAPI {\
@Override\
public void drawCircle(int radius, int x, int y) {\
System.out.println("Drawing Circle\[ color: red, radius: " + radius + ",
x: " + x + ", " + y + "\]");\
}\
}

*GreenCircle.java*

public class GreenCircle implements DrawAPI {\
@Override\
public void drawCircle(int radius, int x, int y) {\
System.out.println("Drawing Circle\[ color: green, radius: " + radius +
", x: " + x + ", " + y + "\]");\
}\
}

Step 3

Create an abstract class *Shape* using the *DrawAPI* interface.

*Shape.java*

public abstract class Shape {\
protected DrawAPI drawAPI;\
\
protected Shape(DrawAPI drawAPI){\
this.drawAPI = drawAPI;\
}\
public abstract void draw();        \
}

Step 4

Create concrete class implementing the *Shape* interface.

*Circle.java*

public class Circle extends Shape {\
private int x, y, radius;

public Circle(int x, int y, int radius, DrawAPI drawAPI) {\
super(drawAPI);\
this.x = x;\
this.y = y;\
this.radius = radius;\
}

public void draw() {\
drawAPI.drawCircle(radius,x,y);\
}\
}

Step 5

Use the *Shape* and *DrawAPI* classes to draw different colored circles.

*BridgePatternDemo.java*

public class BridgePatternDemo {\
public static void main(String\[\] args) {\
Shape redCircle = new Circle(100,100, 10, new RedCircle());\
Shape greenCircle = new Circle(100,100, 10, new GreenCircle());

redCircle.draw();\
greenCircle.draw();\
}\
}

 

 

 

Filter Pattern

Tuesday, September 01, 2015

10:47

Filter pattern or Criteria pattern is a design pattern that enables
developers to filter a set of objects using different criteria and
chaining them in a decoupled way through logical operations. This type
of design pattern comes under structural pattern as this pattern
combines multiple criteria to obtain single criteria.

 

Implementation

We're going to create a Person object, Criteria interface and concrete
classes implementing this interface to filter list of Person objects.
CriteriaPatternDemo, our demo class uses Criteria objects to filter List
of Person objects based on various criteria and their combinations.

 

> ![](media/image8.jpg){width="5.833333333333333in" height="4.375in"}

 

 

Step 1

Create a class on which criteria is to be applied.

*Person.java*

public class Person {\
        \
private String name;\
private String gender;\
private String maritalStatus;

public Person(String name, String gender, String maritalStatus){\
this.name = name;\
this.gender = gender;\
this.maritalStatus = maritalStatus;                \
}

public String getName() {\
return name;\
}\
public String getGender() {\
return gender;\
}\
public String getMaritalStatus() {\
return maritalStatus;\
}        \
}

Step 2

Create an interface for Criteria.

*Criteria.java*

import java.util.List;

public interface Criteria {\
public List&lt;Person&gt; meetCriteria(List&lt;Person&gt; persons);\
}

Step 3

Create concrete classes implementing the *Criteria* interface.

*CriteriaMale.java*

import java.util.ArrayList;\
import java.util.List;

public class CriteriaMale implements Criteria {

@Override\
public List&lt;Person&gt; meetCriteria(List&lt;Person&gt; persons) {\
List&lt;Person&gt; malePersons = new ArrayList&lt;Person&gt;();\
\
for (Person person : persons) {\
if(person.getGender().equalsIgnoreCase("MALE")){\
malePersons.add(person);\
}\
}\
return malePersons;\
}\
}

*CriteriaFemale.java*

import java.util.ArrayList;\
import java.util.List;

public class CriteriaFemale implements Criteria {

@Override\
public List&lt;Person&gt; meetCriteria(List&lt;Person&gt; persons) {\
List&lt;Person&gt; femalePersons = new ArrayList&lt;Person&gt;();\
\
for (Person person : persons) {\
if(person.getGender().equalsIgnoreCase("FEMALE")){\
femalePersons.add(person);\
}\
}\
return femalePersons;\
}\
}

*CriteriaSingle.java*

import java.util.ArrayList;\
import java.util.List;

public class CriteriaSingle implements Criteria {

@Override\
public List&lt;Person&gt; meetCriteria(List&lt;Person&gt; persons) {\
List&lt;Person&gt; singlePersons = new ArrayList&lt;Person&gt;();\
\
for (Person person : persons) {\
if(person.getMaritalStatus().equalsIgnoreCase("SINGLE")){\
singlePersons.add(person);\
}\
}\
return singlePersons;\
}\
}

*AndCriteria.java*

import java.util.List;

public class AndCriteria implements Criteria {

private Criteria criteria;\
private Criteria otherCriteria;

public AndCriteria(Criteria criteria, Criteria otherCriteria) {\
this.criteria = criteria;\
this.otherCriteria = otherCriteria;\
}

@Override\
public List&lt;Person&gt; meetCriteria(List&lt;Person&gt; persons) {\
\
List&lt;Person&gt; firstCriteriaPersons =
criteria.meetCriteria(persons);                \
return otherCriteria.meetCriteria(firstCriteriaPersons);\
}\
}

*OrCriteria.java*

import java.util.List;

public class OrCriteria implements Criteria {

private Criteria criteria;\
private Criteria otherCriteria;

public OrCriteria(Criteria criteria, Criteria otherCriteria) {\
this.criteria = criteria;\
this.otherCriteria = otherCriteria;\
}

@Override\
public List&lt;Person&gt; meetCriteria(List&lt;Person&gt; persons) {\
List&lt;Person&gt; firstCriteriaItems = criteria.meetCriteria(persons);\
List&lt;Person&gt; otherCriteriaItems =
otherCriteria.meetCriteria(persons);

for (Person person : otherCriteriaItems) {\
if(!firstCriteriaItems.contains(person)){\
firstCriteriaItems.add(person);\
}\
}        \
return firstCriteriaItems;\
}\
}

Step4

Use different Criteria and their combination to filter out persons.

*CriteriaPatternDemo.java*

public class CriteriaPatternDemo {\
public static void main(String\[\] args) {\
List&lt;Person&gt; persons = new ArrayList&lt;Person&gt;();

persons.add(new Person("Robert","Male", "Single"));\
persons.add(new Person("John", "Male", "Married"));\
persons.add(new Person("Laura", "Female", "Married"));\
persons.add(new Person("Diana", "Female", "Single"));\
persons.add(new Person("Mike", "Male", "Single"));\
persons.add(new Person("Bobby", "Male", "Single"));

Criteria male = new CriteriaMale();\
Criteria female = new CriteriaFemale();\
Criteria single = new CriteriaSingle();\
Criteria singleMale = new AndCriteria(single, male);\
Criteria singleOrFemale = new OrCriteria(single, female);

System.out.println("Males: ");\
printPersons(male.meetCriteria(persons));

System.out.println("\\nFemales: ");\
printPersons(female.meetCriteria(persons));

System.out.println("\\nSingle Males: ");\
printPersons(singleMale.meetCriteria(persons));

System.out.println("\\nSingle Or Females: ");\
printPersons(singleOrFemale.meetCriteria(persons));\
}

public static void printPersons(List&lt;Person&gt; persons){\
\
for (Person person : persons) {\
System.out.println("Person : \[ Name : " + person.getName() + ", Gender
: " + person.getGender() + ", Marital Status : " +
person.getMaritalStatus() + " \]");\
}\
}\
}

 

 

 

Composite Pattern

Tuesday, September 01, 2015

10:50

 

This pattern creates a class that contains group of its own objects.
This class provides ways to modify its group of same objects. We are
demonstrating use of composite pattern via following example in which we
will show employees hierarchy of an organization.

 

Implementation

We have a class Employee which acts as composite pattern actor class.
CompositePatternDemo, our demo class will use Employee class to add
department level hierarchy and print all employees.

 

> ![](media/image9.jpg){width="3.7291666666666665in" height="4.375in"}

 

Step 1

Create *Employee* class having list of *Employee* objects.

*Employee.java*

import java.util.ArrayList;\
import java.util.List;

public class Employee {\
private String name;\
private String dept;\
private int salary;\
private List&lt;Employee&gt; subordinates;

// constructor\
public Employee(String name,String dept, int sal) {\
this.name = name;\
this.dept = dept;\
this.salary = sal;\
subordinates = new ArrayList&lt;Employee&gt;();\
}

public void add(Employee e) {\
subordinates.add(e);\
}

public void remove(Employee e) {\
subordinates.remove(e);\
}

public List&lt;Employee&gt; getSubordinates(){\
return subordinates;\
}

public String toString(){\
return ("Employee :\[ Name : " + name + ", dept : " + dept + ", salary
:" + salary+" \]");\
}\
}

Step 2

Use the *Employee* class to create and print employee hierarchy.

*CompositePatternDemo.java*

public class CompositePatternDemo {\
public static void main(String\[\] args) {\
\
Employee CEO = new Employee("John","CEO", 30000);

Employee headSales = new Employee("Robert","Head Sales", 20000);

Employee headMarketing = new Employee("Michel","Head Marketing", 20000);

Employee clerk1 = new Employee("Laura","Marketing", 10000);\
Employee clerk2 = new Employee("Bob","Marketing", 10000);

Employee salesExecutive1 = new Employee("Richard","Sales", 10000);\
Employee salesExecutive2 = new Employee("Rob","Sales", 10000);

CEO.add(headSales);\
CEO.add(headMarketing);

headSales.add(salesExecutive1);\
headSales.add(salesExecutive2);

headMarketing.add(clerk1);\
headMarketing.add(clerk2);

//print all employees of the organization\
System.out.println(CEO);\
\
for (Employee headEmployee : CEO.getSubordinates()) {\
System.out.println(headEmployee);\
\
for (Employee employee : headEmployee.getSubordinates()) {\
System.out.println(employee);\
}\
}                \
}\
}

 

 

 

Decorator Pattern

Tuesday, September 01, 2015

11:24

 

This pattern creates a decorator class which wraps the original class
and provides additional functionality keeping class methods signature
intact. We are demonstrating the use of decorator pattern via following
example in which we will decorate a shape with some color without alter
shape class.

 

Implementation

We're going to create a Shape interface and concrete classes
implementing the Shape interface. We will then create an abstract
decorator class ShapeDecorator implementing the Shape interface and
having Shape object as its instance variable. RedShapeDecorator is
concrete class implementing ShapeDecorator. DecoratorPatternDemo, our
demo class will use RedShapeDecorator to decorate Shape objects.

 

> ![](media/image10.jpg){width="7.135416666666667in" height="3.84375in"}

 

 

Step 1

Create an interface.

*Shape.java*

public interface Shape {\
void draw();\
}

Step 2

Create concrete classes implementing the same interface.

*Rectangle.java*

public class Rectangle implements Shape {

@Override\
public void draw() {\
System.out.println("Shape: Rectangle");\
}\
}

*Circle.java*

public class Circle implements Shape {

@Override\
public void draw() {\
System.out.println("Shape: Circle");\
}\
}

Step 3

Create abstract decorator class implementing the *Shape* interface.

*ShapeDecorator.java*

public abstract class ShapeDecorator implements Shape {\
protected Shape decoratedShape;

public ShapeDecorator(Shape decoratedShape){\
this.decoratedShape = decoratedShape;\
}

public void draw(){\
decoratedShape.draw();\
}        \
}

Step 4

Create concrete decorator class extending the *ShapeDecorator* class.

*RedShapeDecorator.java*

public class RedShapeDecorator extends ShapeDecorator {

public RedShapeDecorator(Shape decoratedShape) {\
super(decoratedShape);                \
}

@Override\
public void draw() {\
decoratedShape.draw();        \
setRedBorder(decoratedShape);\
}

private void setRedBorder(Shape decoratedShape){\
System.out.println("Border Color: Red");\
}\
}

Step 5

Use the *RedShapeDecorator* to decorate *Shape* objects.

*DecoratorPatternDemo.java*

public class DecoratorPatternDemo {\
public static void main(String\[\] args) {

Shape circle = new Circle();

Shape redCircle = new RedShapeDecorator(new Circle());

Shape redRectangle = new RedShapeDecorator(new Rectangle());\
System.out.println("Circle with normal border");\
circle.draw();

System.out.println("\\nCircle of red border");\
redCircle.draw();

System.out.println("\\nRectangle of red border");\
redRectangle.draw();\
}\
}

 

 

Facade Pattern

Tuesday, September 01, 2015

11:49

 

This pattern involves a single class which provides simplified methods
required by client and delegates calls to methods of existing system
classes.

 

Implementation

We are going to create a Shape interface and concrete classes
implementing the Shape interface. A facade class ShapeMaker is defined
as a next step. ShapeMaker class uses the concrete classes to delegate
user calls to these classes. FacadePatternDemo, our demo class, will use
ShapeMaker class to show the results.

 

> ![](media/image11.jpg){width="6.34375in" height="3.1875in"}

 

Step 1

Create an interface.

*Shape.java*

public interface Shape {\
void draw();\
}

Step 2

Create concrete classes implementing the same interface.

*Rectangle.java*

public class Rectangle implements Shape {

@Override\
public void draw() {\
System.out.println("Rectangle::draw()");\
}\
}

*Square.java*

public class Square implements Shape {

@Override\
public void draw() {\
System.out.println("Square::draw()");\
}\
}

*Circle.java*

public class Circle implements Shape {

@Override\
public void draw() {\
System.out.println("Circle::draw()");\
}\
}

Step 3

Create a facade class.

*ShapeMaker.java*

public class ShapeMaker {\
private Shape circle;\
private Shape rectangle;\
private Shape square;

public ShapeMaker() {\
circle = new Circle();\
rectangle = new Rectangle();\
square = new Square();\
}

public void drawCircle(){\
circle.draw();\
}\
public void drawRectangle(){\
rectangle.draw();\
}\
public void drawSquare(){\
square.draw();\
}\
}

Step 4

Use the facade to draw various types of shapes.

*FacadePatternDemo.java*

public class FacadePatternDemo {\
public static void main(String\[\] args) {\
ShapeMaker shapeMaker = new ShapeMaker();

shapeMaker.drawCircle();\
shapeMaker.drawRectangle();\
shapeMaker.drawSquare();                \
}\
}

 

 

 

Flyweight Pattern

Tuesday, September 01, 2015

11:51

 

Flyweight pattern tries to reuse already existing similar kind objects
by storing them and creates new object when no matching object is found.
We will demonstrate this pattern by drawing 20 circles of different
locations but we will create only 5 objects. Only 5 colors are available
so color property is used to check already existing *Circle* objects.

 

Implementation

We are going to create a Shape interface and concrete class Circle
implementing the Shape interface. A factory class ShapeFactory is
defined as a next step. ShapeFactory has a HashMap of Circle having key
as color of the Circle object. Whenever a request comes to create a
circle of particular color to ShapeFactory, it checks the circle object
in its HashMap, if object of Circle found, that object is returned
otherwise a new object is created, stored in hashmap for future use, and
returned to client. FlyWeightPatternDemo, our demo class, will use
ShapeFactory to get a Shape object. It will pass information (red /
green / blue/ black / white) to ShapeFactory to get the circle of
desired color it needs.

 

 

> ![](media/image12.jpg){width="4.4375in" height="3.7604166666666665in"}

 

Step 1

Create an interface.

*Shape.java*

public interface Shape {\
void draw();\
}

Step 2

Create concrete class implementing the same interface.

*Circle.java*

public class Circle implements Shape {\
private String color;\
private int x;\
private int y;\
private int radius;

public Circle(String color){\
this.color = color;                \
}

public void setX(int x) {\
this.x = x;\
}

public void setY(int y) {\
this.y = y;\
}

public void setRadius(int radius) {\
this.radius = radius;\
}

@Override\
public void draw() {\
System.out.println("Circle: Draw() \[Color : " + color + ", x : " + x +
", y :" + y + ", radius :" + radius);\
}\
}

Step 3

Create a factory to generate object of concrete class based on given
information.

*ShapeFactory.java*

import java.util.HashMap;

public class ShapeFactory {\
private static final HashMap&lt;String, Shape&gt; circleMap = new
HashMap();

public static Shape getCircle(String color) {\
Circle circle = (Circle)circleMap.get(color);

if(circle == null) {\
circle = new Circle(color);\
circleMap.put(color, circle);\
System.out.println("Creating circle of color : " + color);\
}\
return circle;\
}\
}

Step 4

Use the factory to get object of concrete class by passing an
information such as color.

*FlyweightPatternDemo.java*

public class FlyweightPatternDemo {\
private static final String colors\[\] = { "Red", "Green", "Blue",
"White", "Black" };\
public static void main(String\[\] args) {

for(int i=0; i &lt; 20; ++i) {\
Circle circle = (Circle)ShapeFactory.getCircle(getRandomColor());\
circle.setX(getRandomX());\
circle.setY(getRandomY());\
circle.setRadius(100);\
circle.draw();\
}\
}\
private static String getRandomColor() {\
return colors\[(int)(Math.random()\*colors.length)\];\
}\
private static int getRandomX() {\
return (int)(Math.random()\*100 );\
}\
private static int getRandomY() {\
return (int)(Math.random()\*100);\
}\
}

 

 

Proxy Pattern

Tuesday, September 01, 2015

11:52

 

In proxy pattern, we create object having original object to interface
its functionality to outer world.

 

Implementation

We are going to create an Image interface and concrete classes
implementing the Image interface. ProxyImage is a a proxy class to
reduce memory footprint of RealImage object loading. ProxyPatternDemo,
our demo class, will use ProxyImage to get an Image object to load and
display as it needs.

 

> ![](media/image13.jpg){width="5.833333333333333in"
> height="2.7395833333333335in"}

 

Step 1

Create an interface.

*Image.java*

public interface Image {\
void display();\
}

Step 2

Create concrete classes implementing the same interface.

*RealImage.java*

public class RealImage implements Image {

private String fileName;

public RealImage(String fileName){\
this.fileName = fileName;\
loadFromDisk(fileName);\
}

@Override\
public void display() {\
System.out.println("Displaying " + fileName);\
}

private void loadFromDisk(String fileName){\
System.out.println("Loading " + fileName);\
}\
}

*ProxyImage.java*

public class ProxyImage implements Image{

private RealImage realImage;\
private String fileName;

public ProxyImage(String fileName){\
this.fileName = fileName;\
}

@Override\
public void display() {\
if(realImage == null){\
realImage = new RealImage(fileName);\
}\
realImage.display();\
}\
}

Step 3

Use the *ProxyImage* to get object of *RealImage* class when required.

*ProxyPatternDemo.java*

public class ProxyPatternDemo {\
        \
public static void main(String\[\] args) {\
Image image = new ProxyImage("test\_10mb.jpg");

//image will be loaded from disk\
image.display();\
System.out.println("");\
\
//image will not be loaded from disk\
image.display();         \
}\
}

 

 

 

 

Chain of Responsibility Pattern

Tuesday, September 01, 2015

11:58

 

In this pattern, normally each receiver contains reference to another
receiver. If one object cannot handle the request then it passes the
same to the next receiver and so on.

 

Implementation

We have created an abstract class AbstractLogger with a level of
logging. Then we have created three types of loggers extending the
AbstractLogger. Each logger checks the level of message to its level and
print accordingly otherwise does not print and pass the message to its
next logger.

 

> ![](media/image14.jpg){width="5.833333333333333in"
> height="3.9583333333333335in"}

Step 1

Create an abstract logger class.

*AbstractLogger.java*

public abstract class AbstractLogger {\
public static int INFO = 1;\
public static int DEBUG = 2;\
public static int ERROR = 3;

protected int level;

//next element in chain or responsibility\
protected AbstractLogger nextLogger;

public void setNextLogger(AbstractLogger nextLogger){\
this.nextLogger = nextLogger;\
}

public void logMessage(int level, String message){\
if(this.level &lt;= level){\
write(message);\
}\
if(nextLogger !=null){\
nextLogger.logMessage(level, message);\
}\
}

abstract protected void write(String message);\
        \
}

Step 2

Create concrete classes extending the logger.

*ConsoleLogger.java*

public class ConsoleLogger extends AbstractLogger {

public ConsoleLogger(int level){\
this.level = level;\
}

@Override\
protected void write(String message) {                \
System.out.println("Standard Console::Logger: " + message);\
}\
}

*ErrorLogger.java*

public class ErrorLogger extends AbstractLogger {

public ErrorLogger(int level){\
this.level = level;\
}

@Override\
protected void write(String message) {                \
System.out.println("Error Console::Logger: " + message);\
}\
}

*FileLogger.java*

public class FileLogger extends AbstractLogger {

public FileLogger(int level){\
this.level = level;\
}

@Override\
protected void write(String message) {                \
System.out.println("File::Logger: " + message);\
}\
}

Step 3

Create different types of loggers. Assign them error levels and set next
logger in each logger. Next logger in each logger represents the part of
the chain.

*ChainPatternDemo.java*

public class ChainPatternDemo {\
        \
private static AbstractLogger getChainOfLoggers(){

AbstractLogger errorLogger = new ErrorLogger(AbstractLogger.ERROR);\
AbstractLogger fileLogger = new FileLogger(AbstractLogger.DEBUG);\
AbstractLogger consoleLogger = new ConsoleLogger(AbstractLogger.INFO);

errorLogger.setNextLogger(fileLogger);\
fileLogger.setNextLogger(consoleLogger);

return errorLogger;        \
}

public static void main(String\[\] args) {\
AbstractLogger loggerChain = getChainOfLoggers();

loggerChain.logMessage(AbstractLogger.INFO,\
"This is an information.");

loggerChain.logMessage(AbstractLogger.DEBUG,\
"This is an debug level information.");

loggerChain.logMessage(AbstractLogger.ERROR,\
"This is an error information.");\
}\
}

 

 

Command Pattern

Tuesday, September 01, 2015

12:00

 

Command pattern is a data driven design pattern and falls under
behavioral pattern category. A request is wrapped under an object as
command and passed to invoker object. Invoker object looks for the
appropriate object which can handle this command and passes the command
to the corresponding object which executes the command.

 

Implementation

We have created an interface Order which is acting as a command. We have
created a Stock class which acts as a request. We have concrete command
classes BuyStock and SellStock implementing Order interface which will
do actual command processing. A class Broker is created which acts as an
invoker object. It can take and place orders. Broker object uses command
pattern to identify which object will execute which command based on the
type of command. CommandPatternDemo, our demo class, will use Broker
class to demonstrate command pattern.

 

 

> ![](media/image15.jpg){width="5.833333333333333in" height="4.375in"}

 

Step 1

Create a command interface.

*Order.java*

public interface Order {\
void execute();\
}

Step 2

Create a request class.

*Stock.java*

public class Stock {\
        \
private String name = "ABC";\
private int quantity = 10;

public void buy(){\
System.out.println("Stock \[ Name: "+name+",\
Quantity: " + quantity +" \] bought");\
}\
public void sell(){\
System.out.println("Stock \[ Name: "+name+",\
Quantity: " + quantity +" \] sold");\
}\
}

Step 3

Create concrete classes implementing the *Order* interface.

*BuyStock.java*

public class BuyStock implements Order {\
private Stock abcStock;

public BuyStock(Stock abcStock){\
this.abcStock = abcStock;\
}

public void execute() {\
abcStock.buy();\
}\
}

*SellStock.java*

public class SellStock implements Order {\
private Stock abcStock;

public SellStock(Stock abcStock){\
this.abcStock = abcStock;\
}

public void execute() {\
abcStock.sell();\
}\
}

Step 4

Create command invoker class.

*Broker.java*

import java.util.ArrayList;\
import java.util.List;

public class Broker {\
private List&lt;Order&gt; orderList = new ArrayList&lt;Order&gt;();

public void takeOrder(Order order){\
orderList.add(order);                \
}

public void placeOrders(){\
\
for (Order order : orderList) {\
order.execute();\
}\
orderList.clear();\
}\
}

Step 5

Use the Broker class to take and execute commands.

*CommandPatternDemo.java*

public class CommandPatternDemo {\
public static void main(String\[\] args) {\
Stock abcStock = new Stock();

BuyStock buyStockOrder = new BuyStock(abcStock);\
SellStock sellStockOrder = new SellStock(abcStock);

Broker broker = new Broker();\
broker.takeOrder(buyStockOrder);\
broker.takeOrder(sellStockOrder);

broker.placeOrders();\
}\
}

 

 

Interpreter Pattern

Tuesday, September 01, 2015

12:04

 

This pattern involves implementing an expression interface which tells
to interpret a particular context. This pattern is used in SQL parsing,
symbol processing engine etc.

 

Implementation

We are going to create an interface Expression and concrete classes
implementing the Expression interface. A class TerminalExpression is
defined which acts as a main interpreter of context in question. Other
classes OrExpression, AndExpression are used to create combinational
expressions. InterpreterPatternDemo, our demo class, will use Expression
class to create rules and demonstrate parsing of expressions.

 

> ![](media/image16.jpg){width="5.583333333333333in"
> height="5.083333333333333in"}

 

Step 1

Create an expression interface.

*Expression.java*

public interface Expression {\
public boolean interpret(String context);\
}

Step 2

Create concrete classes implementing the above interface.

*TerminalExpression.java*

public class TerminalExpression implements Expression {\
        \
private String data;

public TerminalExpression(String data){\
this.data = data;\
}

@Override\
public boolean interpret(String context) {\
\
if(context.contains(data)){\
return true;\
}\
return false;\
}\
}

*OrExpression.java*

public class OrExpression implements Expression {\
        \
private Expression expr1 = null;\
private Expression expr2 = null;

public OrExpression(Expression expr1, Expression expr2) {\
this.expr1 = expr1;\
this.expr2 = expr2;\
}

@Override\
public boolean interpret(String context) {                \
return expr1.interpret(context) || expr2.interpret(context);\
}\
}

*AndExpression.java*

public class AndExpression implements Expression {\
        \
private Expression expr1 = null;\
private Expression expr2 = null;

public AndExpression(Expression expr1, Expression expr2) {\
this.expr1 = expr1;\
this.expr2 = expr2;\
}

@Override\
public boolean interpret(String context) {                \
return expr1.interpret(context) && expr2.interpret(context);\
}\
}

Step 3

*InterpreterPatternDemo* uses *Expression* class to create rules and
then parse them.

*InterpreterPatternDemo.java*

public class InterpreterPatternDemo {

//Rule: Robert and John are male\
public static Expression getMaleExpression(){\
Expression robert = new TerminalExpression("Robert");\
Expression john = new TerminalExpression("John");\
return new OrExpression(robert, john);                \
}

//Rule: Julie is a married women\
public static Expression getMarriedWomanExpression(){\
Expression julie = new TerminalExpression("Julie");\
Expression married = new TerminalExpression("Married");\
return new AndExpression(julie, married);                \
}

public static void main(String\[\] args) {\
Expression isMale = getMaleExpression();\
Expression isMarriedWoman = getMarriedWomanExpression();

System.out.println("John is male? " + isMale.interpret("John"));\
System.out.println("Julie is a married women? " +
isMarriedWoman.interpret("Married Julie"));\
}\
}

 

 

 

 

 

 

Iterator Pattern

Tuesday, September 01, 2015

15:18

 

Iterator pattern is very commonly used design pattern in Java and .Net
programming environment. This pattern is used to get a way to access the
elements of a collection object in sequential manner without any need to
know its underlying representation.

 

Implementation

We're going to create a Iterator interface which narrates navigation
method and a Container interface which retruns the iterator . Concrete
classes implementing the Container interface will be responsible to
implement Iterator interface and use it. IteratorPatternDemo, our demo
class will use NamesRepository, a concrete class implementation to print
a Names stored as a collection in NamesRepository.

 

> ![](media/image17.jpg){width="5.833333333333333in" height="2.84375in"}

Step 1

Create interfaces.

*Iterator.java*

public interface Iterator {\
public boolean hasNext();\
public Object next();\
}

*Container.java*

public interface Container {\
public Iterator getIterator();\
}

Step 2

Create concrete class implementing the *Container* interface. This class
has inner class*NameIterator* implementing the *Iterator* interface.

*NameRepository.java*

public class NameRepository implements Container {\
public String names\[\] = {"Robert" , "John" ,"Julie" , "Lora"};

@Override\
public Iterator getIterator() {\
return new NameIterator();\
}

private class NameIterator implements Iterator {

int index;

@Override\
public boolean hasNext() {\
\
if(index &lt; names.length){\
return true;\
}\
return false;\
}

@Override\
public Object next() {\
\
if(this.hasNext()){\
return names\[index++\];\
}\
return null;\
}                \
}\
}

Step 3

Use the *NameRepository* to get iterator and print names.

*IteratorPatternDemo.java*

public class IteratorPatternDemo {\
        \
public static void main(String\[\] args) {\
NameRepository namesRepository = new NameRepository();

for(Iterator iter = namesRepository.getIterator(); iter.hasNext();){\
String name = (String)iter.next();\
System.out.println("Name : " + name);\
}         \
}\
}

 

 

 

Mediator Pattern

Tuesday, September 01, 2015

15:29

This pattern provides a mediator class which normally handles all the
communications between different classes and supports easy maintenance
of the code by loose coupling. Mediator pattern falls under behavioral
pattern category.

 

Implementation

We are demonstrating mediator pattern by example of a chat room where
multiple users can send message to chat room and it is the
responsibility of chat room to show the messages to all users. We have
created two classes ChatRoom and User. User objects will use ChatRoom
method to share their messages.

 

> ![](media/image18.jpg){width="5.833333333333333in" height="1.40625in"}

 

Step 1

Create mediator class.

*ChatRoom.java*

import java.util.Date;

public class ChatRoom {\
public static void showMessage(User user, String message){\
System.out.println(new Date().toString() + " \[" + user.getName() + "\]
: " + message);\
}\
}

Step 2

Create user class

*User.java*

public class User {\
private String name;

public String getName() {\
return name;\
}

public void setName(String name) {\
this.name = name;\
}

public User(String name){\
this.name = name;\
}

public void sendMessage(String message){\
ChatRoom.showMessage(this,message);\
}\
}

Step 3

Use the *User* object to show communications between them.

*MediatorPatternDemo.java*

public class MediatorPatternDemo {\
public static void main(String\[\] args) {\
User robert = new User("Robert");\
User john = new User("John");

robert.sendMessage("Hi! John!");\
john.sendMessage("Hello! Robert!");\
}\
}

 

 

 

Memento Pattern

Tuesday, September 01, 2015

15:31

Memento pattern is used to restore state of an object to a previous
state. Memento pattern falls under behavioral pattern category.

 

Implementation

Memento pattern uses three actor classes. Memento contains state of an
object to be restored. Originator creates and stores states in Memento
objects and Caretaker object is responsible to restore object state from
Memento. We have created classes Memento,Originator and CareTaker.

 

> ![](media/image19.jpg){width="5.833333333333333in" height="3.75in"}

 

Step 1

Create Memento class.

*Memento.java*

public class Memento {\
private String state;

public Memento(String state){\
this.state = state;\
}

public String getState(){\
return state;\
}        \
}

Step 2

Create Originator class

*Originator.java*

public class Originator {\
private String state;

public void setState(String state){\
this.state = state;\
}

public String getState(){\
return state;\
}

public Memento saveStateToMemento(){\
return new Memento(state);\
}

public void getStateFromMemento(Memento Memento){\
state = Memento.getState();\
}\
}

Step 3

Create CareTaker class

*CareTaker.java*

import java.util.ArrayList;\
import java.util.List;

public class CareTaker {\
private List&lt;Memento&gt; mementoList = new
ArrayList&lt;Memento&gt;();

public void add(Memento state){\
mementoList.add(state);\
}

public Memento get(int index){\
return mementoList.get(index);\
}\
}

Step 4

Use *CareTaker* and *Originator* objects.

*MementoPatternDemo.java*

public class MementoPatternDemo {\
public static void main(String\[\] args) {\
\
Originator originator = new Originator();\
CareTaker careTaker = new CareTaker();\
\
originator.setState("State \#1");\
originator.setState("State \#2");\
careTaker.add(originator.saveStateToMemento());\
\
originator.setState("State \#3");\
careTaker.add(originator.saveStateToMemento());\
\
originator.setState("State \#4");\
System.out.println("Current State: " +
originator.getState());                \
\
originator.getStateFromMemento(careTaker.get(0));\
System.out.println("First saved State: " + originator.getState());\
originator.getStateFromMemento(careTaker.get(1));\
System.out.println("Second saved State: " + originator.getState());\
}\
}

 

 

 

 

 

 

Observer Pattern

Tuesday, September 01, 2015

15:34

Observer pattern is used when there is one-to-many relationship between
objects such as if one object is modified, its depenedent objects are to
be notified automatically.

 

Implementation

Observer pattern uses three actor classes. Subject, Observer and Client.
Subject is an object having methods to attach and detach observers to a
client object. We have created an abstract class Observer and a concrete
class Subject that is extending class Observer.

 

> ![](media/image20.jpg){width="5.833333333333333in"
> height="4.020833333333333in"}

 

 

Step 1

Create Subject class.

*Subject.java*

import java.util.ArrayList;\
import java.util.List;

public class Subject {\
        \
private List&lt;Observer&gt; observers = new
ArrayList&lt;Observer&gt;();\
private int state;

public int getState() {\
return state;\
}

public void setState(int state) {\
this.state = state;\
notifyAllObservers();\
}

public void attach(Observer observer){\
observers.add(observer);                \
}

public void notifyAllObservers(){\
for (Observer observer : observers) {\
observer.update();\
}\
}         \
}

Step 2

Create Observer class.

*Observer.java*

public abstract class Observer {\
protected Subject subject;\
public abstract void update();\
}

Step 3

Create concrete observer classes

*BinaryObserver.java*

public class BinaryObserver extends Observer{

public BinaryObserver(Subject subject){\
this.subject = subject;\
this.subject.attach(this);\
}

@Override\
public void update() {\
System.out.println( "Binary String: " + Integer.toBinaryString(
subject.getState() ) );\
}\
}

*OctalObserver.java*

public class OctalObserver extends Observer{

public OctalObserver(Subject subject){\
this.subject = subject;\
this.subject.attach(this);\
}

@Override\
public void update() {\
System.out.println( "Octal String: " + Integer.toOctalString(
subject.getState() ) );\
}\
}

*HexaObserver.java*

public class HexaObserver extends Observer{

public HexaObserver(Subject subject){\
this.subject = subject;\
this.subject.attach(this);\
}

@Override\
public void update() {\
System.out.println( "Hex String: " + Integer.toHexString(
subject.getState() ).toUpperCase() );\
}\
}

Step 4

Use *Subject* and concrete observer objects.

*ObserverPatternDemo.java*

public class ObserverPatternDemo {\
public static void main(String\[\] args) {\
Subject subject = new Subject();

new HexaObserver(subject);\
new OctalObserver(subject);\
new BinaryObserver(subject);

System.out.println("First state change: 15");        \
subject.setState(15);\
System.out.println("Second state change: 10");        \
subject.setState(10);\
}\
}

 

 

 

State Pattern

Tuesday, September 01, 2015

15:36

In State pattern, we create objects which represent various states and a
context object whose behavior varies as its state object changes.

 

Implementation

We are going to create a State interface defining an action and concrete
state classes implementing the State interface. Context is a class which
carries a State.

 

> ![](media/image21.jpg){width="5.833333333333333in" height="4.03125in"}

Step 1

Create an interface.

*State.java*

public interface State {\
public void doAction(Context context);\
}

Step 2

Create concrete classes implementing the same interface.

*StartState.java*

public class StartState implements State {

public void doAction(Context context) {\
System.out.println("Player is in start state");\
context.setState(this);        \
}

public String toString(){\
return "Start State";\
}\
}

*StopState.java*

public class StopState implements State {

public void doAction(Context context) {\
System.out.println("Player is in stop state");\
context.setState(this);        \
}

public String toString(){\
return "Stop State";\
}\
}

Step 3

Create *Context* Class.

*Context.java*

public class Context {\
private State state;

public Context(){\
state = null;\
}

public void setState(State state){\
this.state = state;                \
}

public State getState(){\
return state;\
}\
}

Step 4

Use the *Context* to see change in behaviour when *State* changes.

*StatePatternDemo.java*

public class StatePatternDemo {\
public static void main(String\[\] args) {\
Context context = new Context();

StartState startState = new StartState();\
startState.doAction(context);

System.out.println(context.getState().toString());

StopState stopState = new StopState();\
stopState.doAction(context);

System.out.println(context.getState().toString());\
}\
}

 

 

 

Null Object Pattern

Tuesday, September 01, 2015

15:38

In Null Object pattern, a null object replaces check of NULL object
instance. Instead of putting if check for a null value, Null Object
reflects a do nothing relationship. Such Null object can also be used to
provide default behaviour in case data is not available. In Null Object
pattern, we create an abstract class specifying various operations to be
done, concrete classes extending this class and a null object class
providing do nothing implemention of this class and will be used
seemlessly where we need to check null value.

 

Implementation

We are going to create a AbstractCustomer abstract class defining
opearations. Here the name of the customer and concrete classes
extending the AbstractCustomer class. A factory class CustomerFactory is
created to return either RealCustomer or NullCustomer objects based on
the name of customer passed to it.

 

> ![](media/image22.jpg){width="5.833333333333333in"
> height="3.1458333333333335in"}

 

Step 1

Create an abstract class.

*AbstractCustomer.java*

public abstract class AbstractCustomer {\
protected String name;\
public abstract boolean isNil();\
public abstract String getName();\
}

Step 2

Create concrete classes extending the above class.

*RealCustomer.java*

public class RealCustomer extends AbstractCustomer {

public RealCustomer(String name) {\
this.name = name;                \
}\
\
@Override\
public String getName() {\
return name;\
}\
\
@Override\
public boolean isNil() {\
return false;\
}\
}

*NullCustomer.java*

public class NullCustomer extends AbstractCustomer {

@Override\
public String getName() {\
return "Not Available in Customer Database";\
}

@Override\
public boolean isNil() {\
return true;\
}\
}

Step 3

Create *CustomerFactory* Class.

*CustomerFactory.java*

public class CustomerFactory {\
        \
public static final String\[\] names = {"Rob", "Joe", "Julie"};

public static AbstractCustomer getCustomer(String name){\
\
for (int i = 0; i &lt; names.length; i++) {\
if (names\[i\].equalsIgnoreCase(name)){\
return new RealCustomer(name);\
}\
}\
return new NullCustomer();\
}\
}

Step 4

Use the *CustomerFactory* to get
either *RealCustomer* or *NullCustomer* objects based on the name of
customer passed to it.

*NullPatternDemo.java*

public class NullPatternDemo {\
public static void main(String\[\] args) {

AbstractCustomer customer1 = CustomerFactory.getCustomer("Rob");\
AbstractCustomer customer2 = CustomerFactory.getCustomer("Bob");\
AbstractCustomer customer3 = CustomerFactory.getCustomer("Julie");\
AbstractCustomer customer4 = CustomerFactory.getCustomer("Laura");

System.out.println("Customers");\
System.out.println(customer1.getName());\
System.out.println(customer2.getName());\
System.out.println(customer3.getName());\
System.out.println(customer4.getName());\
}\
}

 

 

 

Strategy Pattern

Tuesday, September 01, 2015

15:40

In Strategy pattern, we create objects which represent various
strategies and a context object whose behavior varies as per its
strategy object. The strategy object changes the executing algorithm of
the context object.

 

Implementation

We are going to create a Strategy interface defining an action and
concrete strategy classes implementing the Strategy interface. Context
is a class which uses a Strategy.

 

 

> ![](media/image23.jpg){width="5.833333333333333in" height="3.34375in"}

Step 1

Create an interface.

*Strategy.java*

public interface Strategy {\
public int doOperation(int num1, int num2);\
}

Step 2

Create concrete classes implementing the same interface.

*OperationAdd.java*

public class OperationAdd implements Strategy{\
@Override\
public int doOperation(int num1, int num2) {\
return num1 + num2;\
}\
}

*OperationSubstract.java*

public class OperationSubstract implements Strategy{\
@Override\
public int doOperation(int num1, int num2) {\
return num1 - num2;\
}\
}

*OperationMultiply.java*

public class OperationMultiply implements Strategy{\
@Override\
public int doOperation(int num1, int num2) {\
return num1 \* num2;\
}\
}

Step 3

Create *Context* Class.

*Context.java*

public class Context {\
private Strategy strategy;

public Context(Strategy strategy){\
this.strategy = strategy;\
}

public int executeStrategy(int num1, int num2){\
return strategy.doOperation(num1, num2);\
}\
}

Step 4

Use the *Context* to see change in behaviour when it changes
its *Strategy*.

*StrategyPatternDemo.java*

public class StrategyPatternDemo {\
public static void main(String\[\] args) {\
Context context = new Context(new OperationAdd());                \
System.out.println("10 + 5 = " + context.executeStrategy(10, 5));

context = new Context(new OperationSubstract());                \
System.out.println("10 - 5 = " + context.executeStrategy(10, 5));

context = new Context(new OperationMultiply());                \
System.out.println("10 \* 5 = " + context.executeStrategy(10, 5));\
}\
}

 

 

 

Template Pattern

Tuesday, September 01, 2015

15:42

In Template pattern, an abstract class exposes defined
way(s)/template(s) to execute its methods. Its subclasses can override
the method implementation as per need but the invocation is to be in the
same way as defined by an abstract class.

 

Implementation

We are going to create a Game abstract class defining operations with a
template method set to be final so that it cannot be overridden. Cricket
and Football are concrete classes that extend Game and override its
methods.

 

> ![](media/image24.jpg){width="5.833333333333333in" height="3.875in"}

Step 1

Create an abstract class with a template method being final.

*Game.java*

public abstract class Game {\
abstract void initialize();\
abstract void startPlay();\
abstract void endPlay();

//template method\
public final void play(){

//initialize the game\
initialize();

//start game\
startPlay();

//end game\
endPlay();\
}\
}

Step 2

Create concrete classes extending the above class.

*Cricket.java*

public class Cricket extends Game {

@Override\
void endPlay() {\
System.out.println("Cricket Game Finished!");\
}

@Override\
void initialize() {\
System.out.println("Cricket Game Initialized! Start playing.");\
}

@Override\
void startPlay() {\
System.out.println("Cricket Game Started. Enjoy the game!");\
}\
}

*Football.java*

public class Football extends Game {

@Override\
void endPlay() {\
System.out.println("Football Game Finished!");\
}

@Override\
void initialize() {\
System.out.println("Football Game Initialized! Start playing.");\
}

@Override\
void startPlay() {\
System.out.println("Football Game Started. Enjoy the game!");\
}\
}

Step 3

Use the *Game*'s template method play() to demonstrate a defined way of
playing game.

*TemplatePatternDemo.java*

public class TemplatePatternDemo {\
public static void main(String\[\] args) {

Game game = new Cricket();\
game.play();\
System.out.println();\
game = new Football();\
game.play();                \
}\
}

 

 

 

Visitor Pattern

Tuesday, September 01, 2015

15:44

 

In Visitor pattern, we use a visitor class which changes the executing
algorithm of an element class. By this way, execution algorithm of
element can vary as and when visitor varies. This pattern comes under
behavior pattern category. As per the pattern, element object has to
accept the visitor object so that visitor object handles the operation
on the element object.

 

Implementation

We are going to create a ComputerPart interface defining accept
opearation.Keyboard, Mouse, Monitor and Computer are concrete classes
implementing ComputerPart interface. We will define another interface
ComputerPartVisitor which will define a visitor class operations.
Computer uses concrete visitor to do corresponding action.

 

 

> ![](media/image25.jpg){width="5.833333333333333in"
> height="4.302083333333333in"}

Step 1

Define an interface to represent element.

*ComputerPart.java*

public interface ComputerPart {\
public void accept(ComputerPartVisitor computerPartVisitor);\
}

Step 2

Create concrete classes extending the above class.

*Keyboard.java*

public class Keyboard implements ComputerPart {

@Override\
public void accept(ComputerPartVisitor computerPartVisitor) {\
computerPartVisitor.visit(this);\
}\
}

*Monitor.java*

public class Monitor implements ComputerPart {

@Override\
public void accept(ComputerPartVisitor computerPartVisitor) {\
computerPartVisitor.visit(this);\
}\
}

*Mouse.java*

public class Mouse implements ComputerPart {

@Override\
public void accept(ComputerPartVisitor computerPartVisitor) {\
computerPartVisitor.visit(this);\
}\
}

*Computer.java*

public class Computer implements ComputerPart {\
        \
ComputerPart\[\] parts;

public Computer(){\
parts = new ComputerPart\[\] {new Mouse(), new Keyboard(), new
Monitor()};                \
}

@Override\
public void accept(ComputerPartVisitor computerPartVisitor) {\
for (int i = 0; i &lt; parts.length; i++) {\
parts\[i\].accept(computerPartVisitor);\
}\
computerPartVisitor.visit(this);\
}\
}

Step 3

Define an interface to represent visitor.

*ComputerPartVisitor.java*

public interface ComputerPartVisitor {\
        public void visit(Computer computer);\
        public void visit(Mouse mouse);\
        public void visit(Keyboard keyboard);\
        public void visit(Monitor monitor);\
}

Step 4

Create concrete visitor implementing the above class.

*ComputerPartDisplayVisitor.java*

public class ComputerPartDisplayVisitor implements ComputerPartVisitor {

@Override\
public void visit(Computer computer) {\
System.out.println("Displaying Computer.");\
}

@Override\
public void visit(Mouse mouse) {\
System.out.println("Displaying Mouse.");\
}

@Override\
public void visit(Keyboard keyboard) {\
System.out.println("Displaying Keyboard.");\
}

@Override\
public void visit(Monitor monitor) {\
System.out.println("Displaying Monitor.");\
}\
}

Step 5

Use the *ComputerPartDisplayVisitor* to display parts of *Computer*.

*VisitorPatternDemo.java*

public class VisitorPatternDemo {\
public static void main(String\[\] args) {

ComputerPart computer = new Computer();\
computer.accept(new ComputerPartDisplayVisitor());\
}\
}

 

 

 

Delegate Pattern

Thursday, September 17, 2015

14:26

 

**"Delegation is like inheritance done manually through object
composition."** *\[Lecture slides of course 601: "Object-Oriented
Software Development" at the University of San Francisco \]*

![](media/image26.jpg){width="5.90625in" height="2.6354166666666665in"}

It is a technique where an object expresses certain behavior to the
outside but in reality delegates responsibility for implementing that
behaviour to an associated object. This sounds at first very similar to
the proxy pattern, but it serves a much different purpose. Delegation is
an abstraction mechanism which centralizes object (method) behaviour.

The diagram above shows how multiple-inheritance behavior can be
accomplished in Java for actual classes. Of course delegation is not
limited to scenarios where multiple-inheritance has to be avoided (as
Java does not support this), but can be seen in general as an
alternative to inheritance. The same functionality can also be
accomplished with interfaces, however sometimes the relationship you
want between two classes is actually one of containment rather than
inheritance.

Applicability / Uses

Use the delegation pattern when:

-   you need to reduce the coupling of methods to their class

-   you have components that behave identically, but realize that this
    > situation can change in the future.

Generally spoken: use delegation as alternative to inheritance.
Inheritance is a good strategy, when a close relationship exist in
between parent and child object, however, inheritance couples objects
very closely. Often, delegation is the more flexible way to express a
relationship between classes.

This pattern is also known as "proxy chains". Several other design
patterns use delegation - the State, Strategy and Visitor Patterns
depend on it.

Related Patterns

-   [Decorator](http://best-practice-software-engineering.ifs.tuwien.ac.at/patterns/decorator.html):
    > is similar to delegation and uses it heavily to accomplish
    > its task.

<!-- -->

-   Delegation is very common, it is used by many other pattern
    > like [Visitor](http://best-practice-software-engineering.ifs.tuwien.ac.at/patterns/visitor.html), [Observer](http://best-practice-software-engineering.ifs.tuwien.ac.at/patterns/observer.html), [Strategy](http://best-practice-software-engineering.ifs.tuwien.ac.at/patterns/strategy.html),
    > and [Event
    > Listener](http://best-practice-software-engineering.ifs.tuwien.ac.at/patterns/event_listener.html).

Structure

This example is actually more advanced than just plain delegation, it
shows how delegation makes it easy to compose behaviors at run-time.

![](media/image27.jpg){width="6.0in" height="2.3645833333333335in"}

Sample

First lets create an Interface for our Delegates, since Delegates can be
interchanged they all must implement the same interface:

 

public interface ISoundBehaviour {\
\
public void makeSound();\
}

public class MeowSound implements ISoundBehaviour {

public void makeSound() {\
System.out.println("Meow");\
}\
}

public class RoarSound implements ISoundBehaviour {

public void makeSound() {\
System.out.println("Roar!");\
}\
}

Now lets create a cat class which uses the MeowSound per default:

public class Cat {\
private ISoundBehaviour sound = new MeowSound();

public void makeSound() {\
this.sound.makeSound();\
}

public void setSoundBehaviour(ISoundBehaviour newsound) {\
this.sound = newsound;\
}\
}

Finally a Main class to test our delegation pattern:

public class Main {\
public static void main(String args\[\]) {\
Cat c = new Cat();\
// Delegation\
c.makeSound(); // Output: Meow\
// now to change the sound it makes\
ISoundBehaviour newsound = new RoarSound();\
c.setSoundBehaviour(newsound);\
// Delegation\
c.makeSound(); // Output: Roar!\
}\
}

 

From
&lt;<http://best-practice-software-engineering.ifs.tuwien.ac.at/patterns/delegation.html>&gt;

 

 

MVC Pattern

Tuesday, September 01, 2015

15:47

 

MVC Pattern stands for Model-View-Controller Pattern. This pattern is
used to separate application's concerns.

-   **Model** - Model represents an object or JAVA POJO carrying data.
    > It can also have logic to update controller if its data changes.

-   **View** - View represents the visualization of the data that
    > model contains.

-   **Controller** - Controller acts on both model and view. It controls
    > the data flow into model object and updates the view whenever
    > data changes. It keeps view and model separate.

 

Implementation

We are going to create a Student object acting as a model.StudentView
will be a view class which can print student details on console and
StudentController is the controller class responsible to store data in
Student object and update view StudentView accordingly.

 

> ![](media/image28.jpg){width="5.833333333333333in" height="4.125in"}

 

Step 1

Create Model.

*Student.java*

public class Student {\
private String rollNo;\
private String name;\
\
public String getRollNo() {\
return rollNo;\
}\
\
public void setRollNo(String rollNo) {\
this.rollNo = rollNo;\
}\
\
public String getName() {\
return name;\
}\
\
public void setName(String name) {\
this.name = name;\
}\
}

Step 2

Create View.

*StudentView.java*

public class StudentView {\
public void printStudentDetails(String studentName, String
studentRollNo){\
System.out.println("Student: ");\
System.out.println("Name: " + studentName);\
System.out.println("Roll No: " + studentRollNo);\
}\
}

Step 3

Create Controller.

*StudentController.java*

public class StudentController {\
private Student model;\
private StudentView view;

public StudentController(Student model, StudentView view){\
this.model = model;\
this.view = view;\
}

public void setStudentName(String name){\
model.setName(name);                \
}

public String getStudentName(){\
return model.getName();                \
}

public void setStudentRollNo(String rollNo){\
model.setRollNo(rollNo);                \
}

public String getStudentRollNo(){\
return model.getRollNo();                \
}

public void updateView(){                                \
view.printStudentDetails(model.getName(), model.getRollNo());\
}        \
}

Step 4

Use the *StudentController* methods to demonstrate MVC design pattern
usage.

*MVCPatternDemo.java*

public class MVCPatternDemo {\
public static void main(String\[\] args) {

//fetch student record based on his roll no from the database\
Student model = retriveStudentFromDatabase();

//Create a view : to write student details on console\
StudentView view = new StudentView();

StudentController controller = new StudentController(model, view);

controller.updateView();

//update model data\
controller.setStudentName("John");

controller.updateView();\
}

private static Student retriveStudentFromDatabase(){\
Student student = new Student();\
student.setName("Robert");\
student.setRollNo("10");\
return student;\
}\
}

 

 

Data Access Object Pattern

Tuesday, September 01, 2015

17:00

 

Data Access Object Pattern or DAO pattern is used to separate low level
data accessing API or operations from high level business services.
Following are the participants in Data Access Object Pattern.

-   **Data Access Object Interface** - This interface defines the
    > standard operations to be performed on a model object(s).

-   **Data Access Object concrete class** - This class implements
    > above interface. This class is responsible to get data from a data
    > source which can be database / xml or any other storage mechanism.

-   **Model Object or Value Object** - This object is simple POJO
    > containing get/set methods to store data retrieved using
    > DAO class.

 

Implementation

We are going to create a Student object acting as a Model or Value
Object.StudentDao is Data Access Object Interface.StudentDaoImpl is
concrete class implementing Data Access Object Interface.
DaoPatternDemo, our demo class, will use StudentDao to demonstrate the
use of Data Access Object pattern.

 

> ![](media/image29.jpg){width="5.833333333333333in" height="4.0in"}

 

 

Step 1

Create Value Object.

*Student.java*

public class Student {\
private String name;\
private int rollNo;

Student(String name, int rollNo){\
this.name = name;\
this.rollNo = rollNo;\
}

public String getName() {\
return name;\
}

public void setName(String name) {\
this.name = name;\
}

public int getRollNo() {\
return rollNo;\
}

public void setRollNo(int rollNo) {\
this.rollNo = rollNo;\
}\
}

Step 2

Create Data Access Object Interface.

*StudentDao.java*

import java.util.List;

public interface StudentDao {\
public List&lt;Student&gt; getAllStudents();\
public Student getStudent(int rollNo);\
public void updateStudent(Student student);\
public void deleteStudent(Student student);\
}

Step 3

Create concrete class implementing above interface.

*StudentDaoImpl.java*

import java.util.ArrayList;\
import java.util.List;

public class StudentDaoImpl implements StudentDao {\
        \
//list is working as a database\
List&lt;Student&gt; students;

public StudentDaoImpl(){\
students = new ArrayList&lt;Student&gt;();\
Student student1 = new Student("Robert",0);\
Student student2 = new Student("John",1);\
students.add(student1);\
students.add(student2);                \
}\
@Override\
public void deleteStudent(Student student) {\
students.remove(student.getRollNo());\
System.out.println("Student: Roll No " + student.getRollNo() + ",
deleted from database");\
}

//retrive list of students from the database\
@Override\
public List&lt;Student&gt; getAllStudents() {\
return students;\
}

@Override\
public Student getStudent(int rollNo) {\
return students.get(rollNo);\
}

@Override\
public void updateStudent(Student student) {\
students.get(student.getRollNo()).setName(student.getName());\
System.out.println("Student: Roll No " + student.getRollNo() + ",
updated in the database");\
}\
}

Step 4

Use the *StudentDao* to demonstrate Data Access Object pattern usage.

*DaoPatternDemo.java*

public class DaoPatternDemo {\
public static void main(String\[\] args) {\
StudentDao studentDao = new StudentDaoImpl();

//print all students\
for (Student student : studentDao.getAllStudents()) {\
System.out.println("Student: \[RollNo : " + student.getRollNo() + ",
Name : " + student.getName() + " \]");\
}

//update student\
Student student =studentDao.getAllStudents().get(0);\
student.setName("Michael");\
studentDao.updateStudent(student);

//get the student\
studentDao.getStudent(0);\
System.out.println("Student: \[RollNo : " + student.getRollNo() + ",
Name : " + student.getName() + " \]");                \
}\
}

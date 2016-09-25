Basics

Monday, February 15, 2016

13:55

 

At its core, the Ruby style of programming is built on a couple of very
simple ideas: The first is that code should be crystal clear. Since
there is a limit to how much information you can keep in your head at
any given moment, good code is not just clear, it is also concise.

 

Ruby indentation convention: In Ruby you indent your code with two
spaces per level. This means that the first level of indentation gets
two spaces, followed by four, then six, and then eight. Note that the
rule is to use two spaces per indent: The Ruby convention is to never
use tabs to indent. Ever

 

Anything following a \# in the code is a comment

 

With a few notable exceptions you should use
lowercase\_words\_separated\_by\_underscores.5 Almost everything in this
context means methods arguments and variables including instance
variables. Class names are an exception to the rule: Class names are
camel case, so Document and LegalDocument are good but Movie\_script is
not.

 

Ruby tries hard not to require any syntax it can do without and a great
example of this is its treatment of parentheses. When you define or call
a method you are free to add or omit the parentheses around the
arguments. Ruby programmers generally vote for the parentheses:

  find\_document( 'Frankenstein', 'Shelley' )   find\_document 'Frankenstein', 'Shelley'
  --------------------------------------------- ------------------------------------------

The other main exception to the “vote yes for parentheses” rule is that
we don’t do empty argument lists. If you are defining—or calling—a
method with no parameters leave the parentheses off. Finally, keep in
mind that the conditions in control statements don’t require
parentheses—and we generally leave them off

Although most Ruby code sticks to the “one statement per line” format,
it is possible to cram several Ruby statements onto a single line: All
you need to do is to insert a

semicolon between the statements. This is not usually followed, but can
be used in case of empty methods or classes or small code blocks..

 

{} or do..end are the same. The two forms of code block are essentially
identical. If your block consists of a single statement fold the whole
statement into a single line and delimit the block with braces.
Alternatively if you have a multi statement block spread the block out
over a number of lines and use the do/end form

 

Ruby programmers will usually end the name of a method that answers a
yes/no or true/false question with a question mark. So if you do peek
into Set you will find the include? method as well as superset? and
empty?. Don’t be fooled by that exotic-looking question mark: It’s just
an ordinary part of the method name not some special Ruby syntax.

 

The same thing is true of exclamation points at the end of a method
name: The Ruby rules say that ! is a fine character with which to end a
method name. In practice Ruby programmers reserve ! to adorn the names
of methods that do something unexpected or perhaps a bit dangerous. So
the Set class has flatten! and map! both of which change the class in
place instead of returning a modified copy.

 

Unless is used for reverse if conditions. **With unless, the body of the
statement is executed only if the condition is false.**

  if @writable          
  -------------------- --------------------
  if not @read\_only   unless @read\_only

 

An until loop keeps going until its conditional part becomes true. It is
reverse while loop

  while ! document.is\_printed?   until document.printed?
  ------------------------------- -------------------------

 

Collapse if into one line : @title = new\_title if @writable

Similar for while :document.print\_next\_page while
document.pages\_available?

 

*For loop - Consider using Each loop*

fonts = \[ 'courier', 'times roman', 'helvetica' \]

 

  for font in fonts   fonts.each do |font|
  ------------------- ----------------------

Ruby actually defines the for loop in terms of the each method: When you
say for font in fonts, Ruby will actually conjure up a call to
fonts.each.

So better use each loop

 

*Case Statement*

 

Ruby also sports a case statement, a multi-way decision statement
similar to the switch statement that you find in many programming
languages

 

case title

> when 'War And Peace'
>
> puts 'Tolstoy'
>
> when 'Romeo And Juliet'
>
> puts 'Shakespeare'
>
> else
>
> puts "Don't know"

End

 

Alternatively, you can use a case statement for the value it computes:

 

author = case title

> when 'War And Peace'
>
> 'Tolstoy'
>
> when 'Romeo And Juliet'
>
> 'Shakespeare'
>
> else
>
> "Don't know"
>
> end

 

More compact version is :

 

author = case title

> when 'War And Peace' then 'Tolstoy'
>
> when 'Romeo And Juliet' then 'Shakespeare'
>
> else "Don't know"
>
> end

 

In above case, if we remove else, the case might return nil.

 

**A key thing to keep in mind about all of these case statements is that
they use the ===2 operator to do the comparisons.**since classes use ===
to identify instances of themselves, you can use a case statement to
switch on the class of an object. In the same spirit, you can use a case
statement to detect a regular expression match:

 

when you are making decisions **in Ruby, only false and nil are treated
as false**. Ruby treats everything else—and I do mean everything—as
true.

 

So if flag == true is unnecessary. If flag is enough

 

defined? returns either a string that describes the thing passed in. if
the thing passed to defined? is not defined, then defined? Will return
nil. So it can be used for false checks.

 

*ternary operator or ?: operator*

 

file = all ? 'specs' : 'latest\_specs'

 

The ?: operator acts like a very compact if statement with the condition
part coming right before the question mark. If the condition (in the
example the value of all) is true then the value of the whole expression
is the thing between the question mark and the colon—'specs' in the
example. If the condition is false then the expression evaluates to the
last part the bit after the colon 'latest\_specs' in the example

 

*Initialize only if variable is empty*

 

Both entries below are valid and same. But first one is preferred.

 

  @first\_name ||= ''   @first\_name = '' unless @first\_name
  --------------------- ---------------------------------------

 

 

Collections

Monday, February 15, 2016

14:57

 

*Arrays*

 

poem\_words = \[ 'twinkle', 'little', 'star', 'how', 'I', 'wonder' \]

 

If you need to initialize an array of strings, where none of the strings
have embedded spaces, you can simply say:

poem\_words = %w{ twinkle little star how I wonder }

 

*Hash*

The traditional hash literal has you associating your keys with your
values with the so-called hash rocket, =&gt;,

 

freq = { "I" =&gt; 1, "don't" =&gt; 1, "like" =&gt; 1, "spam" =&gt; 963
}

 

Similarly using symbols : a shorter form is present

  book\_info = { :first\_name =&gt; 'Russ', :last\_name =&gt; 'Olsen' }   book\_info = { first\_name: 'Russ', last\_name: 'Olsen' }
  ----------------------------------------------------------------------- -----------------------------------------------------------

 

*Varargs *

If, in your method definition, you stick an asterisk before one of your
parameter names, that parameter will soak up any extra arguments passed
to the method. The value of the starred parameter will be an array
containing all the extra arguments

 

def echo\_all( \*args )

> args.each { |arg| puts arg }

end

 

Since ruby 1.9 the vararg can be anywhere in parameter list.

 

The jargon for a star used in this context is **splat**, as in “splat
names.”

 

We can pass hash and arrays to methods and Ruby will convert them to
hash and arrays.

 

 

***Running Through Your Collection***

 

Base loop:

for i in 0..words.size

> puts words\[i\]

end

 

Each loop:

words.each { |word| puts word }

 

Hashes also sport an each method, though the Hash version comes with a
twist

 

  movie.each { |entry| pp entry }                               Prints each entries.. Similar to java map entry
  ------------------------------------------------------------- -------------------------------------------------
  movie.each { |name, value| puts "\#{name} =&gt; \#{value}"}   Normal printing

 

 

  words.find\_index { |this\_word| word == this\_word }   Find the position of a value in array. Right way to do this…
  ------------------------------------------------------- --------------------------------------------------------------

 

*map and inject*

 

Like each and find\_index **map** takes a block and runs through the
collection calling the block for each element. The difference is that
instead of making some kind of decision based on the return from the
block the way find\_index does map cooks up a new array containing
everything the block returned in order. The map method is incredibly
useful for transforming the contents of a collection en mass.

 

lower\_case\_words = doc.words.map { |word| word.downcase }

 

Like each **inject** takes a block and calls the block with each element
of the collection. Unlike each inject passes in two arguments to the
block: Along with each element you get the current result—the current
sum if you are adding up all of the word lengths. Each time inject calls
the block it replaces the current result with the return value of the
previous call to the block. When inject runs out of elements it returns
the result as its return value.

 

total = words.inject(0.0){ |result, word| word.size + result}

 

The argument passed into inject—0.0 in the example—is the initial value
of the result. If you don’t supply an initial value, inject will skip
calling the block for the first element of the array and simply use that
element as the initial result.

 

Don’t however get the idea that only methods with names ending in ! will
change your collection. Remember the Ruby convention is that an
exclamation point at the end of a method name indicates that the method
is the dangerous or surprising version of a pair of methods. Since
making a modified copy of a collection seems very safe while changing a
collection in place can be a bit dicey we have sort and sort!. The punch
line is that there are many !-less methods in Ruby’s collection classes
methods that will cheerfully change your collection in place as an
intrinsic part of what they do. Thus push pop delete and shift are as
capable of changing your array as sort!.

 

**Ruby arrays and hashes have one thing in common that takes many
programmers by surprise: They are both ordered**. Order and arrays go
together like coders and coffee— it’s hard to imagine one without the
other. But hashes have in many programming languages and in earlier
versions of Ruby usually been any unruly bunch. The hashes available in
many other languages and in the bad old days of Ruby would mix up the
entries in a more or less random order. With the advent of Ruby 1.9
however hashes have become firmly ordered. Order is insertion order

 

There are two reasons for this preference for the bare collections over
more specialized classes. First the Ruby collection classes are so
powerful that often there is no practical reason to create a
custom-tailored collection simply to get some specialized feature.
Frequently a call to each or map is all you really need. And second all
things being equal Ruby programmers actually prefer to work with generic
collections. To the Ruby way of thinking one less class is one less
thing to go wrong. In addition I know exactly how an array is going to
react to a call to each or map which isn’t necessarily true of the
SpecializedCollectionOfStuff. When the problem is complexity the cure
might just be simplicity.

 

***Beware***

The easiest way to screw up one of these iterating methods is to change
the collection out from underneath the method.

 

array.each\_index {|i| array.delete\_at(i) if array\[i\] &lt; 0} pp
array

 

The trouble with this code is that it will tend to leave some negative
numbers behind: Removing the first one (the -10) from the array messes
up the internal indexing of the each method so much that it will miss
the second negative number

 

**In ruby array you can also plug new values anywhere you want.** So no
initial size for array

 

***Set***

Example of converting array to set.

 

require 'set'

word\_set = Set.new( words )

 

 

 

 

 

Strings

Monday, February 15, 2016

15:20

 

Single and double quoted strings are supported by Ruby. Only double
quoted Strings support string interpolation

 

Keep in mind that since a single quote is not special in a
doubled-quoted string and vice versa, you can sometimes avoid a lot of
quote escaping by surrounding your string with a different quote flavor,

 

For strings with both single and double quotes..

str = %q{"Stop", she said, "I can't live without 's and "s."}

 

The character after the q is the actual string delimiter—we used a brace
({) in the example above. If your delimiter has a natural partner the
way } goes with { then that’s the character you use to close the string.
In the example above we could have used ( and ) instead of { and }:

 

The case of the letter q that leads off your string also matters: If it
is lowercase as it has been in all of our examples so far the string
gets the limited interpretation singlequote style treatment. A string
with an uppercase Q gets the more liberal doubledquoted interpretation:

 

One nice feature of all Ruby strings is that they can span lines:

 

Finally, if you happen to have a very long multiline string, consider
using a **here document**. A here document allows you to create a
(usually long) string by sticking it

right in your code:

 

**lstrip and rstrip and strip** to strip of spaces from strings

 

  chomp   The chomp method is usefulfor those times when you are reading lines from a text file, something that tends to produce strings with unwanted line-terminating characters at the end. The chomp method will return a copy of the string with at most one newline character2 lopped from the end.
  ------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Note that chomp only does one newline at a time, so that
"hello\\n\\n\\n".chomp will return a string ending with two newlines.

 

  chop   The chop method will simply knock off the last character of the string, no matter what it is, so that "hello".chop is just "hell"
  ------ -----------------------------------------------------------------------------------------------------------------------------------

 

upcase and downcase to change case of letters. Swapcase to change case
of letters one by one

 

  Sub    The name of this method is short for substitute, and the method will enable you to search for some substring and replace it with another
  ------ ------------------------------------------------------------------------------------------------------------------------------------------
  Gsub   gsub will replace as many substrings as it possibly can

 

puts 'yes yes'.sub( 'yes', 'no' )

puts 'yes yes'.gsub( 'yes', 'no' )

 

Will print out:

no yes

no no

 

  Split   Call split with no arguments and it will return an array containing all the bits of your string that were separated by white space. Pass a string argument to split and it will break things up using that string as a delimiter,
  ------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

Like the collection classes, many of the string methods have
counterparts whose names end with a !, which modify the original string
instead of returning a modified copy.

 

*Iterate over String:* @author.each\_char {|c| puts c}

 

*Iterate over String by lines:* @content.each\_line { |line| puts line }

 

**Ruby strings are mutable**

Keep in mind that if you have these two strings:

 

first\_name = 'Karen'

given\_name = first\_name

 

In fact you only have one string: Modify first\_name:

first\_name\[0\] = 'D'

And you have also changed given\_name. You should treat Ruby strings
like any other mutable data structure.

 

 

You can, for example, use negative numbers to index from the end of the
string, with -1 being the last character in the string,

 

  first\_name\[first\_name.size - 1\]   first\_name\[-1\]
  ------------------------------------- -------------------

 

 

**Regular Expressions in Ruby**

 

In Ruby, the regular expression, or Regexp for short,5 is one of the
built-in data types, with its own special literal syntax. To make a Ruby
regular expression you encase your

pattern between forward slashes

/\\d\\d:\\d\\d (AM|PM)/

You use the =\~ operator to test whether a regular expression matches a
string. Thus, if we wanted to match the regular expression above with an
actual time we would run:

puts /\\d\\d:\\d\\d (AM|PM)/ =\~ '10:24 PM'

 

It prints 0. Meaning matched from zeroth pos. If it is say 6, meaning
mathced from 6th pos. If no match, nil is returned.

 

The =\~ operator is also ambidextrous: It doesn’t matter whether the
string or the regular expression comes first.

 

regular expressions are by default case sensitive: /AM/ will not match
'am'. Fortunately, you can turn that case sensitivity off my sticking an
i on the end of your expression,

puts "It matches!" if /AM/i =\~ 'am'

 

*Thus, you can pass a regular expression into the string gsub method,*

 

What if you only want your regular expression to match at the beginning
of the string? Again, there’s a special regular expression for that,
\\A.

/\\AOnce upon a time/

 

Note that the \\A doesn’t match the first character. Instead, it matches
the unseen leading edge of the string. Similarly, \\z (note the lower
case) matches the end of the string

 

**The circumflex \^**. The circumflex character matches two things: the
beginning of the string or the beginning of any line within the string.
Similarly, the dollar sign \$ matches the end of the string or the end
of any line within the string

 

By default, the dot will match any character except the newline
character. the .\* won’t match across the lines . . . unless we simply
turn off this behavior by adding an m to our expression

/\^Once upon a time.\*happily ever after\\.\$/m

 

 

**SYMBOLS**

 

Since we don’t use symbols for data processing tasks, they lack most of
the classic string manipulation methods. Symbols do have some special
talents that make them great for being symbols. For example, there can
only ever be one instance of any given symbol: If I mention :all twice
in my code, it is always exactly the same :all

a = :all

b = a

c = :all

 

Are all same. But

x = "all"

y = "all"

 

Then you have manufactured two different strings. Since both the strings
happen to contain the same three characters the two strings are equal in
some sense of the word but they are emphatically not identically the
same object. The fact that there can only be one instance of any given
symbol means that figuring out whether this symbol is the same as that
symbol is not only foolproof it also happens at lightning speeds.

 

Another aspect of symbols that makes them so well suited to their chosen
career is that **symbols are immutable**—once you create that :all
symbol it will be :all until the end of time.3 You cannot for example
make it uppercase or lob off the second 'l'. This means that you can use
a symbol with confidence that it will not change out from under you

 

*Since symbol comparison runs at NASCAR speeds and symbols never change,
they make ideal hash keys*

 

Hash class has special defenses built in to guard against just this kind
of thing. Inside of Hash there is special case code that makes a copy of
any keys passed in if the keys happen to be strings. The fact that the
Hash class needs to go through this ugly bit of special pleading
precisely to keep you from coming to grief with string keys is the
perfect illustration of the utility of symbols

 

It is, for example, trivially easy to turn a symbol into a string:

the\_string = :all.to\_s

 

To go in the reverse direction, you can use the to\_sym method that you
find on your strings:

the\_symbol = 'all'.to\_sym

 

you want to use strings for data, for things that you might want to
truncate, turn to uppercase, or concatenate. Use symbols when you simply
want an intelligible thing that stands for something in your code.

 

 

 

 

Objects

Monday, February 15, 2016

17:23

 

Every Ruby object is an instance of some class. Classes mainly earn
their keep by providing two key things: First, classes act as containers
for methods. Second, classes are also factories, factories for making
instances:

**During a method call, Ruby sets self to the instance that you called
the method on, (Similar to this)**

Ruby treats self as a sort of default object:

 

Every class—except one—has a superclass someplace that the class can
turn to when someone calls a method that the class doesn’t recognize. If
you don’t specify a superclass when you are defining a new class the new
class automatically becomes a direct subclass of Object

 

In Ruby the number -3 is an object. When you say -3.abs you are calling
the abs method on an object an object that goes by the name -3. It’s not
just the numbers either. In Ruby strings and symbols and regular
expressions are all objects objects that come equipped with their very
own methods: In fact virtually everything you come across in Ruby is an
object. You might for example think that true and false are a couple of
special Ruby language constructs. Not so—they’re just objects

 

Since virtually all Ruby objects can trace their ancestry back to Object
virtually all Ruby objects have a set of methods in common: the ones
they inherit from Object. So the next time you call class or
instance\_of? to see just what sort of object you have thank the Object
class for supplying those methods. The Object class is also the source
of the well-worn to\_s method which returns a string representation of
your object. It’s the to\_s method that puts relies on to turn its
arguments into printable strings

 

Alternatively, you can override to\_s for your own purposes:

 

the **eval** method defined by Object takes a string and executes the
string as if it were Ruby code. The possibilities with eval are
literally limitless: Having eval around means that every Ruby programmer
has the entire Ruby language available at a moment’s notice.

 

The Object class also supplies a set of reflection-oriented methods,
methods that let you dig into the internals of an object
.public\_methods method, which returns an array of all the method names
available on the object. There is also instance\_variables, which will
pull out the names of any instance variables buried in the object.

 

***Public, Private, and Protected***

 

Ruby lets you control the visibility of your methods. Methods can either
be public—callable by any code anywhere, or private, or protected. Ruby
methods are public by default. You can make your methods private by
adding private before the method definition:

> private \# Methods are private starting here
>
> def word\_count

 

Or by making them private after the fact:

> private :word\_count
>
>  

 

The rule is that you cannot call a private method with an explicit
object reference.

Note that **in Ruby, private methods are callable from subclasses**.
Think about it: You don’t need an explicit object reference to call a
superclass method from a subclass

 

Any instance of a class can call a protected method on any other
instance of the class. Thus, if we made word\_count protected, any
instance of Document could call word\_count on any other instance of
Document, including instances of subclasses like RomanceNovel

 

remember that just because the rules say that you can’t call some
private or protected method well you can still call it. Among the
methods that every object inherits from Object is send. If you supply
send with the name of a method and any arguments the method might need
send will call the method visibility be damned. The Ruby philosophy is
that the programmer is in charge. If you want to declare some method
private fine. Later if someone perhaps you wants to violate that privacy
fine again

 

***require***

 

The Ruby interpreter also defines another method one that takes the name
of a file reads the contents of the file and executes those contents as
Ruby code. This method maintains a list of the files it has already
processed and won’t re-execute a file that it has already seen. We call
that method require:

 

require 'date' \# A Call to a method

 

Another set of methods that play the part of language keywords are the
attr\_accessor family:

 

***Dynamic Typing***

 

In a technical sense, this combination of BaseDocument &lt;Document &lt;
Lazy -Document do work.

puts "Title: \#{doc.title}"

 

An example , BaseDocument only exists as a misguided effort to provide a
common interface for the various flavors of documents. The effort is
misguided because Ruby does not judge an object by its class hierarchy.

Nowhere do we say that the variable doc needs to be of any particular
class. Instead of looking at an object’s type to decide whether it is
the correct object Ruby simply assumes that if an object has the right
methods then it is the right kind of object. This philosophy sometimes
called duck typing 2 means that you can completely dispense with the
BaseDocument class and redo the two document classes as a couple of
completely independent propositions

 

The first is that the real compactness payoff of dynamic typing comes
not from leaving out a few int and string declarations; it comes instead
from all of the BaseDocument style abstract classes that you never write
from the interfaces that you never create from the casts and derived
types that are simply irrelevant. The second lesson is that the payoff
is not automatic. If you continue to write static type style base
classes your code will continue to be much bulkier than it might be.

 

def initialize( title, author, content )

> @title = title
>
> @author = author
>
> @content = content

end

 

Above initialization works when passed strings or objects of title and
author classes…

 

It works because Ruby’s dynamic typing means that you don’t declare the
classes of variables and parameters. That means that your classes are
not frozen together in a rigid network of type relationships. There are
no interfaces to extract no declarations to change no class hierarchies
to adjust nothing. It just works.

In Ruby any two classes that can work together will work together.
Flexibility is a huge advantage when it comes to constructing programs.
In our example the Document class does not really do anything with
@title and @author other than carry them around; the Document class
therefore has absolutely no opinion as to what the class of these
objects should be

 

Even if Document did make some demands on @title and @author, perhaps
like this:

"\#{@title.long\_name} by \#{@author.last\_name}"

 

Then we will have increased the coupling between Document and the
@author and @title objects just a bit. With the addition of the
description method Document now expects that @title will have a method
called long\_name and @author will have a last\_name method. But the
bump in coupling is as small as it can be. Document will for example
accept any object that has a long\_name method for @title.

 

Required type declarations inevitably become a ceremonial part of your
code motions you need to go through just to get your program to work. In
contrast making up for the lost documentation value of declarations in
Ruby is easy: You write code that is painfully blazingly obvious. Start
by using nice full words for class variable and method names If that
doesn’t help you can go all the way and throw in some comments

 

don’t artificially couple your classes together

 

 

 

Unit Tests

Monday, February 15, 2016

17:49

Test::Unit comes packaged with Ruby itself and is a member of the so
called XUnit family of testing frameworks

 

The very simple idea behind Test::Unit is to exercise your code in a
series of individual tests, where each test tries out one aspect of the
program. In Test::Unit, each

test is packaged in a method whose name needs to begin with test\_.

 

def test\_document\_holds\_onto\_contents

> text = 'A bunch of words'
>
> doc = Document.new('test', 'nobody', text)
>
> assert\_equal text, doc.content

End

 

One stylistic thing that his test does well is to have a nice
descriptive name. In the same spirit, we could improve our use of
assert\_equal by adding the third, optional description parameter

 

assert\_equal text, doc.content, 'Contents are still there'

 

Along with assert\_equal, Test::Unit also allows you to assert that some
arbitrary condition is true with the assert method. Thus we might check
that our words

method is returning what it should with:

assert doc.words.include?( 'bunch' )

 

To really use Test::Unit you need to roll your tests up in a class, a
subclass of Test::Unit::TestCase . Inside the class you can have any
number of test methods:

 

class DocumentTest &lt; Test::Unit::TestCase

end

 

Kicking off a Test::Unit test is about as easy as it comes: Just run the
file containing the test class with Ruby:Note that if one of the test
methods does happen to fail, Test::Unit will keep soldiering along,
running all the other tests.

 

Test::Unit provides the **setup** method along with its friend, the
**teardown** method. The setup method gets called before each test
method is run;

In the same way the teardown method gets called after each test method
gets run. The teardown method is great for closing database connections
deleting temporary files or any other general post-test tidying up. Note
that setup and teardown get called around each test method not before
and after all of the tests in the class get run.

 

To go with assert and assert\_equal we have assert\_not\_equal as well
as assert\_nil and assert\_not\_nil.

Test::Unit has a handy assert\_match, which will fail if a string does
not match a given regular expression

 

You can also check that an object is an instance of some class:

assert\_instance\_of String, 'hello'

 

And you can assert that some code raises an exception or not

 

In a more perfect world the test would focus on the behavior itself so
that the test would read something like this: About the Document class:

> When you have a document instance it should hang onto the text that
> you give it. It should also return an array containing each word in
> the document when you call the words method. And it should return the
> number of words in the document when you call the word\_count method
>
>  

**Rspec,** possibly the Ruby world’s favorite testing framework, tries
to get us to that more perfect world. RSpec tries to weave a sort of
pseudo-English out of Ruby:

 

We don’t assert things; we say that they should happen. Thus we don’t
assert that word\_count returns 4; instead we say that word\_count
should equal 4. Like Test::Unit assertions RSpec shoulds come in a wide
variety of forms

 

  doc.words.include?( 'bunch' ).should == true   doc.words.should include( 'bunch' )
  ---------------------------------------------- -------------------------------------

 

By convention, your RSpec code—generally just called a spec—goes in a
file called &lt;&lt;class name&gt;&gt;\_spec.rb,

 

A very handy feature of the spec command is its ability to hunt down all
of the spec files in a whole directory tree assuming that you follow the
&lt;&lt;class name&gt;&gt;\_ spec.rb convention. All you need to do is
supply the path to a directory instead of a file to the spec command

 

RSpec allowing you to supply code that is executed before each example.

 

before :each do

> @text = 'A bunch of words'
>
> @doc = Document.new( 'test', 'nobody', @text )

end

it 'should hold on to the contents' do

> @doc.content.should == @text

end

 

There is also an after which is the RSpec cousin of teardown and allows
you to get code executed after each example. The :each parameter means
to run the code supplied before (or after) each example. Alternatively
you can use before(:all) and after(:all) to have some code run before or
after any of the examples are run.

 

*Easy Stubs*

 

A stub is an object that implements the same interface as one of the
supporting cast members, but returns canned answers when its methods are
called.

 

The RSpec stub method is there to reduce the pain of creating stubs. To
use the stub method you pass in a hash of method names (as symbols) and
the correspond - ing values that you want those methods to return. The
stub method will give you back an object equipped exactly with those
methods methods that will return the appropriate values.

 

stub\_printer = stub :available? =&gt; true, :render =&gt; nil

 

You would end up with stub\_printer pointing at an object with two
methods available? and render methods that return true and nil
respectively. With stub there are no classes to create no methods to
code; stub does it all for you

 

Along with stub, RSpec also provides the stub! method, which will let
you stub out individual methods on any regular object you might have
lying around

 

*Easy Mocks*

 

Sometimes, however, you need a stublike object that takes more of an
active role in the test

 

A mock is a stub with an attitude. Along with knowing what canned
responses to return a mock also knows which methods should be called and
with what arguments. Critically a disappointed mock will fail the test.
Thus while a stub is there purely to get the test to work a mock is an
active participant in the test watching how it is treated and failing
the test if it doesn’t like what it sees watching

 

In addition to declaring that some method will or will not be called,
you can also specify what arguments the method should see, RSpec will
check these expectations at the end of each example, and if they aren’t
met the spec will fail.

 

there are a lot of Ruby testing frameworks and utilities around

 

For example if you decide to use Test::Unit you might want to look into
shoulda.4 The shoulda gem defines all sorts of useful utilities for your
Test::Unit tests including the ability to replace those traditional test
methods with RSpec-like examples:

Test::Unit users should also look into mocha,5 which provides mocking
facilities along the same lines as Rspec

 

If you have settled on RSpec a great place to look for examples of specs
is the RubySpec6 project. The fine folks behind RubySpec are trying to
build a complete Ruby language specification in RSpec format. The beauty
of this approach is that when they are done we will not only have a full
specification of the Ruby language that people can read but we will also
have an executable specification one that you can run against any Ruby
implementation

 

RubySpec project uses a mostly compatible RSpec offshoot called MSpec.
Although MSpec is close enough to RSpec for our “find me an example”
purposes it differs from RSpec in ways that are important if you are
trying to test the whole Ruby language

 

 

 

 

 

 

 

Classes

Monday, February 15, 2016

21:09

 

The **composed method technique** advocates dividing your class up into
methods that have three characteristics.

First each method should do a single thing—focus on solving a single
aspect of the problem. By concentrating on one thing your methods are
not only easier to write they are also easier to understand.

Second each method needs to operate at a single conceptual level: Simply
put don’t mix high-level logic with the nitty-gritty details. A method
that implements the business logic around say currency conversions
should not suddenly veer off into the details of how the various
accounts are stored in a database.

Finally each method needs to have a name that reflects its purpose.
Nothing new here; we have all heard endless lectures about picking good
method names. The time to listen to all of that haranguing is when you
are creating lots of little methods that you are trying to pull together
into a functional whole. Done right the method names guide you through
the logic of the code.

 

The composed method way of building classes is particularly effective in
Ruby because Ruby is such a “low ceremony” language. In Ruby the cost of
defining a new method is very low: just an additional def and an extra
end. Since defining a new Ruby method adds very little noise to your
code in Ruby you can get the full composed method bang for a very modest
code overhead buck.

 

*Having many fine-grained methods also tends to make your classes easier
to test.*

 

The key to preventing your composed methods from turning on you is to
remember that every method should have two things going for it. First it
should be short. And second it should be coherent. In plain English your
method should be compact but it should also do something.

 

*Object Equality*

 

Ruby’s Object class defines no less than four equality methods. There is
eql? and equal? as well as == (that’s two equal signs), not to mention
=== (that’s three equal signs).

 

Ruby uses the equal? method to test for object identity. In other words,
the only way that this:

x.equal?(y)

Should ever return true is if x and y are both references to identically
same objects. If x and y are different objects, then equal? should
always return false, no matter how

similar x and y might be

 

default implementation of ==, the one that classes inherits from Object,
does the same thing as equal?—it tests for object identity. So to check
for object equality we need to override the method and provide our own
implementation

 

*Instance of vs kind of*

 

instance\_of? test at the beginning means that the other object must be
an instance of a DocumentIdentifier—no subclasses allowed. We can loosen
the rules a bit by using kind\_of?, which will return true if the object
is an instance of DocumentIdentifier or a subclass of
DocumentIdentifier:

 

*To check for method equality:* Using the respond\_to? method, the
DocumentPointer class asks if this other object has a name method and a
folder method. If so, then it might be an equal. Using this approach,
instances of DocumentPointer will accept an instance of a completely
unrelated class—Document - Identifier for example—as an equal

 

***Important to Consider symmetry and transitive props for equality
checks..***

 

The main use for === is in case statements.Take strings and regular
expressions for example. Strings are not regular expressions and regular
expressions are not strings, so we

certainly would not want a string to be equal to a regular expression
according to == even if they do match. So ==== is used in this case.

By default, === calls the double equals method, so unless you
specifically override ===, wherever you send ==, === is sure to follow.
It’s probably a good idea to leave ===

alone unless doing so results in really ugly case statements

 

***Hash Tables and the eql? Method***

 

The idea behind a hash is to build a thing that works a lot like an
array, but an array on performance-enhancing drugs. The feature that
makes hashes special is that they can take things other than just
numbers as indexes

 

When you need to find a value by its key you simply do a linear search
down that list looking at each key until you find the one you want. The
trouble with this simple implementation is that performance falls off in
direct proportion to the number of entries in the table.

Real hash tables improve the performance of this simple model with a
divide-and conquer strategy. Instead of maintaining a single key/value
list a typical hash table implementation maintains a number of lists or
buckets. By spreading out the stuff that’s stored in the table across a
number of buckets a hash table can do things dramatically faster. Take
that 10 000 entry table: If you spread the 10 000 entries over 100
different buckets instead of having to look at 5 000 entries to find the
one you want you only need to search through about 50. The challenging
thing with this scheme is picking the right bucket

 

You define a method on all of your objects a method which returns a hash
value. The hash value is a more or less random number somehow generated
from the value of the object. When you need to store a key/value pair in
your hash table you pull the hash value from the key. You then use that
number to pick a bucket—typically by using the modulo operator
(hash\_code % number\_of\_buckets)—and you store your key/value pair in
that bucket. Later on when you are looking to retrieve the value
associated with some key you get the hash code for the key again and use
it to pick the right bucket to search

 

Hash codes need to have a couple of properties to make this all work.
First they need to be stable over time: If a key generates one hash code
now and a different one later we are inevitably going to end up looking
in the wrong bucket. Hash codes also need to be consistent with the
value of the key: If two keys are equal—if they should return the same
value out of the hash table—then when asked they must return the same
hash code.

 

The Hash class calls the aptly named hash method (another one of those
methods that you inherit from Object) to get the hash code from its
keys. The Hash class uses the eql? method to decide if two keys are in
fact the same key. The default implementations of hash and eql? from the
Object class like the default implementations of == and === are based on
object identity: The default eql? returns true only if the other object
is identically the same as this object. The default hash method returns
the object\_id of the object which is guaranteed to be unique.

 

There is, however, no rule saying that your class needs to accept the
default implementation. As long as you follow the hash Prime
Directive—that if a.eql?(b) then a.hash == b.hash—you are free to
override these two methods.

 

Ruby’s built-in numeric classes do a bit of equality slight of hand
right under your nose. A little exploration will show that integers
(that is, instances of Fixnum or Bignum) will accept instances of Float
as equals, at least according to the == method.

 

keep in mind that &lt;=&gt; should be consistent with ==. That is, if a
&lt;=&gt; b evaluates to zero, then a == b should be true. The good news
is that Ruby actually supplies a mixin module . If you define a
&lt;=&gt; operator for your class, and include Comparable,

 

Ruby classes—those objects that are instances of Class—have their own
twist on the triple equality method: Classes treat the === method as an
alias for kind\_of?. This is so that you can pick out the class of an
object with a case statement, This is yet another asymmetric
relationship: Although Float === 1.0 is true, 1.0 === Float is not.

 

**Singletons**

 

In Ruby, a **singleton method** is a method that is defined for exactly
one object instance . the term “singleton” as it is used here has
nothing to do with the Singleton Pattern of design patterns fame. It’s
just an unfortunate collision of terminology.

The mechanics of defining singleton methods are really pretty simple:
Instead of saying def method\_name as you would to define a regular
garden-variety method, you define

a singleton method with def instance.method\_name. Singleton methods are
in all respects ordinary methods: They can accept arguments, return
values, and do anything else that a regular method can do. The only
difference is that singleton methods are stuck to a single object
instance.

 

Singleton methods override any regular, class-defined methods

 

There is also an alternative syntax for defining singleton methods, one
that can be less bulky if you are creating a lot of methods

class &lt;&lt; hand\_built\_stub\_printer

> -- define methods here..

End

 

The key is that every Ruby object carries around an additional somewhat
shadowy class of its own. this more or less secret class—**the singleton
class**—sits between every object and its regular class.3 The singleton
class starts out as just a methodless shell and is therefore pretty
invisible.4 It’s only when you add something to it that the singleton
class steps out of the shadows and makes its existence felt.

 

Since it sits directly above the instance, the singleton class has the
first say on how the object is going to behave, which is why methods
defined in the singleton class will win out over methods defined in the
object’s regular class, and in the superclasses

 

![](media/image1.png){width="2.6041666666666665in" height="2.78125in"}

can even get hold of the singleton class, like this:

 

singleton\_class = class &lt;&lt; hand\_built\_stub\_printer

> self

end

 

When you do the class &lt;&lt; hand\_built\_stub\_printer you change
context so that self is the singleton class. Since class definitions
like most Ruby expressions return the last thing they evaluate simply
sticking self inside the class definition causes the whole class
statement to return the singleton class

 

*More Explanation*

 

Ruby provides a way around this - you can define methods that are
available only for a specific object. Such methods are called *Singleton
Methods*.

 

class Foo

end

 

foo=Foo.new

def foo.shout

puts "Foo Foo Foo!"

end

foo.shout

 

 Apparently, no new instances of Foo can respond to shout - only the
object to which this method was added to can. Thus it appears that the
object foo holds the method shout all by itself.

However, singleton methods contradict what we found early: instance
objects cannot hold methods, only class definitions (objects of class
Class) can. It happens that the truth is somewhere in-between.

When you declare a singleton method on an object, Ruby automatically
creates a class to hold just that method. This class is called the
'metaclass' of the object. All subsequent singleton methods of this
object goes to its metaclass. Whenever you send a message to the object,
it first looks to see whether the method exists in its metaclass. If it
is not there, it gets propagated to the actual class of the object and
if it is not found there, the message traverses the inheritance
hierarchy.

 

*Objects in Ruby only store the state. Its behaviour comes from its
class definition.*

*Objects can also have methods that are independent of the parent class
definition. They are called singleton methods and are stored on the
metaclass of the object. The metaclass is typically invisible to the
programmer.*

 

 

**class methods are actually singleton methods in disguise**

 

Any given class say Document is an instance of Class. This means that it
inherits all kinds of methods from Class methods like name and
superclass. When we want to add a class method we want that new method
to exist only on the one class (Document in the example) not on all
classes. Since the object that goes by the name of Document is an
instance of Class we need to create a method that exists only on the one
object (Document) and not on any of the other instances of the same
class. What we need is a singleton method.

 

**A common use for class methods is to provide alternative methods for
constructing new instances**

 

Plain nonclass singleton methods are as rare as class methods are
common. In fact their main use in real code is the one we explored
earlier in this chapter building mocks and stubs for testing frameworks.
Both RSpec and the Mocha framework that we looked at briefly in Chapter
9 use singleton methods to do their mocking magic.

 

Remember, when you define a class method, it is a method attached to a
class. The instances of the class will not know anything about that
method

 

class Document

> def self.create\_test\_document( length )
>
> Document.new( 'test', 'test', 'test ' \* length )
>
> end
>
> \# ...

end

 

Then you can call that method via the class:

> book = Document.create\_test\_document( 10000 )

 

But Document instances are completely ignorant of the Document class
methods, so that this:

> longer\_doc = book.create\_test\_document( 20000 )

Will give you this:

> NoMethodError:

 

Well, perhaps not completely ignorant, since instances do know all about
their classes:

> longer\_doc = book.class.create\_test\_document( 20000 )

 

 

A bit more subtle is the confusion over the value of self during the
execution of a class method when you mix classes, subclasses, and class
methods

 

class Parent

> def self.who\_am\_i
>
> puts "The value of self is \#{self}"
>
> end

end

class Child &lt; Parent

end

 

Now, clearly, if you run Parent.who\_am\_i you would expect the
following output:

> The value of self is Parent

 

But what happens if you run Child.who\_am\_i? The answer is that self is
always the thing before the period when you called the class method:

> The value of self is Child

 

 

 

Classes - 1

Tuesday, February 16, 2016

13:38

 

Class variables start with two @’s instead of one and are associated
with a class instead of an ordinary instance.

Since class variables are not visible to the outside world, we also
supply a pair of accessor methods. A nice thing about class variables is
that they are visible to instances of the class,

 

*class variables, how they are resolved.*

 

Does the current class already have an @@named class variable? If it
does, then the search is over and the @@namede is found and set.

If the class variable is not defined in the current class Ruby will go
looking up the inheritance tree for it. (Inheritance tree is looked
first..) So if there is no @@default\_paper\_size in the current class
Ruby will look for one in the superclass and then the super superclass
until it either finds a @@default\_paper\_size defined on one of those
classes or runs out of classes. If Ruby does find @@default\_paper\_size
somewhere in the inheritance tree that’s the one that gets set. If Ruby
runs out of classes without finding @@default\_paper\_size then it will
create a new class variable in the current class.

Looking up the value of a class variable works pretty much the same way.
Ruby starts with the current class and looks up the inheritance tree; it
either finds the variable or runs out of classes and throws a NameError
exception

 

The problem is that this method for resolving class variables means they
have a tendency to wander from class to class.

 

 

Imagine two subclasses of a super class. The Super class needs to be
loaded before subclasses. Setting class variables in sub class is no
problem. Both classes have their own class variable instance .But what
happens when the super class, class level variable is set? Inheritance
tree is looked and so the super class is changed and so both sub classes
gets variable value changed. Instead of two separate variables,, there
is now only one variable, one that lives up in the Super class

 

 

*Class Instance Variables*

 

The more controllable alternative to the class variable is the class
instance variable. single @ instance variables that happen to find
themselves attached to a class object.

 

**inside a class method, self is always the class.**

 

Class instance variables are a very Ruby solution to the problem holding
onto classwide values. There is no extra syntax and no elaborate special
case rules: @default\_font is simply an instance variable on an object.
The only remotely interesting thing here is that the object happens to
be a class.

 

What would happen if you set an ordinary instance variable inside a
class method

 

def self.default\_font=(font)

> @default\_font = font

end

The answer is that since @default\_font = font always sets an instance
variable on self, the default\_font= method above will set the
@default\_font instance variable on the class object

 

*The short answer is that class instance variables do just fine with
subclasses*

 

The subclass instance variable is completely separate from the super
class instance variabl, and as long as you are careful with which one
you are talking about, super.default\_font or sub.default\_font, life
will be good.

 

 

So how do you use attr\_accessor to get at a class instance variable?

class Document

> attr\_accessor :default\_font

end

 

You end up being able to get and set an *instance variable* called
default\_font.

 

Remember that class methods are just singleton methods on a class
object. The trick to defining class-level attributes is to make self be
the Document singleton class first:

class &lt;&lt; self

> attr\_accessor :default\_font

end

 

will end up with a Document class that has a couple of class methods,
one to get the default font and the other to set it.

 

 

 

Operators

Monday, February 15, 2016

21:16

 

The Ruby mechanism for defining your own operators is straightforward
and based on the fact that Ruby translates every expression involving
programmer-definable

operators into an equivalent expression where the operators are replaced
with method calls.

So when you say this:

> sum = first + second

What you are really saying is:

> sum = first.+(second)

The second expression sets the variable sum to the result of calling the
+ method on first, passing in second as an argument.

 

The Ruby interpreter is clever about the operator-to-method translation
process and will make sure that the translated expression respects
operator precedence

and parentheses, so that this:

> result = first + second \* (third - fourth)

Will smoothly translate into:

> result = first.+(second.\*(third.-(fourth)))

 

What this means is that creating a class that supports operators boils
down to defining a bunch of instance methods, methods with names like +,
-, and \*.

 

> def +(other)
>
> Document.new( title, author, "\#{content} \#{other.content}" )
>
> end
>
> total\_document = doc1 + doc2

 

&lt;&lt; operator has taken on a second meaning as the concatenation, or
“add another one,” operator

 

The not operator, along with and, or,||, and &&, are built in to Ruby,
and their behavior is fixed.

 

To create the unary operator, you need to define a method with the
special (and rather arbitrary) name +@. The same pattern applies to -:
The plain old - method defines the binary operator while -@ defines the
unary one.

 

When you say foo\[4\] you are really calling the \[\] method on
foo,passing in four as an argument. Similarly, when you say foo\[4\] =
99, you are actually calling the \[\]= method on foo, passing in four
and ninety-nine.

 

**string formatting operator, %.** The formatting operator is great when
you need to construct a string and you need more control than the usual
Ruby "string

\#{interpolation}" gives you. A very simple formatting example would
look something like this:

"The value of n is %d" % 42

 

you can use the equivalent **sprintf** method,4 which is defined on all
Ruby objects.

 

 

 

 

Modules and Mixins

Tuesday, February 16, 2016

14:02

 

A Ruby module is the container part of a class without the factory. You
can’t instantiate a module, but you can put things inside of a module.
Modules can hold methods, constants, classes, and even other modules

Getting at the classes in a module is as simple as pasting the module
name on the front of the class name with a couple of colons. To get at
that font class above you just say Rendering::Font. Wrapping a module
around your classes in this way gives you a couple of advantages. It
allows you to group together related classes. Second,, you are
dramatically reducing the probability that there is a name collision.

 

Modules can also hold constants. you can access your constants in the
same way that you access the classes, using ::

Finally, modules can be nested,

 

Along with classes and constants and other modules, you can use modules
to enclose individual methods. Modules make great homes for those pesky
methods that just

don’t seem to fit anywhere else . Defining them this way—analogous to
class-level methods—allows us to call them directly from the module. We
can also get at module-level methods with the double-colon syntax, but
generally Ruby programmers tend to stick to the period

 

Can build a big module by combing small modules by importing them using
require.

 

Since modules are just objects, we can treat them like any other object.
In particular, we can point a variable at a module and then use that
variable in place of the module.

You can take advantage of the object-ness of modules to swap out whole
groups of related classes and constants—and even sub-modules!—at runtime

 

***MIXINS***

 

Mixins allow you to easily share common code among otherwise unrelated
classes. Mixins are custom-designed for those situations where you have
a method or six that need to be included in a number of different
classes that have nothing else in common.

The way to solve the problem of sharing code among otherwise unrelated
classes is by creating a mixin module. Create a module, add common
methods and include the module in the classes as needed.

 

The Ruby jargon is that by including a module in a class you have mixed
it in to the class. A very useful aspect of mixins is that they are not
limited by the “one superclass

is all you get” rule. You can mix as many modules into a class as you
like.

In practice this means that if you have several unrelated classes that
need to share some code you don’t have to resort to restructuring your
whole inheritance tree to get at that code. All you need to do is wrap
the common stuff in a module and include that module in the classes that
need it

 

Extending a module in class makes the methods as class level methods.

 

When you mix a module into a class, Ruby rewires the class hierarchy a
bit, inserting the module as a sort of pseudo superclass of the class.
This explains how the module methods appear in the including
classes—they effectively become methods just up the inheritance chain
from the class.

 

Although including a module inserts it into the class hierarchy, Ruby is
a bit circumspect about this fact: No matter how many modules a class
includes, instances of the class will still claim to be, well, instances
of the class.

 

You can discover whether the class of an instance includes a given
module with the kind\_of? method. So if Document includes the
WritingQuality module, then my\_tome.kind\_of?(WritingQuality) will
return true. You can also use the ancestors method to see the complete
inheritance ancestry—modules included—of a class,

 

can you override a method in a module by defining that method in the
class that includes the module? Once you know that a mixin module
effectively becomes a superclass when it is included the answer is easy
to come by: Yes. Since we know that the methods in a superclass cannot
override the methods in subclasses we can deduce that no module method
can ever override a method in its host class. Call the method and Ruby
will look first in the class find it there and never go looking in any
included modules

 

A similar “who wins?” question arises if we have the same method in two
modules and include them both in the same class. Include a module and it
becomes the nearest parent “class” of the including class. Include a
second module and it becomes the nearest parent of the including class
bumping the other module into second place

 

Mixin modules are also very convenient places to stash constants. Since
including a module in a class inserts the module into the class
hierarchy the including class not only gains access to the module’s
methods but also to its constants

 

 

 

 

 

 

 

 

Blocks

Tuesday, February 16, 2016

20:43

 

In Ruby you create code blocks by tacking them on to the end of a method
call, like this

do\_something do

> puts "Hello from inside the block"

End

 

When you tack a block onto the end of a method call Ruby will package up
the block as sort of a secret argument and (behind the scenes) passes
this secret argument to the method. Inside the method you can detect
whether your caller has actually passed in a block with the
block\_given? method and fire off the block (if there is one) with
yield:

 

def do\_something

> yield if block\_given?

end

 

Blocks can take arguments, which you supply as arguments to yield,

 

def do\_something\_with\_an\_arg

> yield("Hello World") if block\_given?

end

 

do\_something\_with\_an\_arg do |message|

> puts "The message is \#{message}"

end

 

Finally, like most everything else in Ruby, code blocks always return a
value—the last expression that the block executes—which your yielding
method can either use or

ignore as it sees fit

 

An iterator method calls its block once for each element in some
collection, passing the element into the block as a parameter. We can
add custom one to a class

 

An aspect of iterators that beginners often overlook is that you can
write iterators that run through collections that don’t actually exist,
at least not all at the same time. The simplest example of this sort of
thing is the times method that you find on Ruby integers

 

12.times { |x| puts "The number is \#{x}" }

 

This code will print out the first dozen integers but it will print them
without ever assembling a twelve-element collection. Instead the times
method produces each number one at a time and feeds it to the block. So
far so obvious. What’s not so obvious is that you can use this same
trick to build your own iterators. Just pass the objects to the block
and we don’t need to generate arrays on our own.

 

**The Ruby convention is to name the main iterator of your class each.**

 

There is however another reason to follow the crowd and name that key
iterating method each: Doing so enables you to use the Enumerable
module. The Enumerable module is a mixin that endows classes with all
sorts of interesting collection-related methods.

 

The simple act of including Enumerable adds a plethora of
collection-related methods to your class, methods that all rely on your
each method.

Enumerable also enhances your class with a to\_a method that returns an
array of all of the items in our case words in your collection. The
Enumerable module also adds methods that help you find things in your
collection methods with names like find and find\_all. Enumerable also
contributes the each\_cons method to your class. The
each\_cons(consecutive?) method takes an integer and a block and will
repeatedly call the block each time passing in an array of consecutive
elements from the collection.

 

Along the same lines as each\_cons Enumerable also supplies each\_slice
which simply breaks up the collection in chunks of a given size and
passes those into the block. Finally if the elements in your collection
define the &lt;=&gt; operator you can use the Enumerable-supplied sort
method which will return a sorted array of all the elements in your
collection

 

Along with Enumerable Ruby also comes with the Enumerator class. If you
create an Enumerator instance passing in your collection and the name of
the iterating method what you will get is an object that knows how to
sequence through your collection using that method

 

For example, if you make a new Enumerator based on a Document instance
and the each\_character method:

> doc = Document.new('example', 'russ', "We are all characters")
>
> enum = Enumerator.new( doc, :each\_character )

Then you will end up with an object with all of the nice Enumerable
methods based on the each\_character method. Thus you can discover the
number of characters in

your document text:

> puts enum.count

Or sort the characters:

> pp enum.sort

 

The primary way that an iterator method can come to grief is by trusting
the block too much. Remember the code block you get handed in your
iterator method is someone else’s code. You need to regard the block as
something akin to a hand grenade ready to go off at any second. Blocks
can also blow up in your face with an exception.

 

Ruby allows applications to call break in mid-block. The idea is to give
the code using an iterating method a way to escape early.

When called from inside of a block break will trigger a return out of
the method that called the block. An explicit return from inside the
block triggers an even bigger jump: It causes the method that defined
(not called) the block to return. This is generally what you want to
simulate breaking out of or returning from a built-in loop. Fortunately
like exceptions both break and return will trigger any surrounding
ensure clauses.

 

*Execute around Modules*

 

For example instead of putting logging in all methods, we can have a
method that does logging and pass the exectute function as a block to
it.. See example below..

 

def with\_logging(description)

> begin
>
> @logger.debug( "Starting \#{description}" )
>
> yield
>
> @logger.debug( "Completed \#{description}" )
>
> rescue
>
> @logger.error( "\#{description} failed!!")
>
> raise
>
> end
>
> end

end

 

Call it as :

 

with\_logging('load') { @doc = Document.load( 'resume.txt' ) }

with\_logging('save') { @doc.save }

 

Or even:

 

with\_logging( 'Compute miles in a light year' ) do

> 186000 \* 60 \* 60 \* 24 \* 365

end

 

Its generic…!!!

 

This simple “bury the details in a method that takes a block” technique
goes by the name of **execute around.**

 

Use execute around when you have something—like the logging in the
previous example—that needs to happen before or after some operation or
when the operation fails with a exception. Instead of laboriously
sprinkling intention- obscuring code far and wide you build a method
that takes a code block. Inside the method you do whatever preparation
needs doing; in our example it was logging the initial message. Then you
call the block followed by any clean-up work which in the example was
the second log message. You can (and probably should) also catch any
exceptions that come roaring out of the block2 and do the right thing
with them

 

Now although the name “execute around” comes from the full-blown idea of
a method that does something before and after the block gets executed
there is no rule saying you can’t build a slightly degenerate execute
around method that omits the after bit Or the before part.

 

Even if you do leave one or the other parts out, the idea is the same:
Execute around uses a code block to interleave some standard bit of
processing with whatever

it is that the block does (Similar to AOP?)

 

Execute around can also help you get your objects initialized

 

def initialize(title, author, content = '')

> @title = title
>
> @author = author
>
> @content = content
>
> yield( self ) if block\_given?

End

 

And call it as:

 

new\_doc = Document.new( 'US Constitution', 'Madison', '' ) do |d|

> d.content &lt;&lt; 'We the people'
>
> d.content &lt;&lt; 'In order to form a more perfect union'
>
> d.content &lt;&lt; 'provide for the common defense'

end

 

A key part of doing a successful execute around method is paying
attention to what goes into and what comes out of the code block.

 

**All of the variables that are visible just before the opening do or {
are still visible inside the code block. Code blocks drag along the
scope in which they were created**

**wherever they go.**

 

A good rule of thumb is that the only arguments you should pass from the
application into an execute around method are those that the execute
around method

itself, not the block, will use.

 

Similarly, there is nothing wrong with the execute around method passing
arguments that originate in the method itself into the block; in fact,
many execute around

methods do exactly that.

 

Another thing you need to consider with execute around methods is that
the application might want to return something from the block. Can
capture the return value from yield and then return from the method..

 

In fact exception handling is even more important with execute around
than it is with iterators because execute around is all about
guarantees. The whole idea of execute around is that the caller is
guaranteed that this will happen before the code block fires and that
will happen after. Don’t let some stray exception sully the reputation
of your method for absolutely positively getting the job done. With
execute around you also need to consider the human factor: A critical
difference between just using execute around and really applying it
elegantly lies in the name you pick for your method. A good name should
make sense in the context of the application code the code that is
calling the method. Don’t think of it so much as naming a new method as
naming a new feature that you are adding to the Ruby language

 

 

*Save block to execute later*

 

As we have seen, block\_supplied? and yield rely on the fact that Ruby
treats a code block appended to the end of a method call as a sort of
implicit parameter

to the call, a parameter that only yield and block\_supplied? know how
to get at.

 

However implicitly is not the only way to pass blocks to your methods.
If you add a parameter prefixed with an ampersand to the end of your
parameter list 1 Ruby will turn any block passed into the method into a
garden-variety parameter. After you have captured a block with an
explicit parameter you can run it by calling its call method.

 

def run\_that\_block( &that\_block )

> puts "About to run the block"
>
> that\_block.call
>
> puts "Done running the block"

end

 

It’s also trivially easy to figure out whether the caller actually did
pass in a block: Just check to see if the value of the block parameter
is nil:

> that\_block.call if that\_block

 

Explicit code blocks are easy and clear enough that some Ruby
programmers (including me!) habitually use them rather than the implicit
variety. Explicit block parameters make it easy to determine at a glance
which methods expect a code block. Methods with an explicit code block
parameter can also treat the block as an ordinary object instead of some
freakish special case. Stylistic considerations aside explicit code
block parameters allow you to do something that is impossible with the
implicit variety: When you use explicit block parameters you can hold
onto the block and store a reference to it like any other object. And
that means you can execute the block later perhaps much later possibly
long after the method that caught the block has returned

 

 

A different, and really elegant, way to solve the call back problem is
to use explicit code block parameters

def on\_save( &block )

> @save\_listener = block

end

 

def save( path )

> File.open( path, 'w' ) { |f| f.print( @contents ) }
>
> @save\_listener.call( self, path ) if @save\_listener

end

 

my\_doc.on\_save do |doc|

> puts "Hey, I've been saved!"

end

 

Being able to capture a code block for later use opens ups other
possibilities: For example, you can use saved code blocks for lazy
initialization.

We can pass a block to the method and let decide what being passed
during the invocation..

 

**object version of a block, which is actually an instance of the Proc
class**

 

When it comes to creating Proc objects, beware of false friends.
Although calling Proc.new is nearly synonymous with lambda

It’s not quite synonymous enough. The object you get back from Proc.new
differs from what you would get back from lambda in two key ways. One
relatively

innocu-ous difference is that a Proc.new object is very forgiving of the
number of arguments passed to its call method. Pass too few and it will
set the excess block parameters to nil; pass too many and it will
quietly ignore the extra arguments. In contrast, the call method on an
object returned by lambda acts more like a regular method and will throw
an exception if you mess up the argument count.

 

The second difference is much more critical. Objects from Proc.new
feature all of the interesting return break and next behavior that we
touched on in the last couple of chapters. For example if a Proc.new
block executes an explicit return Ruby will try to return not just from
the block but from the method that created the block. This behavior is
great for iterators but it can be a disaster for applications that hang
onto code blocks long after the method that created them has returned.
In contrast the Proc object returned from lambda acts more like a
portable method—a return from a lambda wrapped block will simply return
from the block and no further

 

You can also get into trouble with the closure nature of code blocks.
The fact that code blocks drag along the variables from the code that
defines them is mostly a convenience but it can also have unexpected and
unpleasant consequences. Mostly this has to do with variables staying in
scope and therefore in existence for longer than you might expect

 

 

 

 

Hooks

Wednesday, February 17, 2016

10:56

 

A Ruby hook is some way—sometimes by supplying a block and sometimes by
just overriding a method—to specify the code to be executed when
something specific happens

 

A great example of a hook is the one that tells you when a class gains a
subclass. To stay informed of the appearance of new subclasses, you
define a class-level method called inherited

 

class SimpleBaseClass

> def self.inherited( new\_subclass )
>
> puts "Hey \#{new\_subclass} is now a subclass of \#{self}!"
>
> end

end

 

The module analog of inherited is included. As the name suggests,
included gets called when a module gets included in a class

 

The at\_exit hook is the Ruby’s equivalent of the Grim Reaper: It only
drops in when you—or rather, your Ruby application—is on its way out.
The at\_exit hook gets

called just before the Ruby interpreter exits. Using at\_exit is a bit
different from the other hooks we have seen. Instead of overriding
something, with at\_exit you just call at\_exit with a block: The Ruby
interpreter will fire off the block just before it expires. An advantage
of this code-block approach is that you can call at\_exit several times,
passing in different blocks each time. If you do call at\_exit more than
once, then when your application is ready to exit each block will get
called in “last in/first out” order.

 

Look inside Test::Unit and you will see

that it uses at\_exit to trigger the test just before the Ruby
interpreter exits. Here is

the actual code:

> at\_exit do
>
> unless \$! || Test::Unit.run?
>
> exit Test::Unit::AutoRunner.run
>
> end
>
> end

 

This actually is a fairly sophisticated bit of Ruby: The unless
statement in the at\_exit block first looks at the \$! variable2 to see
whether there has been an error and does nothing if there has been. This
check prevents Test::Unit from trying to run the tests in the face of
gross problems like syntax errors in the test code itself. If \$! is nil
the unless statement next checks to see whether the tests have already
been run. It is possible using the Test::Unit API to run the tests
manually and if that is the case Test::Unit doesn’t want to run them a
second time. If neither of these conditions apply then Test::Unit will
happily—and automatically—run your tests for you.

 

**\$! is a global variable that Ruby sets to the last exception
raised.**

 

One way to find out lies in the details of how Ruby calls a method, and,
in particular, what it does when the method it is trying to call is not
actually there. Initially, Ruby will look for the method in the Document
class and, failing to find it there, it will look in the superclass for
text, and on up the line. If Ruby finds the method anywhere in the
inheritance tree, then that’s the method that gets called.

 

When Ruby fails to find a method, it turns around and calls a second
method. This second call, to a method with the somewhat odd name of
method\_missing, is what eventually generates the exception. It’s the
default implementation of method\_missing, found in the Object class2
that raises the NameError. More specifically, the default
method\_missing actually lives in the Kernel module, which is included
by Object. You are free to override method\_missing in any of your
classes and handle the case of the missing method yourself exception.
method\_missing gets passed the name of the original method that was
called along with the augments it was called with

 

In the same way that Ruby provides method\_missing to cope with calls to
nonexistent methods, it also gives you const\_missing to deal with
constants. As you might guess const\_missing works a lot like
method\_missing: It gets called whenever Ruby detects a reference to an
undefined constant. There are a couple of differences between the two
\_missing methods one obvious and one more subtle. The obvious
difference is that const\_missing takes only a single argument a symbol
containing the name of the missing constant. References to constants
unlike method calls do not have arguments. The less obvious difference
is that const\_missing needs to be a class method:

 

There are a few things to remember about method\_missing- and
const\_missingbased error handling. First, you don’t want to use it
unless you really need it. Second keep in mind that the penalty for
screwing up in method\_missing and const\_missing can be pretty high.
Think about it: Ruby executes method\_missing any time there is a method
call that it can’t locate. Be very very careful that you don’t
inadvertently call a nonexistent method inside your method\_missing
method leading to infinite recursion

 

***Delegation***

 

In the programming world delegation is the idea that an object might
secretly use another object to get part of the job done. Delegation—the
coding edition—is a pretty basic concept: Sometimes you find yourself
building an object that wants to do something and you happen to have
another object that does exactly that something. You could copy all of
the code from one class to the other but that is probably a bad idea.1
Instead what you do is delegate: You supply the first object with a
reference to the second and every time you need to do that something you
call the right method on the other object. Delegation is just another
word for foisting the work on another object

 

def method\_missing(name, \*args)

> check\_for\_expiration
>
> @original\_document.send(name, \*args)

end

 

Shown above is use of method missing to implement cool delegation in
just one method rather than implementing delegation for a number of
methods. Here there is no chance of infinite recursion as detailed above
as we are forwarding the call and not directly invoking the method.

 

If a delegating object actually has a method, the way our all instances
have a to\_s method, then the method is not actually missing and
method\_missing is not going to go off for that method. There is an easy
way out of this conundrum, BasicObject. BasicObject was introduced in
Ruby 1.9 and is the superclass of Object . As the name suggests,
BasicObject is very stripped down: Instances of BasicObject inherit only
a handful of methods. This means that BasicObject is an ideal candidate
to start with when you are doing the kind of mass delegation.

 

In late-model ActiveRecord versions the first time you access the\_
employee.first\_name the method\_missing method will go off just like it
did in the olden days. But instead of simply looking up the field value
the newer method\_missing will also define the first\_name and (for good
measure) last\_name methods on the class. It’s these newly defined
methods that get used on subsequent calls. Apparently skipping the
method\_missing rigmarole improves performance enough to make the whole
thing worthwhile. It is also impressive to watch.

 

Another thing you can do with method\_missing is try to figure out what
the user is asking you to do and actually do it. What if whenever
someone called a nonexistent method on one of your FormLetter objects
you looked at the method name to see whether you could make sense out of
it? If you can you do the right thing. If not there is always
NameException to raise.

 

This variation on method\_missing is sometimes called **magic methods,**
since users of the class can make up method names and, as long as the
names comply with the rules coded into method\_missing, the methods will
just magically work.

 

You also need to be aware of the likelihood that using method\_missing
will muck up the respond\_to? method. Every Object instance includes a
method called respond\_to?

which should return true if the object in question has a particular
method. The problem is that the default implementation of respond\_to?
only knows about the real methods; it has no way of knowing that you
have slapped a method\_missing on your class. Depending on how elaborate
your method\_missing implementation is, you may be able to fix
respond\_to?:

 

***Open Class***

Ruby’s open classes means that you can change the behavior of any class
at any time. You can add new methods. You can replace the code behind an
existing method. You can even delete methods altogether. It turns out
that open classes—and the monkey patching technique that goes with
them—is actually a very practical solution to a number of programming
problems

 

The first time you define a new class, you are, well, defining a new
class say Document. If you write another class statement for Document:
Then you are not defining a new class. Rather, you are modifying the
existing Document class, the same one you defined in the first bit of
code. Even better, the changes you make to your classes will be felt
instantly by all of the instances of the class

class Document

End

 

class Document

> def words
>
> @content.split
>
> end

end

 

The effect of this second chunk of code is to add the words method to
Document.

 

It is possible and not that unusual to redefine existing methods on Ruby
classes. This works on the “last def wins” principal: If you reopen a
class and define a method that already exists the new definition
overwrites the old. This sort of thing is handy when you need to fix a
broken class. This technique of modifying existing classes on the fly
goes by the name of **monkey patching**

 

 

**alias\_method** actually copies a method implementation, giving it a
new name along the way. For example, our original Document class had a
method called word\_count. With alias\_method, we can create a couple
more methods that do exactly the same thing as word\_count

 

class Document

\# Stuff omitted...

> def word\_count
>
> words.size
>
> end
>
> alias\_method :number\_of\_words, :word\_count
>
> alias\_method :size\_in\_words, :word\_count

\# Stuff omitted...

end

 

Aside from letting you easily give a method several different names,
alias\_method comes in handy when you are messing with the innards of an
existing class.

The call to alias\_method copies the implementation of the original
method, giving the fresh copy the new name given as alias. Having done
that we proceed to override the + method but—and here’s the important
part— old\_addition continues to refer to the original unmodified
implementation. When the new + method calls old\_addition we are
actually invoking the original + method which does all of the boring
string addition work

 

When you reopen a class, you can do anything you could have done the
first time. In the same way that we aliased an existing method, we can
make a public method private:

We can even get rid of it all together:

> class Document
>
> remove\_method :word\_count
>
> end

 

the Ruby classes are like variables. You can set them and leave them
alone, or you can fiddle with them as much as you need.

 

Ruby class definitions are executable. That puts statement went off
because when the Ruby interpreter hits a class declaration, it executes
the code between the class and the end

class MostlyEmpty

> puts "hello from inside the class"

end

 

Ruby classes are defined piecemeal one step—or method—at a time. When
Ruby sees that initial class LessEmpty it creates a new and completely
empty class. It then executes the class body the code between the class
statement and the final end. Whatever is inside the class definition— be
it an if or a puts or a method defining def—simply gets executed in
turn. So each block or statement inside class is appended to class and
executed. Same is happening when we re define existing classes its same
as defining the same method twice inside the class

 

Being able to embed code in your classes means that your classes can
make run-time decisions about what methods to define and the code that
those methods will contain.

 

Class example

> if ENCRYPTION\_ENABLED
>
> def encrypt( string )
>
> string.tr( 'a-zA-Z', 'm-za-lM-ZA-L')
>
> end
>
> else
>
> def encrypt( string )
>
> string
>
> end
>
> end

end

 

 

The code that executes inside a class definition has something in common
with a class method: They both execute with self set to the class. This
suggests that we can use class methods to make the same kind of
structural changes that we have done so far with class-level logic

 

Above block can be put like this.

 

class

def self.enable\_encryption( enabled )

> Above block

end

 

enable\_encryption( ENCRYPTION\_ENABLED )

End

 

The last line of the class definition calls enable\_encryption, passing
in true, thereby starting us off with encrypting turned on. A handy side
effect of this latest implementation is that we can toggle encryption
off and on by calling the class method from outside.

 

Executable class definitions are wonderfully useful when you need to
write code that will work in different environments

 

**The difference between load and require is that require keeps track of
which files are already loaded so that it doesn’t load the same file
twice**

**\_\_FILE\_\_ is also supplied via the magic of Ruby and is always set
to the path of the source file of the current class**

 

 

 

 

Gems

Thursday, February 18, 2016

14:23

 

Packaged ruby programs.. Need to install it first..

A really useful feature of the gem system is its complete versioning
support. Every gem is tagged with a version number and, since coders are
forever fixing bugs and adding features, most gems exist in multiple
versions. You can see what versions are available for any given gem with
the gem list command, so that if you run:2

gem list -a --remote ruby-mp3info

Will list versions for the gem…

 

When you install a gem, you will get the latest version unless you ask
for something earlier. Thus, if for some reason you needed the very
first version of rubymp3info,

you can ask for it with the --version option:

gem install --version 0.4 ruby-mp3info

 

Keep in mind that RubyGems is perfectly happy having multiple versions
of the same gem installed on your system. If you do have more than one
version of a gem installed, the default when you ask for the gem in your
code is the latest version.

 

The technology behind RubyGems is pretty simple: The gem developer (the
folks behind ruby-mp3info, for example) package up their work into a
single file, a standardized archive containing not only the code but
also lots of useful metadata, like the gem version number and the other
gems on which this gem depends. Once the code is packed tidily into its
gem file, the developer uploads it to a well-known repository, which is
where gem install will find it. It turns out that the gem file is just a
TAR file.4 Open a gem file with your favorite archive tool—virtually all
of them can handle TAR files—and you will discover that inside each gem
is two more TAR files!

 

Inside the first inner TAR file is where you will finally find the real
contents of the gem including the README file all of the Ruby source
files as well as any executables— the stuff that really makes the gem
go. Inside the second inner TAR file is the metadata—all of that version
authorship and dependency information that makes a gem more than just a
pile of random software.

 

When you install a gem, Ruby will unpack it to a well-known directory,
and from then on Ruby will ensure that the directory containing the code
for that gem is searched when you do a require or a load.

 

Happily, there are only two key things you need to do to create a gem.
The first is to organize your project directories to match the standard
gem layout.

 

![](media/image2.png){width="3.4166666666666665in" height="2.78125in"}

 

 

As you can see from the figure convention calls for a top-level
directory whose name matches the name of the gem in this case document.
Under that you have a README file a directory for unit tests and most
important of all the lib directory that will hold the Ruby code.

It’s no accident that the name of the Ruby file matches the name of the
gem—this is yet another convention. Naming your main Ruby file after gem
is polite, but not absolutely required

 

If your gem is more complicated and carries around multiple source
files, don’t simply drop them in the lib directory. Instead, create a
directory under the lib directory,

whose name matches the name of the gem, and put your code there.

 

![](media/image3.png){width="2.625in" height="1.8645833333333333in"}

 

 

Notice there is still a text.rb file in the lib directory. The
convention is that this top-level Ruby file requires the files buried a
directory down. So, if we peek into text.rb, we see:

 

require 'text/util'

require 'text/double\_metaphone'

require 'text/levenshtein'

require 'text/metaphone'

require 'text/porter\_stemming'

require 'text/soundex'

require 'text/version'

 

The nice effect of doing things this way is that the gem user doesn’t
have to care how complicated your gem is. Whether your gem is simple or
Byzantine, your user simply says require 'text' and they get what they
need

 

The second thing we need for our document gem is the metadata. We need
to tell RubyGems the name of our gem its version and the like. We do
this by creating a gemspec file. A gemspec file is nothing more than a
file full of Ruby code that creates an instance of the
Gem::Specification class.8 Here’s the gemspec for the document gem:

 

Gem::Specification.new do |s|

> s.name = "document"
>
> s.version = "1.0.1"
>
> s.authors = \["Russ Olsen"\]
>
> s.date = %q{2010-01-01}
>
> s.description = 'Document - Simple document class'
>
> s.summary = s.description
>
> s.email = 'russ@russolsen.com'
>
> s.files = \['README', 'lib/document.rb','spec/document\_spec.rb'\]
>
> s.homepage = '<http://www.russolsen.com>'
>
> s.has\_rdoc = true
>
> s.rubyforge\_project = 'simple\_document'

end

 

If your gem depends on having other gems installed in order to work, you
can say that in the gemspec file too. Perhaps the document gem depends
on the text gem. If

so, you would add:

 

s.add\_dependency('text' )

 

You can even depend on a specific version or range of versions:

 

s.add\_dependency('text', '= 0.1.13' )

 

If your gem includes executable scripts—snippets of Ruby code that users
can run from the command line like the rake command from the Rake gem or
spec from RSpec—you can specify that too. Here’s how we might specify
that our document gem has a spell-checking command:

 

s.bindir = "bin" \# Specify the directory

s.executables = \["spellcheck"\] \# Then the file in the dir

 

 

Once you have all of your Ruby files in place under lib, your README
file written, and your gemspec file built, creating the actual gem file
is easy: Just run the gem build

command and call out the gemspec file:

 

gem build document.gem

 

You can install your new gem on your system by simply specifying the gem
file.

 

 

If, however, you are working on an open source project, something that
will be available to the general public, then there is one more step.
You need to put your gem where other people can get at it. In fact, you
will probably want to put it in the place where the gem command will
look by default when someone uses the gem install command

 

Under the covers, the gem command turns to <http://gems.rubyforge.org>
when it goes looking for gems to install. Behind this URL is the open
source project

Gemcutter,9 which is devoted to being the place to get gems. Getting
your gem into the Gemcutter repository could not be easier. You only
need to go to

<http://gemcutter.org> and set up a free account. You will also need to
install the gemcutter gem: gem install gemcutter Now you are ready to
push your gem up to the Gemcutter repository:

gem push document-1.0.0.gem

The push command will ask for your Gemcutter account information and
then upload your gem to the repository. It really is that simple. A few
minutes after running

the push command your gem will be available to anyone who wants to use
it.

 

The trouble with building and uploading your gem by hand is that
someone, probably you, needs to supply the hand. It’s much better to
automate the whole process, and the best way is to build a Rakefile that
takes care of all the details

 

Fortunately there are a number of gems available whose purpose is to
make it easy for you to build your gem. Among the most popular is hoe.11
Hoe tries to automate everything that could possibly be automated when
building a gem.

 

A key danger in using gems is the possibility of name collisions which
unfortunately come in two nasty flavors. The first is the classic “my
class has the same name as your class” problem: If your application
already includes a class called Document you are going to have a problem
trying to use the Document class from the document gem. To lessen the
chance of this sort of thing the wise gem builder will reread Chapter 15
and wrap his or her work in a module: Using modules reduces but doesn’t
completely eliminate the chance of a name collision;

 

The second collision risk is the possibility of filename collisions.
What happens if I’m using the document gem with its document.rb file and
I also happen to have another document.rb file somewhere in my
application? The short answer is nothing good. The longer answer is that
whenever your program tries to load document.rb it will end up loading
the gem version of the file. Fortunately, all is not lost. You can
usually work your way around a filename collision by specifying the full
path for the local file.

 

make sure that you include all the other gems on which your gem depends
in the dependency list. Remember if you happen to have that required but
unlisted gem installed on your system then everything will work fine for
you. It will be a different story when your masterpiece arrives on some
computer that happens to be missing that critical gem. It’s always a
good idea to test your newly minted or modified gem by trying it out on
a clean install of Ruby.

 

The flip side of this is that your gem should avoid claiming that it
uses some gem that it does not. This kind of thing usually happens when
you stop using a gem but

forget to remove it from the list of dependencies

 

Finally you need to keep your gems location independent. One of the best
things about the gem system is that once a gem is installed any
application that wants to use the gem doesn’t have to worry about where
the gem lives—the gem system simply handles that part. So if you install
the widget gem your application can say require 'widget' without having
to know where the widget.rb file is to be found. Your job as the author
of a gem is to avoid screwing up this location independence

 

 

 

 

Ruby Langauge

Thursday, February 18, 2016

15:11

 

To make things even more interesting, there are also three widely used
implementations of Ruby, and not all of them support all versions of the
language:

 

• First, there is the original Ruby implementation written by Yukihiro
Matsumoto,the beloved father of Ruby and widely known as Matz. Rubyists
call this founding

implementation Matz’s Ruby Interpreter, or MRI. MRI is written in C and
supports Ruby 1.8.7.

• Next we have an implementation known as Yet Another Ruby VM, or YARV,
which runs version 1.9.X of the language. YARV is slated to take over as
the Ruby

implementation once the 1.8 to 1.9 transition is complete. Like MRI,
YARV is written in C.

• Finally, there is JRuby, an implementation of Ruby for the Java VM.
JRuby supports

 

 

The first step of that process is to take the program text, break it up
into the individual words and numbers and other assorted bits, and then
reassemble those bits into a tree structure, the abstract syntax tree,
or AST. Once MRI has the AST it executes it, and therefore your program,
using the simplest technique imaginable. Starting at the root of the
abstract syntax tree, MRI works its way down, recursively doing what the
tree tells it to do.

 

If you pull down and unpack YARV,4 you will discover that YARV is the
next generation of MRI. YARV is a real advance over MRI. One big
difference is that MRI supports

Ruby 1.8 while YARV has moved on to version 1.9. So if you look at the
YARV code that creates the Object class, you find that it now has a Ruby
1.9-style BasicObject as a superclass. A more subtle difference between
the two Ruby implementations is that when running Ruby code YARV adds an
extra step between the parse tree and execution. After parsing the Ruby
source YARV turns the resulting tree into a more or less flat list of
byte codes. It is these byte codes that YARV actually executes

 

 

 

Ruby Monk

Wednesday, February 24, 2016

20:14

 

>  

       
  --- -----------------------------------------------------------------------
      ![](media/image4.gif){width="8.333333333333333e-2in" height="0.25in"}

>  
>
> 1\. [In Ruby, just like in real life, our world is filled with objects.
> Everything is an object - integers, characters, text, arrays –
> everything.](https://twitter.com/share?original_referer=http://rubymonk.com/&source=tweetbutton&url=http://rubymonk.com/&via=rubymonk&text=In+Ruby+there+are+no+primitives.+Everything+is+an+object+-+integers,+characters,+arrays+-+everything.)
> As you can see, if you don't specify which object you are, you
> automatically play the role of the mainobject that Ruby provides us by
> default.
>
> One object interacts with another by using what are called methods.
> More specifically, one object "calls or invokes the methods" of
> another object.Invoking a method on an object inevitably generates a
> response. This response is *always* another object. One may also chain
> method invocations by simply adding more periods and method names
> sequentially - each method in the chain is called on the result of the
> previous method
>
>  
>
> 2\. Ruby objects are happy to tell you what methods they provide. [You
> simply call the methods method on
> them.](https://twitter.com/share?original_referer=http://rubymonk.com/&source=tweetbutton&url=http://rubymonk.com/&via=rubymonk&text=In+Ruby,+you+can+list+all+the+methods+of+an+object+by+calling+'.methods'+method+on+it)
>
> Eg: 1.methods.
>
> Sort them also:1.methods.sort
>
>  
>
> 3.Ruby as a language aims to be extremely programmer-friendly, so you
> can usually safely assume that there is a better way.
>
> [Ruby makes an exception in its syntactic rules for commonly used
> operators so you don't have to use periods to invoke them on
> objects.](https://twitter.com/share?original_referer=http://rubymonk.com/&source=tweetbutton&url=http://rubymonk.com/&via=rubymonk&text=In+Ruby+1+++2+is+equal+to+saying+1.+(2).+Providing+consistency+as+well+as+programmer+friendly+API.)
>
>  
>
> 4+(3) is same as 4+3. + is a function just like anyother. Common fns
> have efficient representations.
>
>  
>
> 4\. This last method (\[\]) you've probably already seen in the lesson
> that covers Arrays, and is arguably the most unique in its syntax. Not
> only does it not require a period, it also *encloses* the arguments to
> itself. Even more interesting is that it still works if you use the more
> traditional method syntax
>
>  
>
> words\[1\] = words\[\](1)
>
>  
>
> 5.String construction has what is known as a literal form - the
> interpreter treats anything surrounded with single quotes (') or
> double quotes(") as a string. In other words, both 'RubyMonk' and
> "RubyMonk"will create instances of strings.
>
>  
>
> All Strings are instances of the Ruby String class which provides a
> number of methods to manipulate the string.
>
>  
>
>  
>
>  
>
>  
>
> 6\. It is essential to be able to replace placeholders within a string
> with values they represent. In the programming paradigm, this is called
> "string interpolation". In Ruby, string interpolation is extremely easy.
> Do remember that placeholders aren't just variables. Any valid block of
> Ruby code you place inside \#{}will be evaluated and inserted at that
> location.
>
>  
>
> 7\. We've been using double quotes in all our string interpolation
> examples. **A String literal created with single quotes does *not*
> support interpolation.**
>
> The essential difference between using single or double quotes is that
> [double quotes allow for escape sequences while single quotes do
> not](https://twitter.com/share?original_referer=http://rubymonk.com/&source=tweetbutton&url=http://rubymonk.com/&via=rubymonk&text=In+Ruby,+a+single+quoted+string+supports+only+two+escape+sequences+-+single+quote+and+single+backslash).
> What you saw above is one such example. “\\n” is interpreted as a new
> line and appears as a new line when rendered to the user, whereas
> '\\n' displays the actual escape sequence to the user.
>
>  
>
> 8\. **include?** To check if a string contains the given part
>
>  
>
> **start\_with?** To check if string starts with given part
>
> ** **
>
> Simlarly **ends\_with?**
>
> ** **
>
> **.index** to find index of part in a String
>
> ** **
>
> **upcase** and **downcase** and **swapcase**
>
> ** **
>
> 9\. [It is conventional in Ruby to have '?' at the end of the method if
> that method returns only boolean
> values.](https://twitter.com/share?original_referer=http://rubymonk.com/&source=tweetbutton&url=http://rubymonk.com/&via=rubymonk&text=Ruby+is+awesome,+if+a+method+is+supposed+to+return+true+or+false,+we+can+end+the+method+name+with+'?)Though
> it is not mandated by the syntax, this practice is highly recommended as
> it increases the readability of code.
>
>  
>
> 10\. **split()** to split and **concat()** to join. + can be used for
> concat.
>
> You can use '&lt;&lt;' just like '+', but in this case the String
> object 'Monk' will be appended to the object represented by 'Ruby'
> itself. [In the first case of using '+', the original string is not
> modified, as a third string 'RubyMonk' is created. This can make a
> huge difference in your memory utilization, if you are doing really
> large scale string
> manipulations.](https://twitter.com/share?original_referer=http://rubymonk.com/&source=tweetbutton&url=http://rubymonk.com/&via=rubymonk&text=Want+to+do+large+scale+string+concatenation+in+Ruby?+Use+%3c%3c+rather+than+%2B+to+save+memory!)
>
>  
>
> 11\. **sub (find,replace)** to replace parts.
>
> In order to replace all occurrences we can use a method called
> **gsub** which has a global scope.
>
>  
>
> All string methods accept regex. Eg: gsub(/\[A-Z\]/,'0')
>
>  

       
  --- ---

> 12\. The String\#match method converts a pattern to a Regexp (if it isn‘t
> already one), and then invokes its match method on the target String
> object. Here is how you find the characters from a String which are next
> to a whitespace:
>
>  
>
> 'RubyMonk Is Pretty Brilliant'.match(/ ./)
>
>  
>
> the method just returns the first match rather than all the matches.
> In order to find further matches, we can pass a second argument to the
> match method. When the second parameter is present, it specifies the
> position in the string to begin the search
>
> .match(/ ./, 9) : start from 9^th^ position
>
>  
>
> 13.Ruby uses the == operator for comparing two objects.
>
>  
>
> Ruby lets you negate expressions using the ! operator (read as 'not')
>
>  
>
>  
>
> 14\. if number == 0
>
> number
>
> elsif number &gt; 0
>
> "\#{number} is positive"
>
> else
>
> "\#{number} is negative"
>
> end
>
>  
>
> 15\. Ruby also has an unless keyword that can be used in places where you
> want to check for a negative condition. unless x is equivalent to if !x.
>
>  
>
> 16, In Ruby, ? and : can be used to mean "then" and "else"
> respectively. Known as ternary operators
>
>  
>
>  
>
> 17\. The conditional statements if and unless can also use expressions
> that return an object that is not either true or false
>
> In such cases, the objects **false and nil equates to false**. [Every
> other object like say 1, 0, ""are all evaluated to be
> true.](https://twitter.com/share?original_referer=http://rubymonk.com/&source=tweetbutton&url=http://rubymonk.com/&via=rubymonk&text=In+Ruby+every+other+object+like+say+1,+0,+%22%22+are+all+evaluated+to+be+true.)
>
>  
>
> 18\. Loops are programming constructs that help you repeat an action an
> arbitrary number of times. The methods Array\#each, Array\#select etc.
> are the most frequently used loops since the primary use of loops is to
> iterate over or transform a collection,
>
>  
>
> 19\. loop do
>
> end
>
> create an infinte loop.
>
>  
>
> 20\. \[\] and Array.new creates empty arrays
>
>  
>
> Arrays in Ruby allow you to store any kind of objects in any
> combination with no restrictions on type. Thus, the literal array \[1,
> 'one', 2, 'two'\] mixes Integers and Strings and is perfectly valid
>
>  
>
> [Array indexes can also start from the end of the array, rather than
> the beginning! In Ruby, this is achieved by using negative numbers.
> This is called reverse index
> lookup.](https://twitter.com/share?original_referer=http://rubymonk.com/&source=tweetbutton&url=http://rubymonk.com/&via=rubymonk&text=Looking+up+a+Ruby+array+with+an+index+of+-1,+will+give+you+the+last+element+in+that+array)
> In this case, the values of the index start at -1 and become smaller.
>
>  
>
> In Ruby, the size of an array is not fixed. Also, any object of any
> type can be added to an array, not just numbers
>
>  
>
> &lt;&lt; - that's the 'append' function - to add it to the array. Same
> can be done using push()
>
> Using '&lt;&lt;' is the most common method to add an element to an
> Array
>
>  
>
> 21\. In Ruby, the method map is used to transform the contents of an
> array according to a specified set of rules defined inside the code
> block.
>
>  
>
> \[1, 2, 3, 4, 5\].map { |i| i + 1 }
>
>  
>
> 22\. Filtering elements in a collection according to a boolean expression
> is a very common operation in day-to-day programming. Ruby provides the
> rather handy select method to make this easy.
>
>  
>
> \[1,2,3,4,5,6\].select {|number| number % 2 == 0}
>
>  
>
> 23\. **.delete** to delete elements. delete\_if to delete by condition
>
>  
>
> \[1,2,3,4,5,6,7\].delete\_if{|i| i &lt; 4 }
>
>  
>
> 24\. You'll notice that Ruby methods with multiple words are separated by
> underscores (\_). This convention is called "snake\_casing" because
> a\_longer\_method\_looks\_kind\_of\_like\_a\_snake.
>
>  
>
>  
>
> 25\. The Array\#eachmethod accepts a block to which each element of the
> array is passed in turn. You will find that for loops are hardly ever
> used in Ruby, and Array\#each and its siblings are the de-facto
> standard.
>
>  
>
> 26\. You can retrieve values from a Hash object using \[\] operator. The
> key of the required value should be enclosed within these square
> brackets.
>
> You can use the each method to iterate over all the elements in a
> Hash. However unlike Array\#each, when you iterate over a Hash using
> each, it passes two values to the block: the key and the value of each
> element.
>
>  
>
> 27\. Every Hash object has two methods: keys and values. The keys method
> returns an array of all the keys in the Hash. Similarly values returns
> an array of just the values.
>
>  
>
> 28\. As you can see, where a "normal" hash always returns nil by default,
> specifying a default in the Hashconstructor will always return your
> custom default for any failed lookups on that hash instance.
>
>  
>
> 29\. The other two shortcuts actually use the Hash class's convenience
> method: Hash::\[\]. They're fairly straight-forward. The first takes a
> flat list of parameters, arranged in pairs. The second takes just one
> parameter: an array containing arrays which are themselves key-value
> pairs.
>
> chuck\_norris = Hash\[:punch, 99, :kick, 98,
> :stops\_bullets\_with\_hands, true\]
>
>  
>
>  
>
> a = \[:punch, 0\]
>
> b = \[:kick, 72\]
>
> c = \[:stops\_bullets\_with\_hands, false\]
>
> key\_value\_pairs = \[a,b,c\]
>
> Hash\[key\_value\_pairs\]
>
>  
>
> 30\. we'll ask whether an object is\_a? particular class.
>
> 1.is\_a?(Integer)
>
>  
>
> 31\. An important feature of classes in Ruby is that they too adhere to
> the "everything is an object philosophy."
>
> So, in Ruby, classes themselves are simply objects that belongs to the
> class Class. Here's a simple example that demonstrates this fact:
>
>  
>
> 1.class.class =&gt; Class
>
>  
>
> 32\. In Ruby, like other class-based object oriented languages that you
> may already be familiar with, classes act as the factories that build
> objects. An object built by a certain class is called 'an instance of
> that class.' Typically, calling the new method on a class results in an
> instance being created.
>
>  
>
> 33\. classes in Ruby have names beginning with a capital letter.
>
> For a class to justify its existence, it needs to have two distinct
> features:
>
> **State**
>
> A class must have some kind of state that defines the attributes of
> its instances. In the case of a simple rectangle, this could simply be
> its length and breadth.
>
> **Behaviour**
>
> A class must also do something meaningful. This is achieved by the
> programmer adding methods to the class that interact with its state to
> give us meaningful results.
>
>  
>
> 34\. You'll notice that the variable names length and breadth have an @
> symbol placed in front of them. This is a convention which designates
> them as being a part of the state of the class, or to use jargon, they
> are the "instance variables of the class." This means that every
> instance of the class Rectangle will have its own unique copies of these
> variables
>
> *** ***
>
> Without initialize method creating objects of classes with methods
> using instance varaibles will fail as there is no way to initialize
> them.
>
>  
>
> 35\. So, to summarize, the data an object contains is what it *is* and
> its methods are what it can *do*. Implicit in this definition is the
> fact that the abilities of an object are limited to the methods it
> exposes.
>
>  
>
> 36.Methods aren't exempt from Ruby's "everything is an object" rule.
> This means that the methods exposed by any object are themselves
> objects, and yes, you can use them as such.
>
> All objects in Ruby expose the eponymous method method that can be
> used to get hold of any of its methods as an object.
>
> puts 1.method("next") =-&gt; \#&lt;Method: Fixnum(Integer)\#next&gt;
>
>  
>
> The method object still maintains a relationship with the object to
> which it belongs so you can still call it using the eponymous call
> method and it responds like a normal invocation of that method.
>
>  
>
> next\_method\_object = 1.method("next")
>
> puts next\_method\_object.call
>
>  
>
> 37\. First, note that we use the def keyword to create a method called
> reverse\_sign on the current object. Since Ruby doesn't allow us to use
> spaces in method names, we replace them with underscores instead. It's
> also recommended that, as a convention, method names be in lower case.
>
> The reverse\_sign method accepts one parameter or argument. This is
> simply jargon for the objects a method needs from the caller in order
> for it to do its job. In this case, it's an integer. A method can
> accept any number of parameters (or none).
>
> The return keyword specifies the object to be returned to the caller
> when the method has done its work. If no return keyword is specified,
> the object created by the last line in the method is automatically
> treated as the return value. A method must always return exactly one
> object.
>
> Finally, the method is closed using the end keyword
>
>  
>
> even a method that does nothing at all and has no return produces an
> object - thenil. I
>
> Calling return without specifying an object to return results in a
> nil, which is returned by default.
>
>  
>
> 38.Parameters can have default values too
>
> Older versions of Ruby - 1.8.x and older - required you to set default
> values for parameters starting with the last parameter in list and
> moving backward toward the first. The current version of Ruby (1.9.x)
> no longer has this limitation
>
>  
>
>  
>
> 39\. The list of parameters passed to an object is, in fact, available as
> a list. To do this, we use what is called the *splat operator* - which
> is just an asterisk (\*).
>
> The splat operator is used to handle methods which have a variable
> parameter list
>
> The splat operator works both ways - you can use it to convert arrays
> to parameter lists as easily as we just converted a parameter list to
> an array
>
>  
>
> If you know some of the parameters to your method, you can even mix
> parameter lists and splatting. Again, older versions of Ruby (1.8.x or
> older) required you to place splatted parameters at the end of the
> parameter list, but this is no longer necessary
>
>  
>
> 40\. def add(a\_number, another\_number, options = {})
>
> add(1.0134, -5.568)
>
>  
>
> Ruby makes this possible by allowing the last parameter in the
> parameter list to skip using curly braces if it's a hash, making for a
> much prettier method invocation. That's why we default the options to
> {} - because if it isn't passed, it should be an empty Hash.
>
>  
>
> 41, \*numbers,option={}
>
>  
>
> above two things together is not possible
>
>  
>
> 42.You may have heard of lambdas before. Perhaps you've used them in
> other languages. Despite the fancy name, a lambda is just a
> function... peculiarly... without a name.
>
> Lambdas in Ruby are also objects, just like everything else! The last
> expression of a lambda is its return value, just like regular
> functions.
>
>  
>
> l = lambda { "Do or do not" }
>
> puts l.call
>
>  
>
> Lambdas take parameters by surrounding them with pipes.
>
>  
>
> l = lambda do |string|
>
> end
>
> puts l.call("try")
>
>  
>
> Note that we replaced the {} that wrapped the lambda with do..end.
> Both work equally well, but the convention followed in Ruby is to use
> {} for single line lambdas and do..end for lambdas that are longer
> than a single line.
>
>  
>
> 43.A lambda is a piece of code that you can store in a variable, and
> is an object. The simplest explanation for a block is that it is a
> piece of code that *can't* be stored in a variable and isn't an
> object. It is, as a consequence, significantly faster than a lambda,
> but not as versatile and also one of the rare instances where Ruby's
> "everything is an object" rule is broken.
>
>  
>
> def demonstrate\_block(number)
>
> yield(number)
>
> end
>
> puts demonstrate\_block(1) { |number| number + 1 }
>
>  
>
> 44.It turns out that one of the most common uses for a lambda involves
> passing exactly one block to a method which in turn uses it to get
> some work done. You'll see this all over the place in Ruby -
> Arrayiteration is an excellent example.
>
> Ruby optimizes for this use case by offering the yield keyword that
> can call a single lambda that has been implicitly passed to a method
> without using the parameter list.
>
>  
>
> 45\. Ruby modules allow you to create groups of methods that you can then
> *include* or *mix into* any number of classes. Modules only hold
> behaviour, [unlike
> classes](http://rubymonk.com/learning/books/1/chapters/7-classes/lessons/40-building-your-own-class),
> which hold both behaviour *and* state.
>
>  
>
> Since a module cannot be instantiated, there is no way for its methods
> to be called directly. Instead, it should be included in another
> class, which makes its methods available for use in instances of that
> class.
>
>  
>
> In order to include a module into a class, we use the method include
> which takes one parameter - the name of a Module.
>
>  
>
> 46.Just like all classes are instances of Ruby's Class, all modules in
> Ruby are instances of Module.
>
> Interestingly, Module is the superclass of Class, so this means that
> all classes are *also* modules, and can be used as such.
>
>  
>
> Object
>
> |
>
> Module
>
> |
>
> Class
>
>  
>
> 47\. Namespacing is a way of bundling logically related objects together.
> Modules serve as a convenient tool for this. This allows classes or
> modules with conflicting names to co-exist while avoiding collisions.
>
> Modules can also hold classes
>
>  
>
> :: is a constant lookup operator
>
>  
>
> Module::Class.new -&gt; create object for class inside module
>
>  
>
> 48\. What happens when we don't namespace our class? Because Ruby has
> open classes, doing this simply extends the class globally throughout
> the program, which is dangerous and of course not our intended
> behaviour.
>
>  
>
> The real problem that namespacing solves is when you're loading
> libraries. If your program bundles libraries written by different
> authors, it is often the case that there might be classes or modules
> defined by the same name.
>
>  
>
>  
>
>  
>
> 49.We used the constant lookup (::) operator in the last section to
> scope our class to the module. As the name suggests, you can scope any
> constant using this operator and not just classes
>
>  
>
> One, we can nest constant lookups as deep as we want. Second, we
> aren't restricted to just classes and modules.
>
>  
>
> If you prepend a constant with :: without a parent, the scoping
> happens on the topmost level
>
>  
>
> 50.An input/output stream is a sequence of data bytes that are
> accessed sequentially or randomly.
>
> fd = IO.sysopen("new-fd", "w")
>
> IO.new(fd)
>
>  
>
> fd, the first argument to IO.new, is a file descriptor. This is a
> Fixnum value we assign to an IOobject. We're using a combination of
> the sysopen method with IO.new but we can also create IO objects using
> the BasicSocket and File classes that are subclasses of IO
>
>  
>
> There are a bunch of I/O streams that Ruby initializes when the
> interpreter gets loaded.
>
>  
>
>  
>
> 51.Ruby defines constants STDOUT, STDIN and STDERR that are IO objects
> pointing to your program's input, output and error streams that you
> can use through your terminal, without opening any new files.
>
>  
>
> Whenever you call puts, the output is sent to the IO object that
> STDOUT points to. It is the same forgets, where the input is captured
> by the IO object for STDIN and the warn method which directs toSTDERR.
>
>  
>
> There is more to this though. The Kernel module provides us with
> global variables \$stdout, \$stdinand \$stderr as well, which point to
> the same IO objects that the constants STDOUT, STDIN andSTDERR point
> to
>
> Whenever you call puts, you're actually calling Kernel.puts (methods
> in Kernel are accessible everywhere in Ruby), which in turn calls
> \$stdout.puts.So why all the indirection? The purpose of these global
> variables is temporary redirection: you can assign these global
> variables to another IO object and pick up an IO stream other than the
> one that it is linked to by default. This is sometimes necessary for
> logging errors or capturing keyboard input you normally wouldn't.
>
> 52.Where we used IO.sysopen and IO.new to create a new IO object in
> the last lesson, we'll use theFile class here.You'll notice it's much
> more straight-forward!
>
>  
>
> **mode = "r+"**
>
> **file = File.open("friend-list.txt", mode)**
>
> **puts file.inspect**
>
> **puts file.read**
>
> **file.close**
>
>  
>
> File.open also takes an optional block which will auto-close the file
> you opened once you are done with it.
>
>  
>
> **what\_am\_i = File.open("clean-slate.txt", "w") do |file|**
>
> **file.puts "Call me Ishmael."**
>
> **end**
>
> **p what\_am\_i**
>
> **File.open("clean-slate.txt", "r") {|file| puts file.read }**
>
>  
>
> 53.The File\#read method accepts two optional arguments: length, the
> number of bytes upto which the stream will be read, and buffer, where
> you can provide a String buffer which will be filled with the file
> data. This buffer is sometimes useful for performance when iterating
> over a file, as it re-uses an already initialized string.
>
>  
>
> 54\. When reading from a File object, Ruby keeps track of your position.
> In doing so, you could read a file one line (or page, or arbitrary
> chunk) at a time without recalculating where you left off after the last
> read. So may need to rewind already read file with open file pointer..
>
>  
>
> You can "seek" to a particular byte in the file to tell Ruby where you
> want to start reading from. If you want a particular set of bytes from
> the file, you can then pass the length parameter to File\#read to
> select a number of bytes from your new starting point.
>
>  
>
> 55.readlines returns an array of all the lines of the opened IO
> stream. You can, again, optionally limit the number of lines and/or
> insert a custom separator between each of these lines.
>
>  
>
> lines = File.readlines("monk")
>
>  
>
>  
>
> 56.To **write** to an I/O stream, we can use IO\#write (or, in our
> case, File\#write) and pass in a string. It returns the number of
> bytes that were written
>
>  
>
> File.open("disguise", "w") do |f|
>
> f.write "Bar"
>
> end
>
>  
>
> 57.Array\#countto count the frequency of any element in the given
> array. eg:
>
> \[9,3,4,9,5\].count(9)
>
> Will return the value 2
>
> 58\. values.find\_all { |x| values.count(x) == 1 }
>
> finds sub arry with matchin condition. Count method counts occurance
> of element in array
>
>  
>
> 59\. array.all? { |x| x.is\_a? Fixnum }
>
> to check whole arrray
>
>  
>
> 60.digits.shuffle to shuffle elements of array?
>
>  
>
> 61 inject
>
> \[1, 2, 3, 4\].inject(0) { |result, element| result + element } \#
> =&gt; 10
>
>  
>
> You can think of the first block argument as an accumulator: the
> result of each run of the block is stored in the accumulator and then
> passed to the next execution of the block. In the case of the code
> shown above, you are defaulting the accumulator, result, to 0. Each
> run of the block adds the given number to the current total and then
> stores the result back into the accumulator. The next block call has
> this new value, adds to it, stores it again, and repeats.
>
> At the end of the process, inject returns the accumulator, which in
> this case is the sum of all the values in the array, or 10.
>
> Here's another simple example to create a hash from an array of
> objects, keyed by their string representation:
>
> \[1,"a",Object.new,:hi\].inject({}) do |hash, item|
>
> hash\[item.to\_s\] = item
>
> hash
>
> end
>
> In this case, we are defaulting our accumulator to an empty hash, then
> populating it each time the block executes. Notice we must return the
> hash as the last line of the block, because the result of the block
> will be stored back in the accumulator
>
>  
>
> a=\[1,2,3,4\]
>
> b=a.inject(77) { |accum,num| accum+num\*2}
>
> puts b
>
> \#accum+num\*2 is stored back in accum.. if remove accum,just num\*2
> is stored...
>
>  
>
> \[1, 2, 3, 4\].inject(0) { |result, element| result + element } \#
> =&gt; 10
>
>  
>
> If the example isn't straightforward, don't worry, we're going to
> break it down. The inject method takes an argument and a block. The
> block will be executed once for each element contained in the object
> that inject was called on (\[1,2,3,4\] in our example). The argument
> passed to inject will be yielded as the first argument to the block,
> the first time it's executed. The second argument yielded to the block
> will be the first element of the object that we called inject on.
>
>  
>
> So, the block will be executed 4 times, once for every element of our
> array (\[1,2,3,4\]). The first time the block executes the result
> argument will have a value of 0 (the value we passed as an argument to
> inject) and the element argument will have a value of 1 (the first
> element in our array).
>
>  
>
> You can do anything you want within the block, but the return value of
> the block is very important. The return value of the block will be
> yielded as the result argument the next time the block is executed.
>
>  
>
> In our example we add the result, 0, to the element, 1. Therefore, the
> return value of the block will be 0 + 1, or 1. This will result in 1
> being yielded as the result argument the second time the block is
> executed.
>
>  
>
> The second time the block is executed the result of the previous block
> execution, 1, will be yielded as the result, and the second element of
> the array will be yielded as the element. Again the result, 1, and the
> element, 2 will be added together, resulting in the return value of
> the block being 3.
>
>  
>
> The third time the block is executed the result of the second block
> execution, 3, is yielded as the result argument and the third element
> of the array, 3, will be yielded as the element argument. Again, the
> result and the element will be added, and the return value of the
> block for the third execution will be 6.
>
>  
>
> The fourth time will be the final time the block is executed since
> there are only 4 elements in our array. The result value will be 6,
> the result from the third execution of the block, and the element will
> be 4, the fourth element of the array. The block will execute, adding
> four plus six, and the return value of the block will be 10. On the
> final execution of the block the return value is used as the return
> value of the inject method; therefore, as the example shows, the
> result of executing the code above is 10.
>
>  
>
> That's the very long version of how inject works, but you could
> actually shortcut one of the block executions by not passing an
> argument to inject.
>
> \[1, 2, 3, 4\].inject { |result, element| result + element } \# =&gt;
> 10
>
>  
>
> As the example shows, the argument to inject is actually optional. If
> a default value is not passed in as an argument the first time the
> block executes the first argument (result from our example) will be
> set to the first element of the enumerable (1 from our example) and
> the second argument (element from our example) will be set to the
> second element of the enumerable (2 from our example).
>
>  
>
> In this case the block will only need to be executed 3 times, since
> the first execution will yield both the first and the second element.
> The first time the block executes it will add the result, 1, to the
> element, 2, and return a value of 3. The second time the block
> executes the result will be 3 and the element will also be 3. All
> additional steps will be the same, and the result will be 10 once
> again.
>
>  
>
> Summing numbers with inject is a simple example of taking an array of
> numbers and building a resulting sum one element at a time.
>
>  
>
> Example 2: Building a Hash
>
> Sometimes you'll have data in one format, but you really want it in
> another. For example, you may have an array that contains keys and
> values as pairs, but it's really just an array of arrays. In that
> case, inject is a nice solution for quickly converting your array of
> arrays into a hash.
>
> hash = \[\[:first\_name, 'Shane'\], \[:last\_name,
> 'Harvie'\]\].inject({}) do |result, element|
>
> result\[element.first\] = element.last
>
> result
>
> end
>
> hash \# =&gt; {:first\_name=&gt;"Shane", :last\_name=&gt;"Harvie"}
>
>  
>
>  
>
> As the example shows, I start with an empty hash (the argument to
> inject) and I iterate through each element in the array adding the key
> and value one at a time to the result. Also, since the result of the
> block is the next yielded result, I need to add to the hash, but
> explicitly return the result on the following line.
>
>  
>
> Example 3: Building an Array
>
> Enumerable gives you many methods you need for manipulating arrays.
> For example, if want all the integers of an array, that are even, as
> strings, you can do so chaining various methods from Enumerable.
>
> \[1, 2, 3, 4, 5, 6\].select { |element| element % 2 == 0 }.collect {
> |element| element.to\_s } \# =&gt; \["2", "4", "6"\]
>
>  
>
> Chaining methods of Enumerable is a solution that's very comfortable
> for many developers, but as the chain gets longer I prefer to use
> inject. The inject method allows me to handle everything I need
> without having to chain multiple independent methods.
>
>  
>
> The code below achieves the same thing in one method, and is just as
> readable, to me.
>
> array = \[1, 2, 3, 4, 5, 6\].inject(\[\]) do |result, element|
>
> result &lt;&lt; element.to\_s if element % 2 == 0
>
> result
>
> end
>
> array \# =&gt; \["2", "4", "6"\]
>
>  
>
>  
>
>  
>
>  
>
>  
>
>  
>
>  
>
>  
>
>  
>
>  
>
>  
>
>  
>
> 62.A block is code that you can store in a variable like any other
> object and run on demand. A block is like a method, but one that isn’t
> associated with any object.
>
> the block we just created has an object\_id, belongs to the class Proc
> (which is what a block is called in Ruby), which is itself a subclass
> of Object.
>
> A method is simply a block bound to an object, with access to the
> object's state.
>
> the most common usage involves passing exactly one block to a method.
>
> yield keyword, Ruby's implementation of the most common way of using
> blocks.
>
>  
>
> 63\. using yield is different from the regular approach

-   The block is now no longer a parameter to the method. The block has
    > been implicitly passed to the method - note how it's outside
    > the parentheses.

-   Yield makes executing the block feel like a method invocation within
    > the method invocation rather than a block that's being explicitly
    > called using Proc\#call.

-   You have no handle to the block object anymore - yield "magically"
    > invokes it without any object references being involved.

>  
>
> 64.I call yield "magical" because every object oriented rule in Ruby
> is suspended for this special mode of block invocation.
>
> So yield isn't really a method even though it looks like one (turns
> out, it's a keyword).
>
> Everything in Ruby is an object. Now where's the object that
> represents the block? How is yield getting access to it and seemingly
> invoking the call method on it?
>
> We don't know. As programmers using the language, all we can tell is
> that the normal rules have been suspended.
>
>  
>
>  
>
>  
>
> 65\. Ruby offers the block\_given? method that tells you if a block has
> been passed to a method implicitly. Make the call to yield conditional
> on this method returning true and you'll be fine.
>
>  
>
> 66\. using yield speeds up your code.
>
>  
>
>  
>
> 67\. Below is possible...
>
>  
>
> def prettify\_it
>
> "The result of the block was: \#{yield}"
>
> end
>
>  
>
> 68\. Ruby makes it very easy to convert blocks from implicit to explicit
> and back again, but requires special syntax for this.
>
>  
>
> def calculation(a, b, &block) \# &block is an explicit (named)
> parameter
>
> block.call(a, b)
>
> end
>
>  
>
> puts calculation(5, 5) { |a, b| a + b } \# this is an implicit block
>
> \# -- it is nameless and is not
>
> \# passed as an explicit parameter.
>
>  
>
> Other way
>
>  
>
> def calculation(a, b)
>
> yield(a, b) \# yield calls an implicit (unnamed) block
>
> end
>
>  
>
> addition = lambda {|x, y| x + y}
>
> puts calculation(5, 5, &addition) \# like our last example, &addition
> is
>
> \# an explicit (named) block
>
> \# -- but \`yield\` can still call it!
>
>  

-   The block should be the last parameter passed to a method.

-   Placing an ampersand (&) before the name of the last variable
    > triggers the conversion.

>  
>
>  
>
> 69\. A block can be created by wrapping a chunk of code with curly braces
> ({}) or the words do and end. Unlike the curly braces that you've seen
> thus far, the do - end syntax requires that the do, the code for the
> block, and the end all be on separate lines.
>
>  
>
> In most Ruby codebases, the convention is to use curly braces for
> blocks with just a single line of code, and do-end when more than one
> line is involved.
>
>  
>
> 70\. A block created with lambda behaves like a method when you use
> return and simply exits the block, handing control back to the calling
> method.
>
> A block created with Proc.new behaves like it’s **a part of the
> calling method** when return is used within it, and returns from both
> the block itself as well as the calling method.
>
>  
>
> As a consequence, Proc.new is something that’s hardly ever used to
> explicitly create blocks because of these *surprising* return
> semantics. It is recommended that you avoid using this form unless
> absolutely necessary.
>
>  
>
>  
>
> 71\. all the different ways in which blocks can be created in Ruby that
> we have learned thus far.

-   Implicitly when invoking a method

-   Explicitly using the Kernel\#lambda factory method

-   Explicitly using Proc.new

>  
>
> 72\. The -&gt; literal form is a shorter version of Kernel\#lambda. The
> following two lines produce identical results.
>
> short = -&gt;(a, b) { a + b }
>
> long = lambda { |a, b| a + b }
>
>  
>
> Kernel\#proc factory method is identical to Proc.new. Note that proc
> is a method and not a literal form like -&gt; nor a keyword like
> yield.
>
> The following two lines produce identical results.
>
> short = proc { |a, b| a + b }
>
> long = Proc.new { |a, b| a + b
>
>  
>
> 73.Object\#is\_a? accepts a single parameter - a class. Object\#is\_a?
> has an alias, Object\#kind\_of?. They're identical in every respect so
> you're free to pick whichever reads better in a given context.
>
>  
>
> 74\. This kind of parent-child relationship between classes is often
> referred to as *inheritance*, where the specialized class *inherits* the
> abilities of its more generic parent.
>
>  
>
> 75..class.superclass
>
> to get superclass of a class-based
>
> The Class\#superclass method tells you which class any given class was
> inherited from. Note that it's an instance method on Class and not on
> Object.
>
>  
>
> Object.superclass \# BasicObject
>
>  
>
> Each class in that chain *inherits* the behaviour of the class that
> comes next. All such chains in Ruby end with BasicObject which is a
> completely blank, empty class with no superclass. Calling
> BasicObject's superclass method returns nil.
>
>  
>
> 76\. the &lt; operator informs Ruby that when creating the class, it
> should set another class as its superclass.
>
>  
>
> 77\. *Redefining* a method involves simply replacing one method with
> another. The original method is simply... lost.
>
>  
>
> *78.*Overriding in the context of classes involves defining a method
> in a subclass that is already defined in the superclass. This results
> in the method being *overridden* in the subclass, but doesn't in any
> way affect the method in the superclass.
>
>  
>
> 79\. Most object oriented languages offer a mechanism by which an
> overridden method can be called by the overriding method. Ruby uses the
> super keyword to make this happen. Using super will call the same
> method, but as defined in the superclass and give you the result.
>
>  
>
> 80.Item.new creates a new object - an instance of the classItem. The
> instance variables, in the example above, @item\_name and @quantity,
> are prefixed by the@ symbol. This is enforced by Ruby - if your
> variable does not start with a @, it is considered to be a local
> variable.
>
> the instance variable is bound to the specific instance of the class.
> By binding itself to the entire object, an instance variable makes
> itself available to every method of the object.
>
>  
>
> 81.An object can't exist in isolation. It has to communicate its state
> to other objects at some point. However, only the object's own methods
> can access its instance variables. So, you can have methods known as
> 'getter' methods whose sole purpose is to return the value of a
> particular instance variable
>
> Having to explicitly define getter methods ensures that the object is
> always in control of how your state is exposed to the public.
>
>  
>
> To execute the statement item.color = 'red', Ruby invokes the the
> method Item\#color= and passes the value 'red' to it. This means that
> all setter methods end with the = sign in their names. For instance,
> the method color=.
>
>  
>
> 82.Ruby provides a couple of methods to make life easy when declaring
> getters and setters for your object.
>
> The attr\_reader method defines the reader method for you.
>
> There is a similar method attr\_writer which, as you may expect,
> defines a setter method
>
> attr\_reader :item\_name
>
> No space between : and variable name in attr\_writer
>
>  
>
> Instead of having to call attr\_reader and attr\_writer for the same
> variable, you can use another method, theattr\_accessor, which will
> define both the getter and setter.
>
>  
>
> 83.In def self.show, the keyword self denotes that the method show is
> being defined in the context of the Class itself, not its instances.
> Any method definition without the self qualifier is by default an
> instance method.
>
> class &lt;&lt; self
>
> def show
>
> puts "Class method show invoked"
>
> end
>
> end
>
>  
>
> Class methods do not have access to instance methods or instance
> variables. However instance methods can access both class methods and
> class variables.
>
>  
>
> class variables are prefixed with @@.
>
>  
>
>  
>
>  
>
> 84\. Class variables are inherited .changes made by subclasses will
> reflect in main class.
>
>  
>
> 85\. to stop this..
>
> **class instance variables**.
>
> They are declared and initialzed in class , not in initialize method.
> Also they are accessed only inside class methods..
>
>  
>
> These variables are not inherited.So they have to be decalred and
> initialized in all sub classes. But the class methods using them are
> inherited and are not required to be redeclared.
>
>  
>
> 86.In Ruby, all binary operators (those which have two operands)
> including == are actually methods that gets invoked on the parameter
> on the left-hand side of the operator. In practice that means a == b
> is the same as a.==(b).
>
>  
>
>  
>
> 87\. The short answer is that we failed to implement two other methods
> that are crucial to get object equality correct: the eql? and hash
> methods.
>
> There are a lot of operations in Ruby that need to check the equality
> of two objects. While == serves the purpose well, it is not really
> fast. For operations that might involve large number of equality
> checks (likeArray\#uniq and Hash lookups), the speed disadvantage adds
> up and becomes an overhead. To get around this, Ruby provides a hash
> method with every object. It returns a numeric value which is usually
> unique to every object.
>
> A hash code of an object is usually a short (and in Ruby, always
> numeric) identifier of an object.
>
> So instead of comparing two objects using ==, which could be expensive
> when the objects are large, Ruby uses the hash of the object when
> possible. Being a simple numeric value, this comparison is almost
> always faster than comparing the various instance variables of the
> underlying object.
>
> Even though we use == to check for equality of objects, routines like
> Array\#uniq uses the eql? instead. This means that we must implement
> theeql? method as well whenever we override ==. In most cases, these
> two methods will be identical, so you can implement the actual
> comparison in one method and have the other method just call it.
>
> To summarize, if you ever override any of the ==, eql? or the hash
> method, you must override the others as well.
>
>  
>
>  
>
>  
>
> 88.puts generally prints the result of applying to\_s on an object
> while p prints the result of inspecting the object.
>
> As you can see, puts prints the class name of the object along with a
> number displayed as hex. The number is relative to the position of the
> object in memory, but we seldom find any use for it.
>
> p on the other hand prints the class name and all the instance
> variables of the object. This can be very useful while debugging.
>
>  
>
>  This is because if you override to\_s for an object, Ruby will treat
> it as the result of inspect as well, unless you
> override inspect separately. So p and puts becomes the same. Also, it
> is generally a best practice to override the to\_s method in your
> classes so that it can return meaningful result that is tailored for
> each class.
>
>  
>
> 89\. This basic concept (transferring data between programs) is
> essentially what we're referring to when we say "serializing". By
> turning our Ruby objects into strings we have made them *serial*: the
> objects are all lumped together as a string of chracters, one character
> after another
>
> We want some way of automatically transforming any Ruby object into a
> serialized form. There are a number of serialization formats we could
> use. You may have heard of XML, json, or YAML. Ruby can produce any of
> these formats (they're all strings, by the way) but we'll specifically
> take a look at YAML since it's built right into the Ruby language. 
>
>  
>
> def self.deserialize(yaml\_string)
>
> YAML::load(yaml\_string)
>
> end
>
> def serialize
>
> YAML::dump(self)
>
> end
>
>  
>
>  
>
> 90\. zen, life = \[42, 43\]
>
> This is **destructuring**. We've broken down the array and assigned
> its values to zen and life.
>
> This is equivalent to using the bracket form or the at method to
> extract values. giving you nice a shorthand for doing a sequential
> breakdown of an array.
>
> For multi dimesion arrays, destructuring results in sub arrays..
>
>  
>
>  
>
> a,b=\[1, 2, 3, 4\] =&gt; a=1 and b=2
>
> zen, life, more = \[42, 43\] =&gt; more is nil here.
>
>  
>
> 91\. Ruby has a more dedicated way of destructuring using the **splat
> (\*)** operator.
>
> car, \*cdr = \[42, 43, 44\]
>
> cdr becomes 43,44
>
>  
>
> we're splitting the array up by the number of
> variables **and** slurping the rest of the array into the second
> variable with the **splat (\*)**.
>
> \*initial, last = \[42, 43, 44\]
>
> initial=42,43
>
> last=44
>
>  
>
> initial here only slurps the elements before 44. This is because we
> have two variables **and** lasttakes away the final value.
>
> \*initial, second\_last, last = \[42, 43, 44\]
>
> initial=42 only.
>
>  
>
> 92\. The splat isn't restricted to just the **left** hand side. You can
> also use it with Range, String and convert them into Array objects.
>
> Zen = \*(1..42) =&gt; array from 1 to 42
>
> It's also possible to use this left hand side form to turn array items
> into method arguments.
>
> def zen(a, b)
>
> a + b
>
> end
>
> puts zen(\*\[41, 1\])
>
> You can of course, use this with blocks as well.
>
> \[\[1, 2, 3, 4\], \[42, 43\]\].each { |a, \*b| puts "\#{a} \#{b}" }
>
>  
>
>  
>
>  
>
>  
>
>  
>
> 93.Hash is often created using the array form that takes
> in **even** number of arguments as key-value pairs, or directly, a
> two-dimensional array with paired arrays.
>
> Hash\[4, 8\] =&gt; {4=&gt;8}
>
> Hash\[ \[\[4, 8\], \[15, 16\]\] \] =&gt; {4=&gt;8, 15=&gt;16}
>
> You can use the splat in this form to create hashes.
>
>  
>
> ary = \[\[4, 8\], \[15, 16\], \[23, 42\]\]
>
> puts Hash\[\*ary.flatten\]
>
> {4=&gt;8, 15=&gt;16, 23=&gt;42}
>
>  
>
>  
>
> 94\. count used without any arguments acts like
> the size or length methods, which return the number of elements present
> in the array.
>
>  
>
> count also takes in a single object argument and returns the count of
> the array for which elements equal to that object.
>
> puts \[42, 8, 15, 16, 23, 42\].count(42) =&gt;2
>
>  
>
> count also takes in a block and returns the number of elements in the
> array for which the block results to true.
>
>  
>
> \[4, 8, 15, 16, 23, 42\].count { |e| e%2==0 }
>
>  
>
>  
>
> 95.The index method returns the index of the object specified. If a
> block is given it returns the index of the**first** element for which
> the block results to true.
>
> puts \[4, 8, 15, 16, 23, 42\].index { |e| e % 2 == 0 } =&gt; 0
>
>  
>
> 96\. The flatten method returns a one-dimensional array representation of
> the array. It recursively picks out all elements from the inner-arrays
> and lays them out in the outermost array.
>
> p \[4, \[8\], \[15\], \[16, \[23, 42\]\]\].flatten =&gt; \[4, 8, 15,
> 16, 23, 42\]
>
>  
>
>  
>
> You can also restrict the number of levels flatten will jump in to.
>
> \[4, \[8\], \[15\], \[16, \[23, 42\]\]\].flatten(1) =&gt; \[4, 8, 15,
> 16, \[23, 42\]\]
>
>  
>
>  
>
> 97\. The compact method returns a new array with all the nil elements
> removed.
>
>  
>
> 98\. cant chain methods ending with ! =&gt; check this..
>
>  
>
> 99\. The zip method expects variable number of arguments and returns an
> array of arrays that contain corresponding elements from each array.
> That is, an element-wise merge with the original array
>
> p \[4, 8, 15, 16, 23, 42\].zip(\[42, 23, 16, 15, 8\])
>
> =&gt;
>
> \[\[4, 42\], \[8, 23\], \[15, 16\], \[16, 15\], \[23, 8\], \[42,
> nil\]\]
>
>  
>
> If the elements of the array arguments passed to zip aren't equal to
> the array it's being called on, then it assigns nil to the faulty
> combination in the sequence.
>
>  
>
> 100\. slice is same as using the literal \[\] form for extracting
> subarrays.
>
> It accepts an index, like array\[2\] or a Range, like array\[2..7\]
>
> p \[4, 8, 15, 16, 23, 42\].slice(2..5) =&gt; \[15, 16, 23, 42\]
>
>  
>
> 101.join is useful for joining all the array elements into a string.
> You can add a separator between by specifying it as a String argument.
>
> If you notice, join only applies the separator between two elements,
> hence sparing the last element. This makes join really convenient for
> sanitizing information to be displayed.
>
>  
>
> 102\. shift removes the first element of the array and returns it. Shifts
> the rest of the array towards left, such that the second element becomes
> the first element, the third element becomes the second one and so on.
>
> You can also specify an optional argument -- shift(n) that will remove
> and return an array of the firstn elements.
>
> p \[4, 8, 15, 16, 23, 42\].shift(2) =&gt; \[4, 8\]
>
>  
>
>  
>
>  
>
> 103\. unshift takes a variable number of arguments and adds them to the
> beginning of the array.
>
> p \[16, 23, 42\].unshift(4, 8, 15) =&gt; \[4, 8, 15, 16, 23, 42\]
>
>  
>
>  
>
> 104\. pack returns a packed string of the array elements converted into
> appropriate binary sequences. There are quite a few directives you can
> specify for this
>
>  
>
> 105\. Stack is a last-in-first-out data structure that can be easily
> implemented using Array. We can simply restrict our interface that wraps
> an Array to just two operations -- push and pop and some other useful
> methods to emulate stack like functionality.
>
>  
>
>  
>
> 106\.  Ruby already has one built in: Array\#product
>
> to create comninations of array elements.
>
>  
>
> 106\. reject method in array is opposite to select
>
>  
>
> 107\.  Array\#transpose. Transposing a matrix is just rotating it on an
> axis. 
>
>  
>
> 108.Matrix class for matrix operations..
>
>  
>
> 109\. included method. It is a callback that Ruby invokes whenever the
> module is included into another module/class
>
> module Foo
>
> def self.included(klass)
>
> puts "Foo has been included in class \#{klass}"
>
> end
>
> end
>
> class Bar
>
> include Foo
>
> end
>
>  
>
>  
>
>  
>
>  
>
> includemakes it possible to share behaviour through modules by mixing
> in the methods from a module into a class.
>
> However, include has a limitation: it can only add instance level
> methods - not class level methods. 
>
>  
>
> we receive a NoMethodError when trying to invoke the module level
> method from the class. While using include.
>
>  
>
> 110\. The extend method works similar to include, but unlike include, you
> can use it to extend any object by including methods and constants from
> a module.
>
> The important thing to note here is that extend works everywhere:
> inside a class/module definition and on specific
> instances. include however cannot be used on specific objects.
>
> bar=Bar.new
>
> bar.extend Foo
>
> In a sense, extend can be used to mimic the functionality of
> the include method. 
>
>  
>
> when you add an include statement inside a class defintion, Ruby
> ensures that all new instances of the class will have the methods
> defined in the included module.
>
> So, to mimick include, you'll have to reproduce what Ruby does for you
> when using include. That means you'll have to add all the methods
> present in the mixin module to every new instance of the class. The
> next exercise is to do just that!
>
>  
>
> include is the standard Ruby idiom for mixing in methods from a module
> to a class and you should stick to it.
>
>  
>
> 111.But that is not all! extend is a badass; it can add class level
> methods - something that include can't do.
>
> he magic is in treating everything as an object - as you may extend an
> instance of a class, you may extend the class itself!
>
> Bar.extend Foo
>
>  
>
> 112.
>
> The include method has a callback which is invoked whenever a module
> is included into another module/class - the included method. It is
> executed in the context of the mixin module and should be defined
> there. Its signature is self.included(base) where base is the target
> class.

-   While extend can be used to add instance methods to instances, we
    > don't use that much. However, unlike include, extend can be used
    > to add methods to the classes themselves.

>  
>
>  
>
> You have to modify the moduleFoo in the following exercise so that
> when you include it the class Bar, it also adds all the methods
> from ClassMethods into Bar as class methods.
>
> module Foo
>
> module ClassMethods
>
> def guitar
>
> "gently weeps"
>
> end
>
> end
>
> def self.included(base)
>
> base.extend ClassMethods
>
> end
>
> end
>
>  
>
> class Bar
>
> include Foo
>
> end
>
>  
>
> puts Bar.guitar
>
>  
>
> 113\. Just like included which is a callback for include, there is a
> callback for extend and it is appropriately called extended.
>
> def self.extended(base)
>
> end
>
>  
>
> 114.It is also possible (but not advisable) to write non-object
> oriented code in Ruby by avoiding creation of objects and instead
> relying on independent methods. Ruby's Math module is an example of a
> collection of such methods. 
>
>  
>
> module Weather
>
> def self.will\_it\_rain\_on(date)
>
> "it depends"
>
> end
>
> end
>
>  
>
> puts Weather.will\_it\_rain\_on(Date.today)
>
>  
>
>  
>
> 115.When an exception occurs (Ruby calls this event "raising an
> exception"), it will stop processing further statements in the code
> and will try to escape any methods called so far. 
>
> Raising an exception halts program execution. It might add clarity to
> that image to know that the raised exception makes its way through all
> the methods called (known as the "call stack") to get to the point of
> failure.
>
> A raised exception will propagate through each method in the call
> stack until it is stopped or reaches the point where the program
> started
>
>  
>
> 116\. To stop an exception, we need a way of wrapping our method calls
> such that they are protected when an exception pops out of them. Behold!
> The begin - rescue - end block!
>
> Also raise Exception.new("overheated!") to raise error
>
>  
>
> Exceptions are just Ruby objects.
>
>  
>
> begin
>
> rescue Exception =&gt; e
>
> puts "Let me tell you about heat! \#{e.inspect}"
>
> end
>
>  
>
> f you define a begin-rescue-end block inside a method it actually
> doesn't require the begin and end keywords; as long as you want to
> capture exceptions across the entire method, they're implicit.
>
> rescue has a one-liner form which allows you to rescue the exception
> at the end of the line (similar to the if one-liner). This form,
> however, simply returns whatever is placed to the right of
> the rescue keyword
>
>  
>
> 117.The last aspect of rescuing exceptions is forcing execution of
> some cleanup code you need to run whether there was an error or not.
> This sort of thing often involves closing a connection to a database
> or freeing up some other non-Ruby resource. Doing so is quite easy: we
> use the ensure keyword, at the same indentation level as rescue, to
> define code that should run both in success and failure scenarios.
>
>  
>
> 118.To raise exceptions we
> use raise or Kernel.raise or Kernel.fail. raise without any arguments
> simply raises a RuntimeError exception with the string message that
> we've specified.
>
> raise "Rise."
>
> you would typically use raise when you want to raise these exceptions
> before Ruby does, or raise custom exceptions that are not handled by
> Ruby.These would commonly be StandardError exceptions
>
>  
>
> The most common way to raise an error is to just specify the type of
> the exception with an optional string parameter that acts as its
> message when it is displayed.
>
> raise StandardError, "Raising standard error"
>
>  
>
> 119\. we call the backtrace method on the error variable, which is an
> instance of theSyntaxError class.
>
>  
>
> 120\. ruby can have methods outside class.Just call the method name to
> execute
>
> When you define a function in Ruby at the global scope in this way, it
> technically becomes a private method of the Object class, which is the
> base class that everything inherits from in Ruby. 
>
> Because it is defined as a method with private visibility on Object,
> it can only be called inside objects of the class on which it's
> defined or subclasses.
>
> Basically, the Ruby program itself defines an instance
> of Object called main, which serves as the top-level scope where your
> method was defined. So if you think of your program as
> running*inside* main (which is an Object) its private methods are
> available for use.
>
> The technical reason it happens is because main is special and treated
> differently than any other object. There's no fancy explanation
> available: it behaves that way because it was designed that way.
>
> Okay, but why? What's the reasoning for main to be magical? Because
> Ruby's designer Yukihiro Matsumoto thinks it [makes the language
> better](http://groups.google.com/group/comp.lang.ruby/browse_thread/thread/7bb7b451a8f3cca7/98c4c62127b9d945) to
> have this behavior:
>
>  
>
> 121.What happens when you don't handle the exception anywhere?
>
>  At this point, the exception is not explicitly rescued anywhere,
> hence it is just printed onto the STDERR and the program exits.
>
>  
>
> 122.All the error objects that we've been using come from
> the Exception class. These objects are typically created by raise or
> by simply calling new on the exception object.
>
> The Exception is the master class that subclasses a bunch of more
> granular exceptions.
>
> The larger part of the commonly recoverable exceptions are sub-classed
> by the StandardError class. The others are more low, virtual-machine
> level errors that are less important in a regular course of the
> program and are generally not captured.
>
> This is the StandardError class hierarchy:
>
> ArgumentError
>
> IOError
>
> EOFError
>
> IndexError
>
> LocalJumpError
>
> NameError
>
> NoMethodError
>
> RangeError
>
> FloatDomainError
>
> RegexpError
>
> RuntimeError
>
> SecurityError
>
> SystemCallError
>
> SystemStackError
>
> ThreadError
>
> TypeError
>
> ZeroDivisionError
>
> For more granularity in your exceptions, you can rescue each of these
> individually. RescuingStandardError takes care of all the sub-classed
> exceptions as well
>
>  
>
> Therefore, to create a custom Exception, you can subclass
> the Exception class. More specifically, the StandardError class.
>
>  
>
> class SomeCustomError &lt; StandardError
>
> end
>
>  
>
> backtrace method on the Exception class returns an array of the
> current state of the call stack. Starting from the first element, it
> gives you strings of errors where the exception originated from, till
> it reaches the end of the call stack.
>
> message returns a string that is specified when you create or raise
> the exception object. It returns the name of the exception if no
> message is specified.
>
>  
>
> 123.Ruby has a \`%Q\` syntax which allows you to use any character as
> the string-quote character. For example, %Q\[quotes are "neat".\] is
> valid Ruby. Within the \`%Q\` syntax, you do not need to escape
> quotes, double-quotes, or newlines!
>
>  
>
> 124.Ruby has a \`%w\` and \`%W\` (interpolated) syntax, which works
> just like \`%Q\` except it produces an array of words instead of a
> string.
>
>  
>
> 125\. 'a'..'z'
>
> range of characters.
>
>  
>
> 126\. defined? To check defined...
>
>  
>
> Every time the Ruby interpreter encounters def, it enters a new scope.
> This means simultaneously that it is capturing the code its about to
> read into a name (in this case, \`scope\_the\_scope\`) but also that
> it is creating a new *context* in which that code will be read. That
> context is the local scope, and it cuts both ways: variables defined
> inside the method cannot be changed or read outside the method --
> variables defined outside the method cannot be changed or read inside
> the method.
>
>  
>
> Notice our use of Ruby's keyword defined?. This is a special keyword
> in Ruby (like if), not a method, because we would otherwise
> see NameError for undefined variables
>
>  
>
>  defined? doesn't just report whether the variable is defined but also
> how it is scoped.
>
>  
>
> puts "inside the class: \#{defined?(@toes).inspect}"=&gt; returns
> false as @toes is instance and class level its not defined
>
>  
>
> 127.a global has its own beauty in its simplicity: you can set it
> anywhere, you can get it anywhere. There is only one global with that
> name, no matter where you go. However, this is also the global's
> undoing. Because everyone can see a global, everyone can change it.
> You have no special control.
>
> Using \$operator
>
>  
>
> Ruby does have some predefined globals which you may make use of from
> time to time. These include\$\* (the command-line arguments used to
> execute this Ruby program), \$@ (the location of the last
> error), \$\~ (the last regular expression match), and \$0 (the name of
> the current ruby script). To name a few. 
>
>  
>
> 128.In the same way instance variables come into existence when you
> name a variable with an "@" prefix, constants come into existence when
> you name a *\*cough\**variable *\*cough\** with an upper-case
> character prefix
>
>  
>
> Ruby is forgiving about assigning a constant value twice statically.
> Because classes and modules are constants, this is helpful if one
> accidentally requires the same file into a program twice.
>
>  
>
> If you try to redeclare a constant dynamically, however, Ruby will get
> upset:(like in a function) Ruby does not want you to assign (or
> re-assign) constants while your program is running -- and that's a
> good thing.
>
>  
>
>  
>
> 129.Ruby requires you use a constant when naming classes and modules
>
> There is a way around this, however, and in its use we can see that
> classes and modules themselves are types in the Ruby class hierarchy,
> just like strings and arrays.
>
>  
>
> fence = Module.new do
>
> sheep = Class.new do
>
>  
>
> But \`::\` can only look up constants. So above may not work
> everytime..
>
>  
>
> 130. calling each on the Array \[4, 8\] in this next example, returns
> an Enumerator object.
>
>  
>
> Enumerable is a module used as a mixin in the Array class. It provides
> a number of enumerators likemap, select, inject. The Enumerable module
> itself doesn't define the each method. It's the responsibility of the
> class that is including this module to do so.
>
>  
>
> This Array class, consequently, defines the each method. It returns an
> object of the type Enumeratorwhen no block is given (like our first
> example). It yields a value of the type self when there is one
>
>  
>
> Enumerator is an objectification of enumeration. The point of these
> methods returning these enumerators is to allow us to chain operations
> indefinitely and make more heavy-duty collections.
>
>  
>
> 131.we'll start off with an each variant calledeach\_with\_index. With
> this you can define blocks with two arguments, the element (just
> like each) and its index.
>
>  
>
> \[4, 8, 15, 16, 23, 42\].each\_with\_index { |e, i| puts "\#{e} --
> \#{i}" }
>
>  
>
> 132.Any class that mixes in Enumerable has access to all its
> methods. Hash in Ruby, just like Array, also includes Enumerable
>
>  
>
> The first argument in the each\_with\_index block for hashes would
> contain the key-value pair as an array, the second being the pair's
> position in the hash. Hashes in Ruby are funny that way - iterating
> over a Hash almost always gives you the key and value in an Array.
>
>  
>
> {:locke =&gt; "4", :hugo =&gt; "8"}.each\_with\_index do |kv, i|
>
> puts "\#{kv} -- \#{i}"
>
> end
>
>  
>
> 133.map is another Enumerable method that is similar to each. It goes
> through each element in yourArray or Hash and evaluates the block for
> that element and appends the value in an array that it returns.
>
>  
>
> In other words, each is used for simple
> iteration, map for *transformation*.
>
> map returns the **resultant** array. each returns
> the **original** array.
>
>  
>
> The purpose of map is to return this resultant array created when the
> operations are applied to the original data structure -- which
> obviously makes its return value useful. each is more of a generic
> iterator that is often used to puts things out. Because of the simple
> nature of each, it is also used as a custom iterator builder.
>
>  
>
> 134.Array.first gives first in the array.all
>
>  
>
>  
>
> 135.all?, any? and none? are some useful querying enumerators that
> always return true or false.
>
> These enumerators are principally similar. They
> return true if **any**, **all** or **none** of the items match the
> condition in the block. false, otherwise.
>
>  
>
> \[4, 8, 15, 16, 23, "42"\].any? { |e| e.class == String }
>
>  
>
> With a Hash, you can use these in two ways. Either with one argument
> that is a 2 element array of the key-value pair. candidate\[0\] is the
> key and candidate\[1\] is its value.
>
>  
>
> {:locke =&gt; 4, :hugo =&gt; 8}.any? { |candidate| candidate\[1\] &gt;
> 4 }
>
>  
>
> You can also use these with two arguments.
>
> {:locke =&gt; 4, :hugo =&gt; 8}.any? { |candidate, number| number &lt;
> 4 }
>
>  
>
>  
>
> 136.Ruby lets you treat Arrays in a manner similar to Sets by
> providing the Union, Intersection and Difference operations between
> two arrays.
>
>  
>
> The | (pipe character) is the Union operator. It joins two arrays and
> returns the result with duplicates removed.
>
>  
>
>  
>
>  
>
>  
>
> The & operator is the Intersection operator. It is an easy way to find
> elements that are common to two (or more) arrays. Similar to Array
> union, all the elements in the result of an intersection will be
> unique.*"Returns a new array that is a copy of the original array,
> removing any items that also appear in other\_ary*
>
> The - method preserves even the duplicate elements in the original
> array, however all occurence of each element in second array are
> removed from the result - including the duplicates.
>
>  
>
> Set is a standard Ruby class that provides the semantics of the
> mathematical notion of Set. Apart from the standard union,
> intersection and difference operations, it lets you group elements of
> a set according to arbitrary conditions through the classify method.
> You can also divide a set into subsets using thedivide method
>
>  
>
>  
>
> 137.In Ruby, the standard operation all collections perform is the
> retrieval of elements from the collection sequentially using
> the each method. 
>
> each accepts a block of code as an argument. It iterates through all
> elements of the collection and for every element, executes the code.
>
>  
>
> 138.example select
>
> class FibonacciNumbers
>
> NUMBERS = \[1, 1, 2, 3, 5, 8, 13, 21, 34, 55\]
>
>  
>
> def select(&filtering\_condition\_block)
>
> filtered\_result = \[\]
>
> NUMBERS.each do |number|
>
> filtered\_result &lt;&lt; number if
> filtering\_condition\_block.call(number)
>
> end
>
> filtered\_result
>
> end
>
>  
>
> end
>
>  
>
> \# print only the even Fibonacci numbers
>
> nums = FibonacciNumbers.new
>
> nums.select {|num| num % 2 == 0}.each {|num| puts num}
>
>  
>
> 139.If your collection object implements the each method, Enumerable -
> a standard Ruby module can implement the rest of the collection
> methods for you. Just add the line include Enumerable to your class
> and that will provide your class with all the standard collection
> methods.
>
>  
>
> Do you remember what the include statement does? It makes all the
> instance methods of the module available as instance methods for your
> class as well
>
>  
>
> 140.Enumerables are collections of objects. Implict in that definition
> are two concepts: object references and collection ordering.
>
>  
>
> Ruby, like most other object oriented languages, deals with references
> to objects rather than the objects themselves directly. 
>
>  
>
> a = "tom"
>
> b = "jerry"
>
> superheroes = \[a,b\]
>
> a = "batman"
>
>  
>
> puts superheroes =&gt; \[tom,jerry\]
>
>  
>
> 141.a = "tom"
>
> b = "jerry"
>
> superheroes = \[a,b\]
>
> puts superheroes
>
> \# reassign a to a different superhero
>
> a = "batman"
>
> puts superheroes
>
> \# jerry is in fact superman. who knew!
>
> b.gsub!("jerry", "superman")
>
> puts superheroes
>
>  
>
> This is why bang methods are dangerous - they mutate the objects
> in-place. Your Enumerable is only a collection of 'references' to
> objects. This is good - even if you change what a variable refers to,
> later in the code, the Enumerable will not change. After all, the
> Enumerable does not know anything about the variable. It stores only
> the objects referenced by those variables. But when you use a
> dangerous method, you are changing the value of every Enumerable that
> contains the object. 
>
>  
>
> 142.Typically p is handy because it prints the output of inspecting
> the object which is more detailed than what putsprovides. 
>
>  
>
> 143.Integers in Ruby are of class Fixnum, and numbers with decimals
> (which we call 'floating point numbers') are Float. And of
> course, **if you divide two numbers and expect the correct result with
> decimals, then at least one number in the operation must be aFloat.**
>
>  
>
> **144.**This stack trace is useful when you are inside a method within
> a deep context and want to inspect it. This is provided by
> the caller method which if needed can be used to debug our code as
> well. 
>
> The caller method returns the stack trace as an array which is pretty
> convenient if you want to programmatically introspect it.
>
>  
>
> 145.There will be occasions when you need to continuously keep track
> of what your application is doing so that when something goes wrong,
> you have a detailed trace. This is called 'Logging
>
> Ruby ships with theLogger class that you can use for logging.
>
>  
>
> require 'logger'
>
> logger = Logger.new(\$stdout)
>
> logger.warn("This is a warning")
>
> logger.info("This is an info")
>
>  
>
> Before you can use the Logger class, you have to require it explicitly
> by using the 
>
> require 'logger' statement. When initializing, you have to tell it
> where to log it - this can be the name of a file, a File object or any
> IO object to which it can write
>
>  
>
> The Logger class exposes multiple methods - all of which logs the
> message, but in the following order of severity: *debug &lt; info &lt;
> warn &lt; error &lt; fatal &lt; unknown*. So, if the logging level is
> set to say WARN, then only levels that have same or higher severity
> than WARN are printed - which includes WARN, ERROR, FATAL and UNKNOWN.
> The highest state of logging is DEBUG, which will print everything.
>
> You can set the severity level of logging by assigning the level like
> so: 
>
> logger.level = Logger::INFO
>
>  
>
> require 'logger'
>
> logger = Logger.new(STDOUT)
>
> logger.level = Logger::UNKNOWN
>
>  
>
> 146.logger.formatter = lambda do |severity, datetime, progname, msg|
>
> "\#{datetime}: \#{msg}\\n"
>
>  
>
> The formatter attribute takes in a lambda to which the parameters
> given in the example are passed in order. The lambda can make use of
> the parameters and format the log output the way you need it.
>
>  
>
> 147.You can replace STDOUT with aFile object so that all logs go into
> a file. This is typically how logging is used. Logger only cares that
> the parameter is a stream to which it can write. Instances
> of File, IO and STDOUT/STDERR are all objects that can be used here.
>
>  
>
>  
>
> 148.The sleep method is used to suspend the current thread for some
> amount of time
>
> sleep 0.1
>
>  
>
> 149\. The Ruby standard library has a Benchmark class -
>
> require 'benchmark'
>
>  
>
> puts Benchmark.measure { 602214.times { 3.14159 \* 6.626068 } }
>
>  
>
> The measure method gives you the time taken to execute the block of
> code It is already present in the Ruby standard library, has more
> functionality and is easy to use.
>
>  
>
> A common use case of benchmarking is to compare the performance of
> different implementations of the same functionality.
> The Benchmark class provides the method bm for this.
>
>  
>
> 150.Everything in Ruby is an object. All objects have an identity;
> they can also hold state and manifest behaviour by responding to
> messages. These messages are normally dispatched through method calls.
>
> But what about a method? Is that an object too? Ruby provides an
> object representation for methods as
> well. method(method\_name) returns a method object that
> holds method\_name
>
> Blocks, lambdas, Class - all of the them are objects. Every expression
> in Ruby evaluates to an object. 
>
>  
>
> The Ruby VM keeps track of every object in memory through
> the object\_id method which is present in all objects in Ruby.
> Different objects always have different ids.
>
>  
>
> The class definition from which an object was instantiated is an
> intrinsic part of its identity. The class method serves this purpose
> and is present in every object in Ruby
>
>  
>
> What is the class of the class definition itself? All such class
> definitions themselves belongs to the class Class. The class
> definition objects can instantiate objects of its class.
>
>  
>
> 151.You can check whether an object, say x is an instance of a
> particular class A by comparing x.class == A. The instance\_of? method
> is a standard Ruby method that is a shorthand for this:
>
>  
>
> 152.When a Ruby object receives a message, it checks to see if a
> method of the same name exists. If there is one, that method is
> invoked with the appropriate parameters. If the method doesn't exist,
> it calls the method\_missing method and passes the message to it.
>
>  
>
> The methods object\_id, class were not defined by the class Foo. It is
> however present in every object created from Foo. In fact, these
> methods are present in every object in the Ruby object space.
>
>  
>
> The first thing to note is that every object in Ruby by default
> inherits from the class ObjectSince by default every Ruby object
> inherits from Object, all instance methods defined by Object are
> available to every object in Ruby. The
> methods object\_id and class are thus available everywhere.
>
>  even the class definition object Foo is an object and hence begets
> the behaviour exposed by the Object class. We can use
> the is\_a? method to check whether this is true.
>
>  
>
> 153.The superclass method lets us inspect the inheritance hierarchy of
> a class definition.
>
> The inheritance hierarchy shows that Foo's parent is Object and
> Object's parent is BasicObject. BasicObject is the terminal object and
> does not have any more parents.
>
>  
>
> 154.You would have noticed that we re-opened the standard Ruby
> class Object and added a method to it. It is possible to do this with
> any Ruby class. Using this approach you can add your own behaviours to
> even standard objects. This is called monkey-patching. Monkey-patching
> however is not generally encouraged and should be used only as a
> last-resort.
>
>  
>
> 155.The ancestors method simply returns an array that starts with the
> class or module definition on which it was invoked. It then contains
> the superclasses and mixed in modules of the object.
>
> Kernel is a module that is mixed into
> the Object class. Kernel contains methods like puts, p, rand, loop etc
>
>  
>
> 156.The Object class is the ancestor of almost all objects in
> Ruby. Object however inherits fromBasicObject. BasicObject has almost
> no methods of its own. Object on the other hand defines its own
> methods and includes the Kernel mixin as well.
>
> BasicObject comes last in the inheritance hierarchy of any Ruby
> object:
>
>  
>
> BasicObject is useful, albeit rarely, when you need to build a new
> minimal object that does not include the methods defined
> by Object and Kernel.
>
>  
>
> 157.Since all methods are implemented and stored by the class
> definition, it should be impossible for an object to define its own
> methods. However, Ruby provides a way around this - you can define
> methods that are available only for a specific object. Such methods
> are called *Singleton Methods*
>
> foo=Foo.new
>
> def foo.shout
>
> puts "Foo Foo Foo!"
>
> end
>
> foo.shout
>
>  
>
> Here the object foo has the singleton method shout. This is a
> singleton method because it belongs to just one instance of a class
> and will not be shared with others.
>
> However, singleton methods contradict what we found early: instance
> objects cannot hold methods, only class definitions (objects of
> class Class) can.
>
>  
>
> 158.The respond\_to? method tells us whether the object can respond to
> the given message.
>
>  
>
> 159.When you declare a singleton method on an object, Ruby
> automatically creates a class to hold just that method. This class is
> called the 'metaclass' of the object. All subsequent singleton methods
> of this object goes to its metaclass. Whenever you send a message to
> the object, it first looks to see whether the method exists in its
> metaclass. If it is not there, it gets propagated to the actual class
> of the object and if it is not found there, the message traverses the
> inheritance hierarchy.
>
>  
>
> In summary:

-   Objects in Ruby only store the state. Its behaviour comes from its
    > class definition.

-   Objects can also have methods that are independent of the parent
    > class definition. They are called singleton methods and are stored
    > on the metaclass of the object. The metaclass is typically
    > invisible to the programmer.

>  
>
>  
>
> 160.The class &lt;&lt; self syntax changes the current self to point
> to the metaclass of the current object. Since we are already inside an
> instance method, this would be the instance's metaclass. The method
> simply returns self which at this point is the metaclass of the
> instance.
>
> A metaclass is almost a class in many respects. It however can't be
> instantiated:
>
>  
>
>  
>
> 161.Ruby 1.9 introduced the singleton\_class as a shorthand for
> the class &lt;&lt; self syntax we saw earlier. From now on, you can
> just call the singleton\_class instead of our custom metaclass method.
>
> singleton\_methods =
>
> self.singleton\_class.instance\_methods – self.class.instance\_methods
>
>  
>
> Metaclasses are the underlying mechanism using which Ruby provides us
> an object model with inheritance and mixins. However, you would rarely
> find this concept being used while writing Ruby code. . This is
> because Ruby ensures that the abstraction doesn't leak and effectively
> hides the semantics of metaclasses from the programmer. Even though
> this is the case, understanding metaclasses well helps in
> understanding Ruby's object model better.
>
>  
>
> 162.What happens when you assign the same object to two different
> variables?
>
> a = \[1,2,3\]
>
> b = a
>
> b &lt;&lt; 4
>
> Changing b changed a as well! This is because variables store only
> references to objects. When assigning one variable to another, Ruby
> does not copy the actual object - only the references are copied.
>
>  
>
> 163.To create an independent copy of an object, you should use
> the clone method:
>
>  
>
> a = \[1,2,3\]
>
> b = a.clone
>
> b &lt;&lt; 4
>
> The clone method should be used when you need to mutate an object due
> to performance reasons. This ensures that the original object is not
> affected. Mutation of objects results in brittle code and should be
> avoided.
>
>  
>
>  
>
>  
>
>  
>
> 164.There are occasions when you want to prevent any changes to an
> object. This is called 'freezing' an object. All objects in Ruby has
> the freeze method that does this
>
> a.freeze
>
> As you can see, mutating an already frozen object raises an error.
>
> However, this is still possible:
>
> a = \[1,2,3,4\]
>
> a.freeze
>
> a = \[1,2,3\]
>
>  
>
> The above is perfectly valid. As we have demonstrated in the previous
> section, variables only store references to object. The freeze method
> was executed on the actual object and the object remains frozen.
> However, you can change the variable to refer to a different object
> anytime - which is what the example above did.
>
> You can use the frozen? method on an object to check whether an object
> is currently frozen or not.

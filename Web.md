Javascript

Thursday, August 27, 2015

10:14

What is JavaScript?

> Ans:JavaScript is a scripting language most often used for client-side
> web development.
>
>  

Is JavaScript case sensitive?

> Ans:Yes!
>
>  

What is the difference between “==” and “===”?

> Ans:
>
> “==” checks equality only,
>
> “===” checks for equality as well as the type.
>
>  

In JavaScript, scope is the set of variables, objects, and functions you
have access to.JavaScript has function scope: The scope changes inside
functions.

 

If you assign a value to a variable that has not been declared, it will
automatically become a GLOBAL variable.This code example will declare
carName as a global variable, even if it is executed inside a function.

 

If you use var the variable is declared within the scope you are in
(e.g. of the function). If you don't use var, the variable bubbles up
through the layers of scope until it encounters a variable by the given
name or the global object (window, if you are doing it in the browser),
where it then attaches. It is then very similar to a global variable.
However, it can still be deleted with delete (most likely by someone
else's code who also failed to use var). If you use var in the global
scope, the variable is truly global and cannot be deleted.

 

 

A closure is a function having access to the parent scope, even after
the parent function has closed.

 

Does JavaScript Support automatic type conversion, If yes give example.

> Ans: Yes! Javascript support automatic type conversion. You should
> take advantage of it, It is most common way of type conversion used by
> Javascript developers.
>
>  

A callback function is executed after the current effect is 100%
finished.

 

 

 

 

 

Jquery

Thursday, August 27, 2015

10:04

 

-   jQuery is fast, lightweight and feature-rich client side JavaScript
    > Library/Framework

-   The **Document Object Model (DOM)** is an application programming
    > interface (API) for valid HTML and well-formed XML documents. It
    > defines the logical structure of documents and the way a document
    > is accessed and manipulated

-   JavaScript is a language While jQuery is a library built in the
    > JavaScript language that helps to use the JavaScript language.

-   jQuery is not a W3C standard.

-   The starting point of jQuery code execution is \$(document).ready()
    > function which is executed when DOM is loaded.

-   Dollar Sign is nothing but it's an alias for Jquery

-   YES. We can have any number of document.ready() function on the
    > same page.

 

Can we use our own specific character in the place of \$ sign in jQuery?

> Ans: Yes. It is possible using jQuery.noConflict().
>
>  
>
> document.ready() function is called as soon as DOM is loaded where
> body.onload() function is called when everything gets loaded on the
> page that includes DOM, images and all associated resources of the
> page.
>
>  

 

> What is a CDN?
>
> Ans: A content delivery network or content distribution network (CDN)
> is a large distributed system of servers deployed in multiple data
> centers across the Internet. The goal of a CDN is to serve content to
> end-users with high availability and high performance
>
>  
>
> How do you select element by ID in jQuery?
>
>  
>
>  

How jQuery selectors are executed?

> Ans: Your last selectors is always executed first. For example, in
> below jQuery code, jQuery will first find all the elements with class
> ".myCssClass" and after that it will reject all the other elements
> which are not in "p\#elmID".
>
> \$("p\#elmID .myCssClass");
>
>  

What is the difference between jquery.size() and jquery.length?

> Ans: jQuery .size() method returns number of element in the object.
> But it is not preferred to use the size() method as jQuery provide
> .length property and which does the same thing. But the .length
> property is preferred because it does not have the overhead of a
> function call.
>
>  
>
>  
>
> .bind(): This is the easiest and quick method to bind events. But the
> issue with bind() is that it doesn't work for elements added
> dynamically that matches the same selector. bind() only attach events
> to the current elements not future element. Above that it also has
> performance issues when dealing with a large selection.
>
>  
>
> .live(): This method overcomes the disadvantage of bind(). It works
> for dynamically added elements or future elements. Because of its poor
> performance on large pages, this method is deprecated as of jQuery 1.7
> and you should stop using it. Chaining is not properly supported using
> this method.
>
>  
>
>  
>
> Using clone() method, we can create clone of any element but the
> default implementation of the clone() method doesn't copy events
> unless you tell the clone() method to copy the events. The clone()
> method takes a parameter, if you pass true then it will copy the
> events as well.
>
>  

Caching

> \$("\#myID").css("color", "red");
>
> //Doing some other stuff......
>
> \$("\#myID").text("Error occurred!");
>
> Now in above jQuery code, the element with \#myID is used twice but
> without caching. So both the times jQuery had to traverse through DOM
> and get the element. But if you have saved this in a variable then you
> just need to reference the variable. So the better way would be,
>
> Hide Copy Code
>
> var \$myElement = \$("\#myID").css("color", "red");
>
> //Doing some other stuff......
>
> \$myElement.text("Error occurred!");
>
>  

JqueryUI

>  
>
>  

 

 

 

HTML

Thursday, August 27, 2015

10:22

 

New elements in html5?

 

What Is XHTML?

> XHTML stands for EXtensible HyperText Markup Language
>
> XHTML is almost identical to HTML
>
> XHTML is stricter than HTML
>
> XHTML is HTML defined as an XML application
>
> XHTML is supported by all major browsers

 

The &lt;!DOCTYPE&gt; is an instruction to the web browser about what
version of HTML the page is written in. AND The &lt;!DOCTYPE&gt; tag
does not have an end tag and It is not case sensitive.

The &lt;!DOCTYPE&gt; declaration must be the very first thing in HTML5
document, before the &lt;html&gt; tag. As In HTML 4.01, all &lt;!
DOCTYPE &gt; declarations require a reference to a Document Type
Definition (DTD), because HTML 4.01 was based on Standard Generalized
Markup Language (SGML). WHERE AS HTML5 is not based on SGML, and
therefore does not require a reference to a Document Type Definition
(DTD)

 

 

What is the use of localStorage in HTML5?

> Ans: Before HTML5 LocalStores was done with cookies. Cookies are not
> very good for large amounts of data, because they are passed on by
> every request to the server, so it was very slow and in-effective. In
> HTML5, the data is NOT passed on by every server request, but used
> ONLY when asked for. It is possible to store large amounts of data
> without affecting the website’s performance.and The data is stored in
> different areas for different websites, and a website can only access
> data stored by itself.
>
> And for creating localstores just need to call localStorage object
>
>  

What is the sessionStorage Object in html5 ? How to create and access?

> Ans: The sessionStorage object stores the data for one session. The
> data is deleted when the user closes the browser window. like below we
> can create and access a sessionStorage here we created “name” as
> session
>
>  

What purpose does HTML5 serve?

> Ans: HTML5 is the proposed next standard for HTML 4.01, XHTML 1.0 and
> DOM Level 2 HTML. It aims to reduce the need for proprietary
> plug-in-based rich internet application (RIA) technologies such as
> Adobe Flash, Microsoft Silverlight, Apache Pivot, and Sun JavaFX
>
>  

What is the difference between HTMl5 Application cache and regular HTML
browser cache?

> Ans: HTML5 specification allows browsers to prefetch some or all of a
> website assets such as HTML files, images, CSS, JavaScript, and so on,
> while the client is connected. It is not necessary for the user to
> have accessed this content previously, for fetching this content. In
> other words, application cache can prefetch pages that have not been
> visited at all and are thereby unavailable in the regular browser
> cache. Prefetching files can speed up the site’s performance, though
> you are of course using bandwidth to download those files initially.

 

WHAT ARE THE DIFFERENT TYPES OF STORAGE IN HTML5?

> Ans:HTML5 offers two new objects for storing data on the client:
>
> LocalStorage – stores data with no time limit
>
> SessionStorage – stores data for one session.The data is deleted when
> the user closes the browser window.

 

WHAT OTHER ADVANTAGES DOES HTML5 HAVE?

> Ans:a) Cleaner markup
>
> b\) Additional semantics of new elements like &lt;header&gt;,
> &lt;nav&gt;, and &lt;time&gt;
>
> c\) New form input types and attributes that will (and in Opera’s case,
> do) take the hassle out of scripting forms.
>
>  

HTML 5 Features:

> Ans :1. The &lt;canvas&gt; element for 2D drawing
>
> 2\. The &lt;video&gt; and &lt;audio&gt; elements for media playback
>
> 3\. local storage support.
>
> 4\. Added New elements, like &lt;figure&gt;,&lt;small&gt;,
> &lt;header&gt;, &lt;nav&gt;,&lt;article&gt;, &lt;footer&gt;,
> &lt;section&gt;,&lt;mark&gt;
>
> 5\. New form controls, like placeholder,calendar, date, time, email, url,
> search,required ,autofocus
>
> 6\. In HTML5 there is only one &lt;!doctype&gt; declaration: &lt;!DOCTYPE
> html&gt;
>
>  

Explain the difference between HTML and HTML5

> HTML5 is nothing more then upgraded version of HTML where in HTML5 Lot
> of new future like Video, Audio/mp3, date select function ,
> placeholder , Canvas, 2D/3D Graphics, Local SQL Database added so that
> no need to do external plugin like Flash player or other library

 

 

 

 

 

 

 

 

 

 

CSS

Thursday, August 27, 2015

10:42

What is CSS?

> CSS is a standard for applying style to HTML elements. This styling
> includes margins, positioning, fonts, colors, and so forth. The
> styling can apply to the complete document or be granular and apply to
> a specific element. Theoretically, the use of CSS promotes the
> separation of content and design, allowing the designer to focus on
> how a Web application will look while the developer(s) concentrate on
> the structure and functionality.
>
> The main part of CSS is a rule. A rule consists of a selector (i.e.,
> what will be styled) followed by a declaration (i.e., the style to be
> applied) that is broken into one or more properties and associated
> styles. In the following example, h1 is the selector, followed by the
> color property and the style of blue.
>
> h1 {color: blue;}
>
>  

What does the cascading portion of CSS mean?

> Cascading refers to cascading order. It is a system of sorting the
> various CSS declarations to avoid conflicts. The process begins with a
> search for all declarations that apply to specific elements; it ends
> if no match is found. Cascading occurs if multiple styles are defined
> for an element. In general, values will be applied from the more
> specific style sheet.

 

Is CSS case-sensitive?

> The CSS standard is not case-sensitive, but if an XHTML doctype is
> used, then CSS class names will be case-sensitive in some browsers. In
> addition, items like font families, image URLs, and other direct
> references with the style sheet can be case-sensitive. To be safe, you
> should stick with lower-case to avoid confusion or unexpected
> problems.

 

What are different ways to apply styles to a Web page?

> There are four ways to integrate CSS into a Web page (some consider
> items three and four the same):
>
> Inline: HTML elements may have CSS applied to them via the STYLE
> attribute.
>
> Embedded: CSS may be embedded in a Web page by placing the code in a
> STYLE element within the HEAD element.
>
> Linked: CSS may be placed in an external file (a simple text file
> containing CSS) and linked via the link element.
>
> Imported: Another way to utilize external CSS files via @import.
>
>  

What is a class?

> A class is a style (i.e., a group of CSS attributes) that can be
> applied to one or more HTML elements. This means it can apply to
> instances of the same element or instances of different elements to
> which the same style can be attached. Classes are defined in CSS using
> a period followed by the class name. It is applied to an HTML element
> via the class attribute and the class name.

 

What is the difference between an ID selector and CLASS?

> An ID selector identifies and sets style to only one occurrence of an
> element, while CLASS can be attached to any number of elements.

 

What is grouping?

> When more than one selector shares the same declaration, they may be
> grouped together via a comma-separated list; this allows you to reduce
> the size of the CSS (every bit and byte is important) and makes it
> more readable. The following snippet applies the same background to
> the first three heading elements.
>
> h1, h2, h3 {background: red;}
>
>  

What are child selectors?

> A child selector is used when you want to match an element that is the
> child of another specific element. The parent and child selectors are
> separated by spaces. The following selector locates an unordered list
> element within a paragraph element and makes a text within that
> element bold.
>
> p &gt; ul {font-weight: bold;}
>
>  

 

What are pseudo classes?

> Pseudo classes allow you to identify HTML elements on characteristics
> (as opposed to their name or attributes). The classes are specified
> using a colon to separate the element name and pseudo class. A good
> example is the :link and :visited pseudo classes for the HTML A
> element. Another good example is first-child, which finds an element's
> first child element.
>
> The following CSS makes all visited links red and green, the actual
> link text becomes yellow when the mouse pointer is positioned over it,
> and the text of the first element of a paragraph is bold.
>
> a:link {font-color: red;}
>
> a:visited {font-color: green;}
>
> a:hover {font-color: yellow;}
>
> p.first-child {font-weight: bold;}

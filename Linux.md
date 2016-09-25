 

Tuesday, August 11, 2015

12:35

 

Groups: list groups

groupadd developers : add group developers

useradd -G infosys humera

passwd vivek

 

id vivek : check user

 

 

 

There is no block comment on shell script.

Using vi ( yes vi ) you can easily comment from line n to m

&lt;ESC&gt;\
:10,100s/\^/\#/

*( that reads, from line 10 to 100 substitute line start (\^) with a \#
sign. )*

and un comment with

&lt;ESC&gt;\
:10,100s/\^\#//

*( that reads, from line 10 to 100 substitute line start (\^) followed
by \# with noting //. )*

vi is almost universal on anywhere where there is /bin/sh

 

From
&lt;<http://stackoverflow.com/questions/947897/block-comments-in-a-shell-script>&gt;

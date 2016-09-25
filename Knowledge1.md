 

Monday, March 23, 2015

14:38

 

java -cp jar1:jar2:jar3:dir1:. HelloWorld

The default classpath (unless there is a CLASSPATH environment variable)
is the current directory so if you redefine it, make sure you're adding
the current directory (.) to the classpath as I have done.

 

From
&lt;<http://stackoverflow.com/questions/2096283/including-jars-in-classpath-on-commandline-javac-or-apt>&gt;

 

 

<http://stackoverflow.com/questions/18226317/how-to-use-memcached-on-different-port>
: memcache windows test

 

 

 

 

 

 

1\. To set the environment variables:

echo ‘export JAVA\_HOME=/opt/jdk1.5.0\_12′ &gt; /etc/profile.d/jdk.sh\
echo ‘export PATH=\$JAVA\_HOME/bin:\$PATH’ &gt;&gt;
/etc/profile.d/jdk.sh

2\. You have to source the file you just created by typing:

source /etc/profile.d/jdk.sh

 

From
&lt;<http://www.cyberciti.biz/faq/linux-unix-set-java_home-path-variable/>&gt;

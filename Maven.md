 

Friday, January 15, 2016

16:58

 

1.  There are two locations where a settings.xml file may live:

>  
>
> **The Maven install: \$M2\_HOME/conf/settings.xml**
>
> **A user’s install: \${user.home}/.m2/settings.xml**
>
> The former settings.xml are also called global settings, the latter
> settings.xml are referred to as user settings. If both files exists,
> their contents gets merged, with the user-specific settings.xml being
> dominant.
>
>  
>
> *Example Settings for Maven*
>
>  

1.  &lt;localRepository&gt;\${user.home}/.m2/repository&lt;/localRepository&gt;

2.  &lt;interactiveMode&gt;true&lt;/interactiveMode&gt;

3.  &lt;usePluginRegistry&gt;false&lt;/usePluginRegistry&gt;

4.  &lt;offline&gt;false&lt;/offline&gt;

>  
>
>  

1.  **localRepository**: This value is the path of this build system’s
    > local repository. The default
    > value is \${user.home}/.m2/repository. This element is especially
    > useful for a main build server allowing all logged-in users to
    > build from a common local repository.

>  
>
>  
>
>  

1.  &lt;pluginGroups&gt;

> &lt;pluginGroup&gt;org.mortbay.jetty&lt;/pluginGroup&gt;
>
> &lt;/pluginGroups&gt;
>
> This element contains a list of pluginGroup elements, each contains a
> groupId. The list is searched when a plugin is used and the groupId is
> not provided in the command line. This list automatically contains
> org.apache.maven.plugins and org.codehaus.mojo.
>
>  
>
>  

1.  The repositories for download and deployment are defined by the
    > repositories and distributionManagement elements of the POM.
    > However, certain settings such as username and password should not
    > be distributed along with the pom.xml. **This type of information
    > should exist on the build server in the settings.xml.**

>  
>
>  
>
> &lt;servers&gt;
>
> &lt;server&gt;
>
> &lt;id&gt;server001&lt;/id&gt;
>
> &lt;username&gt;my\_login&lt;/username&gt;
>
> &lt;password&gt;my\_password&lt;/password&gt;
>
> &lt;privateKey&gt;\${user.home}/.ssh/id\_dsa&lt;/privateKey&gt;
>
> &lt;passphrase&gt;some\_passphrase&lt;/passphrase&gt;
>
> &lt;filePermissions&gt;664&lt;/filePermissions&gt;
>
> &lt;directoryPermissions&gt;775&lt;/directoryPermissions&gt;
>
> &lt;configuration&gt;&lt;/configuration&gt;
>
> &lt;/server&gt;
>
> &lt;/servers&gt;
>
>  

1.  **Profiles**

>  
>
> If a profile is active from settings, its values will override any
> equivalently ID’d profiles in a POM or profiles.xml file.
>
> Activations are the key of a profile. Like the POM’s profiles, the
> power of a profile comes from its ability to modify some values only
> under certain circumstances; those circumstances are specified via an
> activation element.
>
>  
>
> Activation occurs when all specified criteria have been met, though
> not all are required at once.
>
> **jdk**: activation has a built in, Java-centric check in the jdk
> element. This will activate if the test is run under a jdk version
> number that matches the prefix given. In the above example, 1.5.0\_06
> will match. Ranges are also supported as of Maven 2.1. See the
> maven-enforcer-plugin for more details about supported ranges.
>
> **os**: The os element can define some operating system specific
> properties shown above. See the maven-enforcer-plugin for more details
> about OS values.
>
> **property**: The profile will activate if Maven detects a property (a
> value which can be dereferenced within the POM by \${name}) of the
> corresponding name=value pair.
>
> **file**: Finally, a given filename may activate the profile by the
> existence of a file, or if it is missing.
>
>  
>
> The activation element is not the only way that a profile may be
> activated. The settings.xml file’s activeProfile element may contain
> the profile’s id. They may also be activated explicitly through the
> command line via a comma separated list after the -P flag
>
>  

1.  **Properties**

> Maven properties are value placeholder, like properties in Ant. Their
> values are accessible anywhere within a POM by using the notation
> \${X}, where X is the property.
>
>  
>
> **env.X**: Prefixing a variable with “env.” will return the shell’s
> environment variable. For example, \${env.PATH} contains the \\\$path
> environment variable (%PATH% in Windows).
>
> **project.x**: A dot (.) notated path in the POM will contain the
> corresponding element’s value. For example:
> &lt;project&gt;&lt;version&gt;1.0&lt;/version&gt;&lt;/project&gt; is
> accessible via \${project.version}.
>
> **settings.x**: A dot (.) notated path in the settings.xml will
> contain the corresponding element’s value. For example:
> &lt;settings&gt;&lt;offline&gt;false&lt;/offline&gt;&lt;/settings&gt;
> is accessible via \${settings.offline}.
>
> **Java System Properties**: All properties accessible via
> java.lang.System.getProperties() are available as POM properties, such
> as \${java.home}.
>
> **x**: Set within a &lt;properties /&gt; element or an external files,
> the value may be used as \${someVar}
>
>  
>
>  

1.  **Repositories**

>  
>
> Repositories are remote collections of projects from which Maven uses
> to populate the local repository of the build system. It is from this
> local repository that Maven calls it plugins and dependencies.
> Different remote repositories may contain different projects, and
> under the active profile they may be searched for a matching release
> or snapshot artifact.
>
>  

1.  The final piece of the settings.xml puzzle is the
    > **activeProfiles** element. This contains a set of activeProfile
    > elements, which each have a value of a profile id. Any profile id
    > defined as an activeProfile will be active, reguardless of any
    > environment settings. If no matching profile is found nothing
    > will happen. For example, if env-test is an activeProfile, a
    > profile in a pom.xml (or profile.xml with a corrosponding id will
    > be active. If no such profile is found then execution will
    > continue as normal.

>  

 

 

 

Friday, January 15, 2016

17:13

 

**Using Mirrors for Repositories**

To configure a mirror of a given repository, you provide it in your
settings file (\${user.home}/.m2/settings.xml), giving the new
repository its own id and url, and specify the mirrorOf setting that is
the ID of the repository you are using a mirror of. For example, the ID
of the main Maven Central US repository included by default is central,
so to use the European Central instance, you would configure the
following:

 

&lt;mirrors&gt;

&lt;mirror&gt;

&lt;id&gt;UK&lt;/id&gt;

&lt;name&gt;UK Central&lt;/name&gt;

&lt;url&gt;http://uk.maven.org/maven2&lt;/url&gt;

&lt;mirrorOf&gt;central&lt;/mirrorOf&gt;

&lt;/mirror&gt;

&lt;/mirrors&gt;

 

Note that there can be at most one mirror for a given repository. In
other words, you cannot map a single repository to a group of mirrors
that all define the same &lt;mirrorOf&gt; value. Maven will not
aggregate the mirrors but simply picks the first match. If you want to
provide a combined view of several repositories, use a repository
manager instead.

 

 

You can force Maven to use a single repository by having it mirror all
repository requests. The repository must contain all of the desired
artifacts, or be able to proxy the requests to other repositories. This
setting is most useful when using an internal company repository with
the Maven Repository Manager to proxy external requests. To achieve
this, set mirrorOf to \*.

 

 

 

 

 

Friday, January 15, 2016

17:18

 

**Apache Maven Compiler Plugin**

 

The Compiler Plugin is used to compile the sources of your project.
Since 3.0, the default compiler is javax.tools.JavaCompiler (if you are
using java 1.6) and is used to compile Java sources. If you want to
force the plugin using javac, you must configure the plugin option
forceJavacCompilerUse. Also note that at present the default source
setting is 1.5 and the default target setting is 1.5, independently of
the JDK you run Maven with. If you want to change these defaults, you
should set source and target.

 

 

&lt;plugins&gt;

&lt;plugin&gt;

&lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;

&lt;artifactId&gt;maven-compiler-plugin&lt;/artifactId&gt;

&lt;version&gt;3.3&lt;/version&gt;

&lt;configuration&gt;

&lt;source&gt;1.4&lt;/source&gt;

&lt;target&gt;1.4&lt;/target&gt;

&lt;/configuration&gt;

&lt;/plugin&gt;

&lt;/plugins&gt;

 

The compilerVersion parameter can be used to specify the version of the
compiler that the plugin will use

 

Sometimes when you may need to compile a certain project to a different
version than what you are currently using. The javac can accept such
command using -source and -target. The Compiler Plugin can also be
configured to provide these options during compilation

 

 

 

Friday, January 15, 2016

17:21

 

**Apache Maven Deploy Plugin**

 

The deploy plugin is primarily used during the deploy phase, to add your
artifact(s) to a remote repository for sharing with other developers and
projects. This is usually done in an integration or release environment.
It can also be used to deploy a particular artifact.

 

In order to deploy artifacts using FTP you must first specify the use of
an FTP server in the distributionManagement element of your POM as well
as specifying an extension in your build element which will pull in the
FTP artifacts required to deploy with FTP:

 

&lt;project&gt;

...

&lt;distributionManagement&gt;

&lt;repository&gt;

&lt;id&gt;ftp-repository&lt;/id&gt;

&lt;url&gt;ftp://repository.mycompany.com/repository&lt;/url&gt;

&lt;/repository&gt;

&lt;/distributionManagement&gt;

 

&lt;build&gt;

&lt;extensions&gt;

&lt;!-- Enabling the use of FTP --&gt;

&lt;extension&gt;

&lt;groupId&gt;org.apache.maven.wagon&lt;/groupId&gt;

&lt;artifactId&gt;wagon-ftp&lt;/artifactId&gt;

&lt;version&gt;1.0-beta-6&lt;/version&gt;

&lt;/extension&gt;

&lt;/extensions&gt;

&lt;/build&gt;

...

&lt;/project&gt;

Your settings.xml would contain a server element where the id of that
element matches id of the FTP repository specified in the POM above:

 

&lt;settings&gt;

...

&lt;servers&gt;

&lt;server&gt;

&lt;id&gt;ftp-repository&lt;/id&gt;

&lt;username&gt;user&lt;/username&gt;

&lt;password&gt;pass&lt;/password&gt;

&lt;/server&gt;

&lt;/servers&gt;

...

&lt;/settings&gt;

You should, of course, make sure that you can login into the specified
FTP server by hand before attempting the deployment with Maven. Once you
have verified that everything is setup correctly you can now deploy your
artifacts using Maven:

 

mvn deploy

 

 

------------------------

In order to deploy artifacts using SSH you must first specify the use of
an SSH server in the distributionManagement element of your POM as well
as specifying an extension in your build element which will pull in the
SSH artifacts required to deploy with SSH:

 

 

 

 

 

Friday, January 15, 2016

17:24

**Apache Maven Install Plugin**

 

The Install Plugin is used during the install phase to add artifact(s)
to the local repository. The Install Plugin uses the information in the
POM (groupId, artifactId, version) to determine the proper location for
the artifact within the local repository.

 

The local repository is the local cache where all artifacts needed for
the build are stored. By default, it is located within the user's home
directory (\~/.m2/repository) but the location can be configured in
\~/.m2/settings.xml using the &lt;localRepository&gt; element.

 

 

 

 

 

Friday, January 15, 2016

17:25

 

**Apache Maven Resources Plugin**

 

The Resources Plugin handles the copying of project resources to the
output directory. There are two different kinds of resources: main
resources and test resources. The difference is that the main resources
are the resources associated to the main source code while the test
resources are associated to the test source code.

Thus, this allows the separation of resources for the main source code
and its unit tests.

 

 

**Specifying resource directories**

 

By default, Maven will look for your project's resources
under src/main/resources.

Project\
|-- pom.xml\
\`-- src\
\`-- main\
\`-- resources

However, all your resources may not be in src/main/resources. Thus,
you'd have to specify those directories by adding the following to your
POM.

&lt;project&gt;\
...\
&lt;build&gt;\
...\
&lt;resources&gt;\
&lt;resource&gt;\
&lt;directory&gt;\[your folder here\]&lt;/directory&gt;\
&lt;/resource&gt;\
&lt;/resources&gt;\
...\
&lt;/build&gt;\
...\
&lt;/project&gt;

 

Furthermore, you can have several directories by adding
multiple &lt;resource&gt; elements:

...\
&lt;resources&gt;\
&lt;resource&gt;\
&lt;directory&gt;resource1&lt;/directory&gt;\
&lt;/resource&gt;\
&lt;resource&gt;\
&lt;directory&gt;resource2&lt;/directory&gt;\
&lt;/resource&gt;\
&lt;resource&gt;\
&lt;directory&gt;resource3&lt;/directory&gt;\
&lt;/resource&gt;\
&lt;/resources&gt;\
...

 

 

 

 

 

 

 

Friday, January 15, 2016

17:28

 

**Maven Surefire Plugin**

The Surefire Plugin is used during the test phase of the build lifecycle
to execute the unit tests of an application.

 

*Junit*

To get started with JUnit, you need to add the required version of JUnit
to your project: This is the only step that is required to get started

 

**Running Tests in Parallel**

From JUnit 4.7 onwards you can run your tests in parallel. To do this,
you must set the parallel parameter, and may change
the threadCount oruseUnlimitedThreads

 

To skip running the tests for a particular project, set
the **skipTests** property to **true**.

 

You can also skip the tests via the command line by executing the
following command: mvn install -DskipTests

 

 

**Skipping by Default**

If you want to skip tests by default but want the ability to re-enable
tests from the command line, you need to go via a properties section in
the pom:

 

 

 

&lt;project&gt;

\[...\]

&lt;properties&gt;

&lt;skipTests&gt;true&lt;/skipTests&gt;

&lt;/properties&gt;

\[...\]

&lt;build&gt;

&lt;plugins&gt;

&lt;plugin&gt;

&lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;

&lt;artifactId&gt;maven-surefire-plugin&lt;/artifactId&gt;

&lt;version&gt;2.19.1&lt;/version&gt;

&lt;configuration&gt;

&lt;skipTests&gt;\${skipTests}&lt;/skipTests&gt;

&lt;/configuration&gt;

&lt;/plugin&gt;

&lt;/plugins&gt;

&lt;/build&gt;

\[...\]

&lt;/project&gt;

This will allow you to run with tests disabled by default and to run
them with this command:

 

mvn install -DskipTests=false

 

 

---------------

 

To skip remaining tests after first failure or error has happened set
configuration parameter skipAfterFailureCount to 1. To skip remaining
tests after the Nth failure or error has happened set configuration
parameter skipAfterFailureCount to N, where N is number greater than
zero.

 

During development, you may re-run failing tests because they are flaky.
To use this feature through Maven surefire, set the
rerunFailingTestsCount property to be a value larger than 0. Tests will
be run until they pass or the number of reruns has been exhausted.

 

**Debugging Tests**

 

Sometimes you need to debug the tests exactly as Maven ran them. Here's
how!

 

By default, Maven runs your tests in a separate ("forked") process. You
can use the maven.surefire.debug property to debug your forked tests
remotely, like this:

 

**mvn -Dmaven.surefire.debug test**

The tests will automatically pause and await a remote debugger on port
5005. You can then attach to the running tests using Eclipse.

 

 

You can force Maven not to fork tests by setting the configuration
parameter forkCount to 0.

mvn -DforkCount=0 test

 

 

Then all you need to do is debug Maven itself. Since Maven 2.0.8, Maven
ships with a mvnDebug shell script that you can use to launch Maven with
convenient debugging options:

mvnDebug -DforkCount=0 test

Then you can attach Eclipse to Maven itself, which may be easier/more
convenient than debugging the forked executable.

 

 

 

 

 

 

Archiver

Monday, January 18, 2016

10:08

 

The default manifest created by Maven Archiver will contain the
following bits of information:

 

 

Manifest-Version: 1.0

Archiver-Version: Plexus Archiver

Created-By: Apache Maven \${maven.version}

Built-By: \${user.name}

Build-Jdk: \${java.version}

 

*&lt;manifest&gt;*

*&lt;addDefaultImplementationEntries&gt;true&lt;/addDefaultImplementationEntries&gt;*

*&lt;addDefaultSpecificationEntries&gt;true&lt;/addDefaultSpecificationEntries&gt;*

*&lt;/manifest&gt;*

 

The resulting manifest would contain these pieces of information:

 

*Manifest-Version: 1.0*

*Archiver-Version: Plexus Archiver*

*Created-By: Apache Maven \${maven.version}*

*Built-By: \${user.name}*

*Build-Jdk: \${java.version}*

*Specification-Title: \${project.name}*

*Specification-Version: \${project.version}*

*Specification-Vendor: \${project.organization.name}*

*Implementation-Title: \${project.name}*

*Implementation-Version: \${project.version}*

*Implementation-Vendor-Id: \${project.groupId}*

*Implementation-Vendor: \${project.organization.name}*

*Implementation-URL: \${project.url}*

 

 

  mainClass     The Main-Class manifest entry.   String
  ------------- -------------------------------- --------
  packageName   Package manifest entry.          String

 

 

 

 

 

 

Packaging

Monday, January 18, 2016

10:06

 

> Specify a list of fileset patterns to be included or excluded by
> adding &lt;includes&gt;/&lt;include&gt; or
> &lt;excludes&gt;/&lt;exclude&gt; in your pom.xml.
>
>  
>
> &lt;configuration&gt;
>
> &lt;includes&gt;
>
> &lt;include&gt;\*\*/service/\*&lt;/include&gt;
>
> &lt;/includes&gt;
>
> &lt;/configuration&gt;
>
>  
>
>  

-   [war:war](https://maven.apache.org/plugins/maven-war-plugin/war-mojo.html) is
    > the default goal invoked during the package phase for projects
    > with a packaging type of war. It builds a WAR file.

-   [war:exploded](https://maven.apache.org/plugins/maven-war-plugin/exploded-mojo.html) is
    > generally used to speed up testing during the developement phase
    > by creating an exploded webapp in a specified directory.

-   [war:inplace](https://maven.apache.org/plugins/maven-war-plugin/inplace-mojo.html) another
    > variation of war:explode where the webapp is instead generated in
    > the web application source directory, which
    > is src/main/webapp by default.

>  
>
>  
>
> The default resource directory for all Maven projects is
> src/main/resources which will end up in target/classes and in
> WEB-INF/classes in the WAR. The directory structure will be preserved
> in the process. The WAR Plugin is also capable of including resources
> not found in the default resource directory through the **webResources
> paramete**r.
>
>  
>
> &lt;configuration&gt;\
> &lt;webResources&gt;\
> &lt;resource&gt;\
> &lt;!-- this is relative to the pom.xml directory --&gt;\
> &lt;directory&gt;resource2&lt;/directory&gt;\
> &lt;/resource&gt;\
> &lt;/webResources&gt;
>
>  
>
>  
>
> webResources is a list of resources. All options of resource are
> supported.
>
> A web resource

-   can have includes/excludes

-   can be filtered

-   is not limited to the default destination - the root of the WAR

>  
>
> **Be careful when mixing includes and excludes, excludes will have a
> higher priority. Includes can not override excludes if a resource
> matches both.**
>
>  
>
>  
>
> **Overriding the default destination directory**
>
> By default web resources are copied to the root of the WAR, as shown
> in the previous example. To override the default destination
> directory, specify the target path.
>
>  
>
> &lt;resource&gt;\
> &lt;directory&gt;configurations&lt;/directory&gt;\
> &lt;!-- override the destination directory for this resource --&gt;\
> &lt;targetPath&gt;WEB-INF&lt;/targetPath&gt;\
> &lt;!-- enable filtering --&gt;\
> &lt;filtering&gt;true&lt;/filtering&gt;\
> &lt;excludes&gt;\
> &lt;exclude&gt;\*\*/properties&lt;/exclude&gt;\
> &lt;/excludes&gt;\
> &lt;/resource&gt;
>
>  
>
>  
>
> **Including and Excluding Files From the WAR**
>
> It is possible to include or exclude certain files from the WAR file,
> by using
> the &lt;packagingIncludes&gt; and &lt;packagingExcludes&gt; configuration
> parameters. They each take a comma-separated list of Ant file set
> patterns. You can use wildcards such as \*\* to indicate multiple
> directories and \* to indicate an optional part of a file or directory
> name.
>
> Sometimes even such wildcards are not enough. In these cases you can
> use regular expressions with the %regex\[\] syntax.
>
>  
>
>  
>
> **Apache Maven Shade Plugin**
>
> This plugin provides the capability to package the artifact in an
> uber-jar, including its dependencies and to *shade* - i.e. rename -
> the packages of some of the dependencies.
>
>  
>
> **Executable JAR**
>
> To create an executable uber JAR, one simply needs to set the main
> class that serves as the application entry point:
>
>  
>
> This snippet configures a special resource transformer which sets
> the Main-Class entry in the MANIFEST.MF of the shaded JAR. Other
> entries can be added to theMANIFEST.MF as well via key-value pairs in
> the &lt;manifestEntries&gt; section:
>
>  
>
> **Resource Transformers**
>
> Aggregating classes/resources from several artifacts into one uber JAR
> is straight forward as long as there is no overlap. Otherwise, some
> kind of logic to merge resources from several JARs is required. This
> is where resource transformers kick in.
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

 

 

 

Monday, January 18, 2016

10:17

 

**Rapid Testing Using the Jetty Plugin**

Normally, testing a web application involves compiling Java sources,
creating a WAR and deploying it to a web container.

Using the Jetty Plugin enables you to quickly test your web application
by skipping the last two steps. By default the Jetty Plugin
scans target/classes for any changes in your Java sources
and src/main/webapp for changes to your web sources. The Jetty Plugin
will automatically reload the modified classes and web sources.

 

&lt;plugin&gt;\
&lt;groupId&gt;org.mortbay.jetty&lt;/groupId&gt;\
&lt;artifactId&gt;maven-jetty-plugin&lt;/artifactId&gt;\
&lt;version&gt;6.1.10&lt;/version&gt;\
&lt;configuration&gt;\
&lt;scanIntervalSeconds&gt;10&lt;/scanIntervalSeconds&gt;\
&lt;connectors&gt;\
&lt;connector
implementation="org.mortbay.jetty.nio.SelectChannelConnector"&gt;\
&lt;port&gt;8080&lt;/port&gt;\
&lt;maxIdleTime&gt;60000&lt;/maxIdleTime&gt;\
&lt;/connector&gt;\
&lt;/connectors&gt;\
&lt;/configuration&gt;\
&lt;/plugin&gt;

 

Then start Jetty:

mvn jetty:run

The command will block with Jetty listening on port 8080.

 

 

 

 

 

 

Reporting

Monday, January 18, 2016

10:22

 

**Apache Maven Changelog Plugin**

The Maven Changelog Plugin generates reports regarding the recent
changes in your Software Configuration Management or SCM. These reports
include the changelog report, developer activity report and the file
activity report.

 

 

The reports may use either range, date, or tag as the type for
generating the reports. Only one type can be set. The change sets can be
configured by setting the correct parameter for the chosen type.
If type "date" is chosen, then the parameter dates should contain the
start and stop dates for the date range. Similar configurations should
be made for the "range" and "tag" types.

To generate the changelog reports, just add the following in your
project's pom.xml:

 

&lt;project&gt;\
...\
&lt;reporting&gt;\
&lt;plugins&gt;\
&lt;plugin&gt;\
&lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;\
&lt;artifactId&gt;maven-changelog-plugin&lt;/artifactId&gt;\
&lt;version&gt;2.3&lt;/version&gt;\
&lt;/plugin&gt;\
&lt;/plugins&gt;\
&lt;/reporting&gt;\
...\
&lt;/project&gt;

 

Aside from the required plugin configuration parameters needed to
generate the reports, all reports will refer to the scm elements inside
the project descriptor for details regarding the connection to the
project's SCM.

 

&lt;project&gt;\
...\
&lt;scm&gt;\
&lt;connection&gt;scm:svn:http://server/path/to/project/trunk&lt;/connection&gt;\
&lt;developerConnection&gt;scm:svn:https://server/path/to/project/trunk&lt;/developerConnection&gt;\
&lt;url&gt;scm:svn:http://server/path/to/view/trunk&lt;/url&gt;\
&lt;/scm&gt;\
...\
&lt;/project&gt;

 

 

 

**Apache Maven Changes Plugin**

This plugin is used to inform your users of the changes that have
occurred between different releases of your project. The plugin can
extract these changes, either from a changes.xml file or from an issue
management system (Jira, Trac and GitHub supported), and presents them
as a report.

You also have the option of creating a release announcement and even
sending it via email to your users.

 

In order to use this goal, simply create a changes.xml file in
the src/changes/ directory. To generate the Changes Report, insert the
Changes Plugin in the &lt;reporting&gt; section of your
project's pom.xml

 

Starting with version 2.4 the plugin comes pre-configured for a whole
bunch of different issue management systems. All you have to to is enter
your issue management system and the URL to it in your POM. It can look
like this:

 

*&lt;project&gt;\
...\
&lt;issueManagement&gt;\
&lt;system&gt;JIRA&lt;/system&gt;\
&lt;url&gt;http://jira.company.com/&lt;/url&gt;\
&lt;/issueManagement&gt;\
...\
&lt;/project&gt;*

 

 

**Apache Maven Checkstyle Plugin**

The Checkstyle Plugin generates a report regarding the code style used
by the developers. 

 

**Checking for Violations as Part of the Build**

If you want to report to the console or fail the build, you must add an
execution of checkstyle::check to the &lt;build&gt; element and
configure any options that you need.

 

Note that the phase that checkstyle::check is bound to is very
important. If bound to the validate phase, it would check the code prior
to compiling the code. If the code is invalid, the parsing errors
reported by checkstyle may be different than what would be expected from
the javac compiler. However, it's guaranteed to run. Another popular
option is to bind it to the verify phase which would run much later (and
allow the javac compiler to flag invalid code prior to checkstyle).
However, if developers generally just use "mvn test" prior to pushing
changes, checkstyle would not run as verify occurs after the test phase.

 

**Apache Maven Javadoc Plugin**

The Javadoc Plugin uses the Javadoc tool to generate javadocs for the
specified project

 

**Maven JXR Plugin**

The JXR Plugin produces a cross-reference of the project's sources. The
generated reports make it easier for the user to reference or find
specific lines of code. It is also handy when used with the PMD Plugin
for referencing errors found in the code.

 

 

**Apache Maven PMD Plugin**

The PMD Plugin allows you to automatically run
the [PMD](http://pmd.sourceforge.net/) code analysis tool on your
project's source code and generate a site report with its results. It
also supports the separate Copy/Paste Detector tool (or CPD) distributed
with PMD.

 

**Maven Surefire Report Plugin**

The Surefire Report Plugin parses the generated TEST-\*.xml files
under \${basedir}/target/surefire-reports and renders them using DOXIA,
which creates the web interface version of the test results.

 

**Apache Maven Assembly Plugin**

 

The Assembly Plugin for Maven is primarily intended to allow users to
aggregate the project output along with its dependencies, modules, site
documentation, and other files into a single distributable archive.

&gt;

 

Currently it can create distributions in the following formats:

-   zip

-   tar

-   tar.gz (or tgz)

-   tar.bz2 (or tbz2)

-   jar

-   dir

-   war

-   and any other format that the ArchiveManager has been configured for

If your project wants to package your artifact in an uber-jar, the
assembly plugin provides only basic support. For more control, use
the [Maven Shade
Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).

 

 

**Apache Maven Dependency Plugin**

The dependency plugin provides the capability to manipulate artifacts.
It can copy and/or unpack artifacts from local or remote repositories to
a specified location.

 

**Maven Enforcer Plugin -**

The Enforcer plugin provides goals to control certain environmental
constraints such as Maven version, JDK version and OS family along with
many more standard rules and user created rules.

This goal is meant to be bound to a lifecycle phase and configured in
your pom.xml. The enforcers execute the configured rules to check for
certain constraints

 

 

**Apache Maven PDF Plugin**

This plug-in allows you to generate a PDF version of your project's
documentation.

 

**Apache Maven Remote Resources Plugin**

This plugin is used to retrieve JARs of resources from remote
repositories, process those resources, and incorporate them into JARs
you build with Maven. A very common use-case is the need to package
certain resources in a consistent way across your organization: at
Apache it is required that every JAR produced contains a copy of the
Apache license and a notice file that references all used software in a
given project.

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

POM Basics

Monday, January 18, 2016

10:36

 

-   **groupId**: This is generally unique amongst an organization or
    > a project. For example, all core Maven artifacts do (well, should)
    > live under the groupId org.apache.maven. Group ID's do not
    > necessarily use the dot notation, for example, the junit project.
    > Note that the dot-notated groupId does not have to correspond to
    > the package structure that the project contains. It is, however, a
    > good practice to follow. When stored within a repository, the
    > group acts much like the Java packaging structure does in an
    > operating system. The dots are replaced by OS specific directory
    > separators (such as '/' in Unix) which becomes a relative
    > directory structure from the base repository. In the example
    > given, the org.codehaus.mojo group lives within
    > the directory \$M2\_REPO/org/codehaus/mojo.

-   **artifactId**: The artifactId is generally the name that the
    > project is known by. Although the groupId is important, people
    > within the group will rarely mention the groupId in discussion
    > (they are often all be the same ID, such as the [Codehaus
    > Mojo](http://mojo.codehaus.org/) project groupId: org.codehaus.mojo).
    > It, along with the groupId, create a key that separates this
    > project from every other project in the world (at least, it
    > should :) ). Along with the groupId, the artifactId fully defines
    > the artifact's living quarters within the repository. In the case
    > of the above
    > project, my-project lives in \$M2\_REPO/org/codehaus/mojo/my-project.

-   **version**: This is the last piece of the naming
    > puzzle. groupId:artifactId denote a single project but they cannot
    > delineate which incarnation of that project we are talking about.
    > Do we want the junit:junit of today (version 4), or of four years
    > ago (version 2)? In short: code changes, those changes should be
    > versioned, and this element keeps those versions in line. It is
    > also used within an artifact's repository to separate versions
    > from each other. my-project version 1.0 files live in the
    > directory structure \$M2\_REPO/org/codehaus/mojo/my-project/1.0.\
    > The three elements given above point to a specific version of a
    > project letting Maven knows *who* we are dealing with,
    > and *when* in its software lifecycle we want them.

-   **packaging**: Now that we have our address structure
    > of groupId:artifactId:version, there is one more standard label to
    > give us a really complete address. That is the project's
    > artifact type. In our case, the example POM
    > for org.codehaus.mojo:my-project:1.0 defined above will be
    > packaged as a jar. We could make it into a war by declaring a
    > different packaging:

> When no packaging is declared, Maven assumes the artifact is the
> default: jar.
>
>  
>
> **Dependencies**
>
> The cornerstone of the POM is its dependency list. Most every project
> depends upon others to build and run correctly, and if all Maven does
> for you is manage this list for you, you have gained a lot. Maven
> downloads and links the dependencies for you on compilation and other
> goals that require them. As an added bonus, Maven brings in the
> dependencies of those dependencies (transitive dependencies), allowing
> your list to focus solely on the dependencies your project requires.
>
>  
>
> Install the dependency locally using the install plugin. The method is
> the simplest recommended method. For example:
>
> mvn install:install-file -Dfile=non-maven-proj.jar
> -DgroupId=some.group -DartifactId=non-maven-proj -Dversion=1
> -Dpackaging=jar
>
>  
>
>  
>
> **scope:**
>
> This element refers to the classpath of the task at hand (compiling
> and runtime, testing, etc.) as well as how to limit the transitivity
> of a dependency. There are five scopes available:

-   **compile** - this is the default scope, used if none is specified.
    > Compile dependencies are available in all classpaths. Furthermore,
    > those dependencies are propagated to dependent projects.

-   **provided** - this is much like compile, but indicates you expect
    > the JDK or a container to provide it at runtime. It is only
    > available on the compilation and test classpath, and is
    > not transitive.

-   **runtime** - this scope indicates that the dependency is not
    > required for compilation, but is for execution. It is in the
    > runtime and test classpaths, but not the compile classpath.

-   **test** - this scope indicates that the dependency is not required
    > for normal use of the application, and is only available for the
    > test compilation and execution phases.

-   **system** - this scope is similar to provided except that you have
    > to provide the JAR which contains it explicitly. The artifact is
    > always available and is not looked up in a repository.

>  
>
> **Dependency Version Requirement Specification**
>
> Dependencies' version element define version requirements, used to
> compute effective dependency version. Version requirements have the
> following syntax:

-   1.0: "Soft" requirement on 1.0 (just a recommendation, if it matches
    > all other ranges for the dependency)

-   \[1.0\]: "Hard" requirement on 1.0

-   (,1.0\]: x &lt;= 1.0

-   \[1.2,1.3\]: 1.2 &lt;= x &lt;= 1.3

-   \[1.0,2.0): 1.0 &lt;= x &lt; 2.0

-   \[1.5,): x &gt;= 1.5

-   (,1.0\],\[1.2,): x &lt;= 1.0 or x &gt;= 1.2; multiple sets are
    > comma-separated

-   (,1.1),(1.1,): this excludes 1.1 (for example if it is known not to
    > work in combination with this library)

>  
>
>  
>
> It is also sometimes useful to clip a dependency's transitive
> dependencies. A dependency may have incorrectly specified scopes, or
> dependencies that conflict with other dependencies in your project.
> Using wildcard excludes makes it easy to exclude all a dependency's
> transitive dependencies.
>
>  
>
> **Inheritance**
>
> The packaging type required to
> be pom for *parent* and *aggregation* (multi-module) projects
>
>  
>
> The elements in the parent POM that are inherited by its children are:

-   dependencies

-   developers and contributors

-   plugin lists

-   reports lists

-   plugin executions with matching ids

-   plugin configuration

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

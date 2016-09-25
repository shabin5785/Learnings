 

Monday, April 20, 2015

12:19

 

> **Storm in pictures**
>
> POSTED ON [FEBRUARY 14, 2014](http://jansipke.nl/storm-in-pictures/)
>
> We’ve been using [Storm](http://storm.incubator.apache.org/) for some
> time now. It is quite easy to start using it in a local environment
> (e.g. your IDE), but it can be a bit daunting to install a cluster and
> then really understand what Storm is actually doing to execute your
> topology.
> The [documentation](http://storm.incubator.apache.org/documentation/Home.html) has
> improved over time, and some blogs have appeared, notably the one
> by [Michael Noll](http://www.michael-noll.com/blog/categories/storm),
> that explain how Storm works. Nevertheless I still felt the need to
> explain to myself how Storm works and hopefully this will prove useful
> to others as well.
>
> We’ll start with some Storm terminology. The following picture shows a
> topology:
>
> ![](media/image1.png){width="7.78125in" height="2.9583333333333335in"}

-   A topology is a description of a workflow. It defines how the code
    > you write is put together and executed.

-   A spout is responsible for data input. Storm does not impose any
    > restriction on the source of the data. Hadoop, for example, wants
    > the data to be in its own filesystem, HDFS. With Storm, you can
    > use any data source you want as long as you’re able to write a
    > piece of code for it that fetches this data. Typically, the input
    > data comes from a queue such as Kafka or ActiveMQ, but databases,
    > filesystems or web servers are also fine.

-   A bolt is responsible for processing the data. It gets data from a
    > spout or another bolt in the form of tuples. A tuple is a
    > lightweight data format provided by Storm that you can use to wrap
    > the data you actually need to process. A bolt either processes the
    > input data and sends it out as another tuple (or set of tuples),
    > or it stores it in some external system. This could be yet another
    > queue, database, filesystem, etc.

-   Storm 0.9 added the notion of a metrics consumer. It is often
    > helpful to know what is going on in your topology. The Storm UI
    > provides some insight, but this is on a general level, i.e. it
    > shows how many tuples were transmitted between spouts and bolts,
    > and how many were acknowledged or failed. It can’t tell anything
    > about the internal state of your spouts and bolts, because that is
    > application specific. This is where the metrics framework, and the
    > metrics consumer in particular, comes into play. The metrics
    > framework allows you to create metrics variables in your spouts
    > and bolts. These metrics are transmitted to the metrics consumer.
    > Like the bolts, it is then your responsibility to push these
    > metrics to an external system for storage or visualization.

> The architecture of Storm is illustrated by the following picture:
>
> ![](media/image2.png){width="6.21875in" height="6.145833333333333in"}

-   There is a single master node that is responsible for the scheduling
    > of tasks in the cluster. One process on this machine is called
    > Nimbus, which performs the actual scheduling of tasks. Another
    > process is the Storm UI, which can be used to view the cluster and
    > the topologies.

-   There are several slave nodes that actually execute your code. One
    > process on these machines is the Supervisor, which supervises the
    > process that actually executes your code (see below for
    > more detail). Another process, new since Storm 0.9, is
    > the Logviewer. It is now possible to use the Storm UI, pinpoint
    > any problem in the execution of your code and then click through
    > to the logfile on the slave node that executed the code.

-   Storm uses ZooKeeper to perform cluster management. In a development
    > environment, a single ZooKeeper node is fine. In a production
    > environment, it is necessary to use three, five or more (2n+1)
    > nodes.

> Storm tries to make use of as much parallelism as possible. To achieve
> this, it uses multiple machines (supervisors), runs several Java
> virtual machines on each machine (workers) and uses many threads per
> JVM (executors). The following picture illustrates this:
>
> ![](media/image3.png){width="5.90625in" height="4.510416666666667in"}
>
> The number of supervisors obviously depends on the number of machines
> you have installed the Storm supervisor process on. The number of
> workers each of these machines run is configured in
> the *storm.yaml* configuration file. By default there are four worker
> processes (JVMs) per supervisor, but this can be changed by adding
> port numbers to this file.
>
> *supervisor.slots.ports:\
> - 6700\
> - 6701\
> - 6702\
> - 6703*
>
> The number of supervisors and workers that are useable by Storm are
> now set. Now we can tell Storm how we want to run our topology on this
> cluster:
>
> ![](media/image4.png){width="5.760416666666667in" height="3.34375in"}
>
> We start by creating a Config object and setting the number of workers
> we want to use for this specific topology. In this case we selected
> two of them. Then we create a TopologyBuilder object and set our
> spout, our bolts and our metrics consumer. We can set two parameters
> that tell Storm how many to have of these components and how parallel
> they should be executed:

-   The first parameter is the parallelism hint. This tells Storm how
    > many executors (threads) should be used for this component. By
    > default this number is equal to 1.

-   The second number we can set is the number of tasks. This tells
    > Storm how many times the component should be present in total. If
    > the number of tasks is higher than the parallelism hint, then
    > there will be executors that run more than one task serially. For
    > example, when using a parallelism hint of 2 and a number of tasks
    > of 6, there will be 2 executors that run 3 components serially. By
    > default the number of tasks is equal to the parallelism hint.

>  
>
> From &lt;<http://jansipke.nl/storm-in-pictures/>&gt;

# Eric Baldeschwieler (Big Data): Apache Hadoop in Context
##### @jeric14

#### What is hadoop?
THE open source big data platform. Yarn is the computation layer, for deploying jobs e.g. MapReduce.

HDFS for distributed file system, data replicated on 3 computers.

Scalable: can make bigger through jsut adding computers. Reliable, because it has self healing built in (e.g. in HDFS). Flexible, because it stores many types of data, and Economical because open source, commodity hardware.

Can run lots of stuff on it. Really large cost advantage because it's open source and you can deploy it yourself in lots of places.

#### Typical hadoop cluster
Composed of 10 to 4500 nodes, 1-4 master nodes. Interchangeable workers. Typical nodes have like 64GB RAM, 2x4-8 core. Switch machines have 10GB about, 2-3 layers of switches.

Local storage is 0.05$ per gigabyte: there are other enterprise storage solutions which cost like 1-10 dollars per gigabyte. When you buy local memory, you also get a compute cluster (if you buy the right ones). Basically, local storage is cost advantageous. Using Hadoop is cheaper than others, basically.

#### What Hadoop is used for
First application was to sort/index the web: have to find out which documents certain words are contained in. Sorting/processing engine, which makes sense. Program in Java or C.Actually works on billions-scale datasets.

Data science, log processing, advertising target building, data warehouse offload, document/audio/video processing, financial processing, seismic, genetic, physics processing.

Application monitoring (e.g. Yelp use case). You can do this with databases, but it's very hard to scale and there's a shit ton of complexity in the database. Other solution (hadoop) is to scrape the logs and put it into an analytics database. This approach is basically inifinitely scalable. Super flexible too because it's just about how you process the logs!

Hadoop clusters involve more stuff than just MR. Message Bus (Kafka, etc), Streaming Engine (like storm, spark), YARN for the actual MR, results stored in HDFS.

#### Pros and cons
Things like Oracle Rack, Vertica, Aster, Greenplum are okay, but they're less scalable, less resilient, more expensive. But you do get rich SQL, better UI (of course, you're paying for it). Redshift also? Should put it in the list.

NoSQL vs. Hadoop: This is basically the difference between interactive (highly available, low latency) data and offline (huge, takes a long time) data. Not the same use case at all.

At this point, Hadoop is NOT JUST map reduce. Over time it's taken in new types of interactivity other than MR through YARN. Pig, Hive, Oozie are examples. Yarn, Mezos. Kafka, Spark/Storm/Samza, Stringer/Presto/Impala/Spark... etc.

#### Takeaways
DIY supercomputing only make sense at scale. Broader enterprise thinks differently than startups. Enterprise thinks differently, will spend more to do more stuff. Building open source communities is not free: lots of time negotiating, marketing, etc for stuff that you really don't care about. The "right to contribute" must be earned over time for a big open source project. Know WHY you are open sourcing: is it for guerilla warfare against enterprise software (Linux, Android, Hadoop), distribution/sales of your stuff (MySQL, Mongo), or for bigger collaboration (HttpD, Git)?

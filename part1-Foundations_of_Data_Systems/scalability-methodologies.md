# Methodologies to scale a system

## 1.Splitting the system

The idea is that, since vertical scaling the whole system is limited by hardware capability, we need to split the system into components and scale each component separately.

Example: "we are designing an e-commerce system"

Ways of splitting could be:
- we can put web application one server and the database on another.
- we can clone the web application to put on multiple servers, all accessing the same database server.
- we can split the database into multiple databases, each containing several tables from the original database. The sub-databases can now be put on separate servers.

> Of course, we cannot split things that easily if we didn’t design our system for that from the beginning. For example, if our application joins data from two tables, these two tables cannot be split into different servers. This little example can show us the importance of designing a system for scalability from the early days.

> HDFS, MapReduce, Kafka, ElasticSearch, and many more applications are designed to be able to split and scale by adding more servers to the application cluster.

## 2: Detecting and Optimizing Bottlenecks

To make the system handle more workloads, we need to find the system’s weakest point and make that point handle more workloads.


Let’s think of an example. In our e-commerce system, we have 5 web servers and 1 database server, each hosted on a separate physical server instance. The web servers are running at about 5% of CPU on average, while the database server is always running at 95% of CPU. The bottleneck of the system in this case is the database server - there’s no point adding more web servers to the system.

To optimize bottleneck at the database server, we can buy a more powerful server and relocate the database into it. If that is not an option, we can try to split the tables on the database into serveral sub-databases on different server instances, but that would include some code modifying, and may not be an option either.

Taking a closer look at the resouce usage on the database server, we find out that most of the time, the CPUs are not doing the computation, but are instead waiting for the I/O requests to complete. We monitor the disk I/O, just to find out that the disk-write is always at 100 MB/s. Now we know that the real bottleneck is the disk I/O - to optimize the disk I/O bottleneck, we can upgrade our HDDs into SSDs, or we can add more disks to the RAID system, or try to use a SAN. 

On the other hand, we can reduce the I/O request by optimizing database queries and indexes. If after creating some database indexes, the disk I/O rate reduces to 10 MB/s, we may not need to upgrade the database server anymore. There were also many times in my past projects, the reason was that the database doesn’t have enough memory to cache the queries, and strange it may sound, but adding more memory could solve the disk I/O problems.

After optimizing the database, our system can handle another million users, but looking at the resources usage, we now see that the web servers are using 99% of CPU all the time, while the database only uses less than 10% of CPU. This time, the web servers become the bottleneck. 

## 3: Detecting and Eliminating Single Point of Failure (SPOF)

To make our system high available, which means the system can still function if some part of it goes down, we have to eliminate its Single Point of Failure.

Back to our example, to eliminate the Single Point of Failure at the database, we can user the mirroring function of the database. We setup the database on 2 separate server instances, one as the master server and the other as the mirror server. If the master goes down, the mirror server will stand up to replace the master to make sure the web servers can still accessing the database.


For the web server, we setup another web server that function exactly the same as the first one. We setup a reverse proxy to load balance requests between the two web server. If a web server breaks down, the reverse proxy will detect and route all traffic to the remaining one.

## 4: Caching

A cache is a hardware or software component that stores data so future requests for that data can be served faster; the data stored in a cache might be the result of an earlier computation, or the duplicate of data stored elsewhere.

If your system has a lot of data that doesn’t changes for short period of time, or if the change isn’t critical and it doesn’t hurt to serve the user with an old version of the data, caching is a good candidate that can optimize your system by ten or even a hundred times.
For example, a news website doesn’t need to change its news every second. People can read a 5-minute-ago version of the news without any critical problems.

### Strategies

- Caching in disk (in form of file)
- Caching in memory
- Caching objects
- Caching in database
- Distributed caching

## 5: Indexing

Indexing is a way of storing data in a suitable structure, so that data retrieval can be fast and accurate.

- Database index
- Search index

## 6: Classifying and Prioritizing Data

Not all data are same

- Real-time vs. Near real-time vs. Offline
- Read-heavy vs. Write-heavy





Reference:
- https://hexadix.com/design-scalable-systems-part-1-the-basics/

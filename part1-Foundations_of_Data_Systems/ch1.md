Problem : 

- There are many database systems with different characteristics, because different applications have different requirements. There are various approaches to caching, several ways of building search indexes, and so on.
- When building an application, we still need to figure out which tools and which approaches are the most appropriate for the task at hand.

Although a *database* and a *message queue* have some superficial similarity— both store data for some time— they have very different *access* patterns, which means different performance characteristics, and thus very different implementations.

**If you are designing a data system or service, a lot of tricky questions arise:**

- How do you ensure that the data remains correct and complete, even when things go wrong internally?
- How do you provide consistently good performance to clients, even when parts of your system are degraded?
- How do you scale to handle an increase in load?
- What does a good API for the service look like?


**Factors that may influence the design of a data system:**

- Skills and experience of the people involved
- Legacy system dependencies
- The timescale for delivery
- Organization’s tolerance of different kinds of risk. 
- Regulatory constraints etc.

**3 concerns that are important in most software systems:**

- *Reliability*: The system should continue to work correctly even in the face of adversity
- *Scalability*: As the system grows (in data volume, traffic volume, or complexity), there should be reasonable ways of dealing with that growth
- *Maintainability*: Over time, many different people will work on the system and they should all be able to work on it productively.

## Reliability

> continuing to work correctly, even when things go wrong

*Go wrong:* The things that can go wrong are called *faults*, and systems that anticipate faults and can cope with them are called *fault-tolerant* or resilient.

*Resilient:* is slightly misleading: it suggests that we could make a system tolerant of every possible kind of fault, which in reality is not feasible.

*Fault is not the same as a failure:* A fault is usually defined as one component of the system deviating from its spec, whereas a failure is when the system as a whole stops providing the required service to the user.

> Many critical bugs are actually due to poor error handling by deliberately inducing faults, you ensure that the fault-tolerance
machinery is continually exercised and tested, which can increase your confidence that faults will be handled correctly when they occur naturally. The Netflix [Chaos Monkey](https://netflix.github.io/chaosmonkey/) is an example of this approach.

### Faults

**Hardware Faults**

- Hard disks crash
- RAM becomes faulty 
- the power grid has a blackout
- someone unplugs the wrong network cable. etc.


One solution that comes into our mind is : [RAID](https://en.wikipedia.org/wiki/Standard_RAID_levels) : Redundant Array of Independent Disks.


**Software Errors**

- A software bug that causes every instance of an application server to crash when given a particular bad input.
- A runaway process that uses up some shared resource—CPU time, memory, disk space, or network bandwidth.
- A service that the system depends on that slows down
- Cascading failures, where a small fault in one component triggers a fault in another component, which in turn triggers further faults.

**Human Errors**

Even when they have the best intentions, humans are known to be unreliable. How do we make our systems reliable, in spite of unreliable humans?

- Design systems in a way that minimizes opportunities for error. For example, well-designed abstractions, APIs, and admin interfaces make it easy to do “the right thing” and discourage “the wrong thing.”
- Provide fully featured non-production sandbox environments where people can explore and experiment safely, using
real data, without affecting real users.
- Set up detailed and clear monitoring, such as performance metrics and error rates.


## Scalability


Even if a system is working reliably today, that doesn’t mean it will necessarily work reliably in the future. One common reason for degradation is increased load: perhaps the system has grown from 10,000 concurrent users to 100,000 concurrent users, or
from 1 million to 10 million. Perhaps it is processing much larger volumes of data than it did before.

> Scalability is the term we use to describe a system’s ability to cope with increase load.

## Describing Load

- First, we need to clearly describe the current load on the system;
- then can we discuss growth questions

- Load can be described with a few numbers which we call load parameters.
  - it may be requests per second to a web server
  - the ratio of reads to writes in a database
  - number of simultaneously active users in a chat room
  - hit rate on a cache etc.
- 













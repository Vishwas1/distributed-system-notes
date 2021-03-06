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

Examples of key load parameter:
  - Requests per second
  - Ratio of read and writes in database.
  - Number of simultaneous active users in chat room.
  - Hit rate on cache.

In the above use-case, distribution of followers per user is the key load parameter. 


## Describe Performance

Investigate what happens when the load increases. 

2 ways: 
  - When you increase a load param, by keeping system resource (CPU, memory, network bandwidth) fix, how is the performance of your system affected?
  - When you increase a load param, how much do you need to increase resource if you want to keep performance unchanged?

Throughput: 
  - Number of records we can process per second.  
  - Or, total time it takes to process a dataset of certain size.

Response time:
  - Time between a client sending a request and receiving response. 
  - This is what client sees; besides actual time to process the request, it includes network delay, queueing delays.


Latency:
  - Not same as response time. 
  - Is the duration that a request is waiting to be handled.
  - For instance, you want to invoke a web service or access a web page. Apart from the processing time that is needed on the server to process your request, there is a delay  - involved for your request to reach to server. While referring to Latency, it’s that delay we are talking about.

> Even if you make same request over and over again, you will get slightly different response time. 

*Mean* is not a very good metric if you want to know your “typical” response time since it does not tell how many users actually experienced that delay. 

*Percentile* is better. If you take your list of response time and sort it from fastest to slowest, then median  will tell how long half of the users have to wait; half of the users are served in median response time. *Median* is also known as the *50th percentile*.

> Median can be good metric to measure performance

## Approaches for Coping with Load

- Vertical scale (scaling up) 
  - Moving to more powerful machine.
  - Single point of failure
  - No load balancer required
  - [IPC](https://www.youtube.com/watch?v=dJuYKfR8vec) - which is fast
  - Single source of truth
  - Expensive 

- Horizontal scale (scaling out) 
  - Distributing the load across multiple smaller machines.
  - Resilient
  - Load balancer required since there are multiple machines.
  - Network calls ([RPC](https://www.youtube.com/watch?v=QmhTjsOOrlw)) - slow 
  - No single source of truth - data consistency is the issue since

## Maintainability 

  - Make it easy for operations teams to keep the system running smoothly
  - Make it easy for new engineers to understand the system, by removing complexity.
  - Make it easy for engineers to make changes to the system in the future.
    - Test driven development
    - Refactoring


Notes/References
- [DESIGNING SCALABLE SYSTEMS – PART 1: THE BASICS](https://hexadix.com/design-scalable-systems-part-1-the-basics/)
- [IPC](https://www.youtube.com/watch?v=dJuYKfR8vec)
- [Note: use IPC if the processes are on different systems](https://stackoverflow.com/questions/3742334/using-ipc-for-different-systems)
- [RPC](https://www.youtube.com/watch?v=QmhTjsOOrlw)
















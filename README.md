# go-distributed-system
# A series of distributed systems challenges brought to you by Fly.io.

## Challenge #1: [Echo](https://fly.io/dist-sys/1/)

### Cracking the Maelstrom 

---

## Challenge #2: [Unique ID Generation](https://fly.io/dist-sys/2/)
### Problem
Implement a globally-unique ID generation system that runs against Maelstrom's unique-ids workload. Your service should be totally available, meaning that it can continue to operate even in the face of network partitions.


#### Evaluations
Run a 3-node cluster for 30 seconds and request new IDs at the rate of 1000 requests per second. It checks for total availability and will induce network partitions during the test. It will also verify that all IDs are unique.

- Global unique ID
- High availability
- Network partitions


### Tech Designs
There are multiple ways to design a system for implementing a global ID generator service

1. Google UUID

Concept of UUID
- UUID (Universally Unique Identifier) is a standard for generating unique identifiers in distributed systems. <span style="color:#FFD580">It ensures that even in scenarios where multiple systems are generating IDs independently, the chance of collision (two systems generating the same ID) is extremely low.</span>
- A UUID is a 128-bit value typically represented as a string of hexadecimal characters, divided into five groups separated by hyphens. The format of a UUID is as follows: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx, where each 'x' represents a hexadecimal digit (0-9 or a-f).
- The 128 bits of a UUID are generated using a combination of different elements, including <span style="color:#FFD580">the current timestamp, the unique MAC address of the system generating the UUID, and random or pseudo-random bits.</span> This combination ensures that even if multiple systems generate a UUID at the same time, the likelihood of collisions is minimized.

Advantages
- Simple implementation enables high throughputs for generating IDs.
- The chance of collision (two systems generating the same ID) is extremely low, ensuring uniqueness of generated IDs.
- Independent generation of IDs without the need for synchronization or coordination with other nodes.

Further discussions
- Network partitioning: While UUIDs themselves are resilient to network partitions, the challenge lies in ensuring consistency and availability of the UUID generation service during and after a partition. Depending on the system's requirements, we may need to consider techniques such as distributed consensus algorithms or handling stale data during reconciliation post-partition.

- Scalability and load balancing: As the system scales and the number of clients and servers increase, load balancing the UUID generation workload becomes crucial to avoid bottlenecks and ensure optimal performance.

- High availability: Redundancy, replication, and failover mechanisms should be in place to ensure the availability of the UUID generator service even in the event of server failures or outages.
>>>>>>> 84c30cc (Implement global unique ID generator)

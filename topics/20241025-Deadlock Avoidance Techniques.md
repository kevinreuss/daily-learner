# Deadlock Avoidance Techniques

Deadlock is a situation where two or more processes are unable to proceed because each is waiting for the other to release resources. Deadlock avoidance aims to evade the occurrence of deadlock by careful resource scheduling. Here we discuss two main techniques for deadlock avoidance: Banker's Algorithm and Resource Allocation Graph (RAG).

## Banker's Algorithm
The Banker's Algorithm, proposed by Edsger Dijkstra, is a resource scheduling method that avoids deadlock by simulating resource allocation for each process, and checking if this would lead to a safe state. A state is considered safe if there exists a sequence of all processes in the system where every process can request resources and still allow the remaining processes to complete.

Here's a pseudo-code snippet for the Banker's Algorithm:

```python
def bankers_algorithm(state, processes, resources):
    # Step 1: Initialization
    work = available_resources(state)
    finish = [False] * len(processes)

    # Step 2: Find an index i such that both:
    for i in range(len(processes)):
        if not finish[i] and can_finish(processes[i], work):
            # Step 3: Simulate the execution
            work += resources[i]
            finish[i] = True
            break
    # Step 4: Check if state is safe
    if False in finish:
        return "Unsafe State"
    else:
        return "Safe State"
```

## Resource Allocation Graph (RAG)
A Resource Allocation Graph represents processes and resources as vertices, and the allocation and request of resources as edges. Deadlock can be avoided by ensuring that no cycles exist in the graph. 

If a process requests a resource that creates a cycle (i.e., the graph becomes cyclic), the resource is not immediately allocated. The system checks if allocating the requested resource to the process does not result in a cycle in the RAG.

Here's a basic example of a RAG:

```
P1 ---> R1 <--- P2
```

In the diagram above, P1 and P2 are processes, R1 is a resource. P1 requests for R1 (P1 ---> R1), while R1 is held by P2 (R1 <--- P2). No cycle exists, so the system is in a safe state.

For more in-depth knowledge, you can refer to the [Wikipedia page on Deadlock Prevention Algorithms](https://en.wikipedia.org/wiki/Deadlock_prevention_algorithms).

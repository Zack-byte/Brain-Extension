# Systems Performance (Author: Brendan Gregg)
`Systems Performance` Enterprise and the Cloud <i>Second Edition </i> by Brendan Gregg is the second performance book by the author covering everything from `models`, `architecture`, and `methodologies` related to performance to `tools` and `specific examples` that can be used to enrich knowledge on performance history and prepare Engineers for future performance based problems and endeavors.

The book covers a large set of technologies however OS wise focuses on Linux based systems and references other OS's when necessary. 

Probably one of the most thought provoking quotes in the preface for me -> 
**"If a tool does require laborious explanation, that may be a failure of design!"**

### How the book is Structured
1. `Introduction`: introduces systems performance analysis, summarizing key concepts and providing examples of performance activities
2. `Methodologies`, provides the background for performance analysis and tuning, including terminology, concepts, models, methodologies for observation and experimentation, capacity planning, analysis, and statistics.
3. `Operating Systems`: summarizes kernel internals for the performance analyst. This is necessary background for interpreting and understanding what the operating system is doing.
4. `Observability Tools`: introduces the types of system observability tools available, and the interfaces and frameworks upon which they are built.
5. `Applications`: discusses application performance topics and observing them from the operating system.
6. `CPUs`: covers processors, cores, hardware threads, CPU caches, CPU interconnects, device interconnects, and kernel scheduling.
7. `Memory`: is about virtual memory, paging, swapping, memory architectures, buses, address spaces, and allocations.
8. `File Systems`: is about file system I/O performance, including the different caches involved.
9. `Disks`: covers storage devices, disk I/O workloads, storage controllers, RAID, and the kernel I/O subsystem.
10. `Network`: is about network protocols, sockets, interfaces, and physical connections.
11. `Cloud Computing`: introduces operating system and hardware based virtualization methods in common use for cloud computing along with their performance overhead, isolation, and observability characteristics. this chapter covers hypervisors and containers.
12. `Benchmarking`: shows how to benchmark accurately, and how to interpret others benchmark results. This is a surprisingly tricky topic, and this chapter shows how you can avoid common mistakes and try to make sense of it.
13. `perf`: summarizes the standard Linux profiler and its capabilities
14. `Ftrace`: Linux's tracer, especially good for exploring kernel code execution.
15. `BPF`: summaries the BPF front ends: `BCC` and `bpftrace`
16. `Case Study`: A systems performance case study from Netflix.



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

### Tracing
This book goes over the `BCC` and `bpftracing` tools as well as Linux's built in `Ftrace` tool. Windows also has tracing tools such as `Tracelog`, `Tracefmt`, `Tracepdb`, `Tracerpt`.

### Typographic Conventions
Conventions used in the book. **TODO: Come back and flesh out the table**


## Chapter 1 Introduction
Chapter Objectives:
- Understand systems performance roles, activities, and challenges.
- Understand the difference between observability, and experimental tools.
- Develop a basic understanding of performance observability: statistics, profiling, flame graphs, tracing, static instrumentation, and dynamic instrumentation.
- Learn the role of methodologies and the Linux 60-second checklist.

### 1.1 Systems Performance
System Performance is the study of the entire computer system, which includes all major software and hardware. As well as anything in the Data path (storage devices, application software) is included as well because it all effects performance.

**Diagram your environment...it helps identify bottlenecks in the infrastructure**

<b><i>fullstack</i></b> when speaking of systems performance means the entire software stack from the application down to metal, including system libraries, the kernel, and the hardware itself.

### 1.2 Roles
Systems Performance can be research or carried out by a variety of job roles. Engineers or teams can be component specific (database, application, ect...) or teams/Engineers can be put in place to test, monitor and improve performance over the entire scope.

### 1.3 Activities
The following is a list of activities that are also ideal steps in the life cycle of a software project from conception through development to production deployment.

1. Setting performance objectives and performance modeling for a future product.
2. Performance characterization of prototype software and hardware.
3. Performance analysis of in-development products in a test environment.
4. Non-regression testing for new product versions.
5. Benchmarking product releases.
6. Proof-of-concept testing in the target production environment.
7. Performance tuning in production.
8. Monitoring of running production software
9. Performance analysis of production issues.
10. Incident reviews for production issues.
11. Performance tool development to enhance production analysis.

steps `1` to `5` comprise `traditional` production development, regardless of the product intended for internal or external users.

Performance engineering should ideally begin before any hardware is chosen or software is written: the first step should be to set objectives and create a performance model. 

**With each step of the development process it can become progressively harder to fix performance issues that arise due to architectural decisions made earlier**

Cloud computing provides new techniques for proof-of-concept testing (step 6) that encourage skipping the earlier steps (steps 1 to 5). 

1. `Canary testing`: A technique that tests new software on a single instance with a fraction of the production workload.
2. `Blue-Green Deployment`: A technique in which traffic is gradually moved to a new pool of instances while leaving the old pool online as a backup.

These are `safe to fail` options that allow testing of new equipment and software in production without prior environment testing.

### 1.4 Perspectives
Performance roles can be viewed from different perspectives.
Two perspectives are...
1. `Workload analysis`: Commonly employed by Application developers who are responsible for the delivered performance of the workload. 
2. `Resource analysis`: Commonly employed by System Admins who are responsible for the system resources.

### 1.5 Performance is Challenging
Systems performance is challenging because it is subjective, it is complex, there may not be a single root cause, and it often involves multiple issues.

#### 1.5.1 Subjectivity
Tech disciplines tend to be <i>objective</i> A.K.A <i>black or white</i>. A software bug for example tends to be fixed or not fixed, present or absent. 

When it comes to performance however it is often <i>subjective</i>. To make things harder it may not even be clear that there even is an issue to begin with. "bad" performance can be "good" performance to someone else.

#### 1.5.2







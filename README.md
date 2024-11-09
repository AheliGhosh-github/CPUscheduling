
CPU Scheduling Algorithms

This document presents an implementation of several CPU scheduling algorithms using C++. The algorithms featured include First Come First Serve (FCFS), Round Robin (RR), Shortest Process Next (SPN), Shortest Remaining Time (SRT), Highest Response Ratio Next (HRRN), Feedback (FB), and Aging. Below is the table of contents for easy navigation:

Table of Contents
- [CPU Scheduling Algorithms](#cpu-scheduling-algorithms)
- [Algorithms](#algorithms)
- [First Come First Serve (FCFS)](#first-come-first-serve-fcfs)
- [Round Robin with Varying Time Quantum (RR)](#round-robin-with-varying-time-quantum-rr)
- [Shortest Process Next (SPN)](#shortest-process-next-spn)
- [Shortest Remaining Time (SRT)](#shortest-remaining-time-srt)
- [Highest Response Ratio Next (HRRN)](#highest-response-ratio-next-hrrn)
- [Feedback (FB)](#feedback-fb)
- [Feedback with Varying Time Quantum (FBV)](#feedback-with-varying-time-quantum-fbv)
- [Aging](#aging)
- [Installation](#installation)
- [Input Format](#input-format)
- [Contributors](#contributors)

### Algorithms

**First Come First Serve (FCFS)**  
The First Come First Serve (FCFS) algorithm is a straightforward scheduling method where the process that arrives first is executed first. While it is easy to comprehend, it can result in inefficient performance, especially when long processes are involved. FCFS lacks any prioritization mechanism, categorizing it as a non-preemptive algorithm. In this scheduling method, the order of arrival dictates execution, which may lead to longer processes delaying shorter ones. It is predominantly utilized in batch processing systems where the sequence of operations is critical.

**Round Robin with Varying Time Quantum (RR)**  
Round Robin scheduling with variable time quantum employs a time-sharing strategy to allocate CPU time among multiple processes. In this variant, the time slice assigned to each process can vary according to their needs. This flexibility allows shorter tasks to receive smaller time slices while longer tasks may get more substantial allocations. The algorithm operates by maintaining a queue of processes, granting each one a specified quantum to execute on the CPU. Once a process’s time expires, it moves to the back of the queue, allowing the next process in line its turn. This adaptability enhances efficiency by reducing average waiting times and mitigating starvation issues that might arise from longer processes monopolizing CPU time.

**Shortest Process Next (SPN)**  
Shortest Process Next (SPN) is a scheduling strategy that prioritizes processes based on their burst times—the duration required for completion. As a non-preemptive algorithm, once a process begins execution, it continues until it either finishes or enters a waiting state. The algorithm organizes incoming processes into a queue based on their burst times; the shortest one is executed first. New arrivals are added and sorted accordingly, ensuring that the shortest task always takes precedence. This method effectively minimizes average waiting times but can inadvertently block longer tasks, potentially harming overall system performance.

**Shortest Remaining Time (SRT)**  
Shortest Remaining Time Next (SRT) resembles SPN but operates as a preemptive algorithm. This means that an executing process can be interrupted if a new process with a shorter remaining time arrives. The SRT maintains a queue where each process has an assigned burst time upon arrival. The one with the least remaining time is executed first, and new processes are sorted into the queue based on their remaining times. This approach can significantly reduce average waiting times and is particularly useful when burst times are unpredictable, as it allows for adjustments during execution.

**Highest Response Ratio Next (HRRN)**  
The Highest Response Ratio Next (HRRN) scheduling algorithm prioritizes processes based on their response ratios—a calculation involving waiting time and burst time. As a non-preemptive algorithm, once execution begins for a process, it continues until completion or entering a wait state. The response ratio determines execution order; processes with higher ratios are prioritized. New arrivals are queued and sorted according to their response ratios. This method can effectively minimize average waiting times since longer-waiting processes are executed sooner, making it adaptable even when burst times are not predetermined.

**Feedback (FB)**  
The Feedback scheduling algorithm allocates CPU resources according to priority levels using multiple priority queues. Each queue represents different priority tiers; higher-priority processes are executed before lower-priority ones. When new processes arrive, they are placed in the appropriate queue based on their priority level. Upon completion of execution, processes move down to lower-priority queues. This strategy proves advantageous in environments where both short and long-running tasks coexist alongside varying priority levels, ensuring timely execution for high-priority tasks while still allowing lower-priority tasks to be processed eventually.

**Feedback with Varying Time Quantum (FBV)**  
Similar to Feedback but with an added layer of complexity, Feedback with Varying Time Quantum incorporates different time slices for each priority level within its multiple queues. This design enhances efficiency by allocating more CPU time to higher-priority tasks while reducing the time spent on lower-priority ones.

**Aging**  
Xinu is an operating system developed at Purdue University that implements a scheduling invariant where at any given moment, the highest priority process eligible for CPU access is executing—using round-robin scheduling among equal-priority processes. This policy results in high-priority processes consistently running while lower-priority ones may starve due to lack of CPU time when competing with higher-priority candidates.

To combat starvation, an aging scheduler may be employed; during each rescheduling event—such as after a timeout—the scheduler increases the priority of all ready processes by a fixed amount. This mechanism ensures that each ready process can only be overlooked by the scheduler for a limited number of cycles before achieving the highest priority.

When the scheduler operates, it follows these steps:
1. Resetting the current process's priority back to its initially assigned level.
2. Incrementing the priorities of all ready processes—excluding the currently running one—by one.
3. Selecting the highest priority process from all eligible candidates for execution next.

This approach effectively mitigates starvation while maintaining efficient scheduling practices within Xinu's operating environment.


- Note that during each call to the scheduler, the complete ready list has to be traversed.

Installation
1- Clone the repository

2- Install g++ compiler and make
```bash
sudo apt-get install g++ make
```
3- Compile the code using `make` command

4- Run the executable file

Input Format
- Line 1: "trace" or "stats"
- Line 2: a comma-separated list telling which CPU scheduling policies to be analyzed/visualized along with
their parameters, if applicable. Each algorithm is represented by a number as listed in the
introduction section and as shown in the attached testcases.
Round Robin and Aging have a parameter specifying the quantum q to be used. Therefore, a policy
entered as 2-4 means Round Robin with q=4. Also, policy 8-1 means Aging with q=1.
 1. FCFS (First Come First Serve)
 2. RR (Round Robin)
 3. SPN (Shortest Process Next)
 4. SRT (Shortest Remaining Time)
 5. HRRN (Highest Response Ratio Next)
 6. FB-1, (Feedback where all queues have q=1)
 7. FB-2i, (Feedback where q= 2i)
 8. Aging
- Line 3: An integer specifying the last instant to be used in your simulation and to be shown on the timeline.
- Line 4: An integer specifying the number of processes to be simulated.
- Line 5: Start of description of processes. Each process is to be described on a separate line. For algorithms 1 through 7, each process is described using a comma-separated list specifying:

    1- String specifying a process name\
    2- Arrival Time\
    3- Service Time

- Note: For Aging algorithm (algorithm 8), each process is described using a comma-separated list specifying:

    1- String specifying a process name\
    2- Arrival Time\
    3- Priority
- Processes are assumed to be sorted based on the arrival time. If two processes have the same arrival time, then the one with the lower priority is assumed to arrive first.
I have provided the test cases as well.
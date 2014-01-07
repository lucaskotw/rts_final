System Synthesis
================

- Graph-Based Model

   - Communication graph

      - A digraph with vertices and edge weights

      - Computation Time

         - the sum of the weights of the verices of C (C, r, d, p)

      - A task graph C is said being executed in the interval [t_1, t_2]
        if there is a multiset of functional-element (vertices) executions
        in [t_1, t_2], which is consistent with the partial ordering C

      - process-based language (a programming model)

         - Process declaration::

            Process <Name>

               activated by (<signal>|Timer)

               <body>

            End

         - Synchronization constraints::

            Rendezvous <Process>

         - Mutual Exclusion Constraints::
         
            Rendezvous <Monitor>

         - Monitor::

            Monitor <Name>

               <Body>

            End

- Decomposition Strategies

   - CTC (Critical Timing Constraints)

      - Have a process for each timing constraint

      - # of time Constraints = # of process

   - CCC (Centralizing Concurrency Control)

      Minimizing Inter-Process Communication

      - Partition the computation required by the timing constraints
        into sets such that

         1. Only *compatible* timing constraints are assigned to the same set,

         2. Only timing constraints are share some of the function calls are
            assigned to the sae set

      - The computation in each set is assigned to a periodic process whose period
        attribute is set to the *GCD* of the periods in the set

      - Strength

         - eliminate redundant computations

      - dangerous to give app with schduling authority

   - DCC

      Partition the require computation into as many processes as possible so as to
      maximize the parallelism

   - Comparison

      +-----------------------------+--------------+---------------+---------------+
      |                             | By Timing    | By Minimizing | By Maximizing |
      |                             | Constraints  | Communication | Parallellism  |
      +-----------------------------+--------------+---------------+---------------+
      | Processor Speed Requirement | Higher       | [#]_          | Lower         |
      +-----------------------------+--------------+---------------+---------------+
      | Communication Bandwidth     |              | Lower         | Higher        |
      | Requirement                 |              |               |               |
      +-----------------------------+--------------+---------------+---------------+
      | Ease of Understanding       | Good         | Poor          |               |
      +-----------------------------+--------------+---------------+---------------+
      | Ease of Modification        |              | Poor          | [#2]_         |
      +-----------------------------+--------------+---------------+---------------+
      .. [#] Less locking problems and more efficient utilzation of the processor power.
      .. [#] Additional timing constraint may not involve any change in program, but it
         may require more difficult analysis (throw complexity to the OS)

- Another Way to Meet Timing Constriants

   - Latency Scheduling

      - execution trace

         a processor is a mapping from non-negative integers to the set of the nodes in a 
         communication graph F plus a null symbol such that::

            F(i) = u if u is executed in the time internal [i, i+1]

      - latency if K time units (the Figure!)

         execution trace has, w.r.t a timing constraint (c, p, d) iff F contains an execution
         of C in any time interval of length >= K

      - Complexity::

         NP-Hard

      - A static schedule L is feasible w.r.t a set of synchronous timing constraints T_a iff
        L has a latency of d time units w.r.t every timing contraint (c, p, d) \in T_a

Efficient On-Line Schedulability Tests and Configuration Selection
==================================================================

- Motivation

   - Load Shedding

   - Relax timing constraint

   - Load Scaling

      - harmonically related

- Configuration Selection

   - Configuration Selection Problem (easier n^m)
   
      - Given a set of configuration, choose a schedulable configuration

   - Period Assignment Problem (harder n*m)
   
      - Given a set of adpative processes, choose a schedulable configuration

         - issue of adaptive processes?
  
- Schedulability Test for the Liu&Layland Model

   - Need for

      - Exploit harmonic relationship of task periods

      - on-line implementation

      - relax heavy CPU utilization

   - Need of Schedulability Tests

      - Performance Guarantee

      - Resource Reservation

      - Open System Architecture

   - Definition

      - Offspring Set

         - self, child, grandchild, ...

      - RS-representative

         - a process \tau that has the highest period within the set and the
           utilization factor equal to the sum of the elements ones

      - Reduced Set

         - a set that RS-representative stands for

      - Division Graph

         - represent the divisibility relation among a set of real numbers

      - Fundamental Frequency

         - the minimum number that the division graph can be decomposed
           into vertex-disjoint linear paths

      - Minimum Linear Covering

         - to find the smallest K such that the vertices of G are partitioned
           into K vertex-disjoint linear paths

   - Lemma 1

      - okay to merge a offspring set to minimize the scheduling test
        procedure

      - intuitively choose root

   - Theorem 2

      - Merge multiple offspring set

- Schedulability Test for the Multiframe Model

   - Goal

      Extend reduced-set-based to multiframe model

   - Intention

      - varying timing constraints

      - skipping of process executions in consecutive periods

   - Definition

      - Multiframe process

         - \tau = (\Sigma_i, p_i), where \Sigma_i is an array of N_i execution times
           (c^0_i, c^1_i,...c^(N_i-1)_i) for some N_i >= 1

      - Peak Execution

         - max (c^0_i, c^1_i,...c^(N_i-1)_i), usually c^0_i

         - (c^0_i, c^1_i,...c^(N_i-1)_i) is in non-increasing order

      - AM (Accumalative Monotonic)

         - the sum will be non-increasing order

      - Critical Instance

         the begining of the period when its peak execution time is requested simultaneously
         with the peak execution times of all higher priority processes

      - RS-Representative ( the figure! )

         - \tau, which

         - N = LCM(N_i)

         - p_i | p, p = max(p_i)

         - C = sum

      - Reduced set

         - set that \tau represent

      - The RS-representative is an AM multiframe periodic process
        (of multiframe periodic process)

      - Peak Utilization Factor

         - sum( c^0_i / p_i )

   - Theorem 6

      - schedulable as its critical instance
         
- Performance Evaluation

   - Guarantee Ratio
   
      (# of guarantee schedulable process sets) / (# of process sets)

- Conclusion

   - Summary
      
      - on-line schedulability tests

      - relax heavy CPU utilization

   - Future Search

      - soft and firm real-time process sets


Storage Systems
===============

- Real-Time Disk Scheduling

   - Strategies

      - FCFS

      - EDF

      - Scan (elevator)

         - variation

            - classify requests into classes

      - C-Scan (Circle Scan)

      - Shortest-seek-time-first (SSTF)

      - weighted scheduling

   - File Allocation Methods

      - Contiguous Allocation, Linked Allocation, Indexed Allocation

   - Handling of Bad Blocks

      - Sector Sparing of Forwarding

      - Sector Slipping

- Flash-Memory Storage Systems

   - Introduction

      - Diversified Application Domains

      - SoC and Hybrid Devices

      - Technology Trend over the Market

         - Improved density

         - Degraded reliability

         - Degraded performance

         - Worsened access constraints

      - SLC

         - Speed

         - Endurance

         - Reliability

      - MLC

         - Lower Cost

         - Higher Density

   - Management Issues

      - SLC constraints

         - Write-Once

         - Bulk-Erasing

         - Wear-Leveling

      - Additional MLC constraints

         - Prohibition of partial page programming

         - Serial Page programming in a block

         - Coming 3D access constraints

      - Policies

         - FTL

            large address translation table lie in main memory

         - NFTL (NAND)

            (Type 2) with replacement block <- sequential

   - Performance vs Overheads

         +------------------------------+-------+-------+---------------------------+
         |                              |  FTL  | NFTL  | AFTL                      |
         +------------------------------+-------+-------+---------------------------+
         | Memory Space Requirements    | Large | Small | A little larger than NFTL |
         +------------------------------+-------+-------+---------------------------+
         | Address Translation Time     | Short | Long  | Much better than NFTL     |
         +------------------------------+-------+-------+---------------------------+
         | Garbage Collection Overhead  | Less  | More  | Much Better than NFTL     |
         +------------------------------+-------+-------+---------------------------+
         | Space Utilization            | High  | Low   | Much Better than NFTL     |
         +------------------------------+-------+-------+---------------------------+
         AFTL moves the mapping information of the replacement block to the
         fine-grained hash table by adding fine-grained slots

         +----------------------------+
         | A Fine-Grain Hash Table    |
         +----------------------------+
         | (Page Name, RPBA + offset) |
         +----------------------------+

         +----------------------------+
         | A Coarse-Grain Hash Table  |
         +----------------------------+
         | (VBA, PPBA, RPBA)          |
         +----------------------------+

      - *MFS* controls the `Maximimum number of Fine-grained Slots`

      - *ST* controls the `frequency of switched between the two address translation mechanisms`

        - n/**ST**

         - Larger ST, Less Switch

      - AFTL is proposed to

         - exploit the advantages of fine-grained/coarse-grained address traslation mechanisms

         - switch dynamically and adaptively the mapping information between the two address traslation mechanisms

   - Reliability Enhancement

      - Over-Erasing Problems

         - Fast Erasing Bits

      - Read/Program Disturb Problems

         - DC Erasing of a programmed cell

            - Electrons might be tunneled from floating gate to control gate through interpoly oxide in all the
              programmed cells

         - drain disturb

            - Electrons are tunneld from the floating get through gate oxide to the frain

               - E.g. Programming Cell B also Erases programmed Cell D
                 
      - Data Retention Problems

         - Electrons stored in a floating gate might be lost such that the the lost of electrons will sonner
           or later affects the charging status of the gate

      - Observations

         - The write throughput drops significantly after garbage collection starts

         - The capacity of flash-memory storage systems increases very quickly such that memory space
           requirements grows quickly

      - Wear leveling

         - In-Place-Updates

            - Rewriting on the Same Page

         - Dynamic Wear Leveling

            - Rewriting over Another Free Page with erasing over blocks with Dead Pages

         - Static Wear Leveling

            - Rewriting over Another Free Page with erasing over any blocks

            - Use a counter for each block

            - The garbage collector always finds the block with the least erase count

            - Block Erasing Table (bit flags)

      - Key Issues and Technologies

         - Address Translation

         - Garbage Collection and Wear Leveling

         - Parallelism in Access

         - Identification of Hot and Cold Data

         - Downgrading Designs

      - Challenges

         - Low Endurance

         - High Bit Error Rate

         - Bad Data Retention

         - Serious Disturbing

   - Challenges and Key Research Issues

      - PCM

         - bucket and array-based strategies

            - Throwing olde pages far away so that they are less likely to be used soon

   - Conclusion

Introduction to Real-Time Databases
===================================

Real-Time Task Synchronization: Timing versus Concurrency
=========================================================

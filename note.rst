System Synthesis
================
- Decomposition Strategies
   - CTC
   - CCC
   - DCC

Efficient On-Line Schedulability Tests and Configuration Selection
==================================================================

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

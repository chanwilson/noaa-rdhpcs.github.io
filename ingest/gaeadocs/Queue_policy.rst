Overview
========

Below is the strategy for the queue structure on Gaea. The original
queue policy was outlined at a meeting on July 9, 2010. It was then
approved approved through NOAA's HPC Integrated Management Team. Changes
and fine-tuning to the queue structure can be done on a weekly basis
through the Configuration Management process.

Note: the *Persistent* queue has had its priority boost removed. Users
should not use the *Persistent* queue any longer, but it still exists in
case users' workflows still refer to it.

The following are the guidelines that was put in place. The details for
implementation were left up to Frank Indiviglio and ORNL.

-  Some overall points

   -  The queuing system should allow groups/projects to spend their
      allocation each month.
   -  The contest between keeping persistent jobs in the system and
      running very large jobs suggests that in general there should be a
      limit on the number of cores a job may use, but with a capability
      to make exceptions for “novel” jobs that may require up to the
      entire system.

      -  This will promote consideration of whether a job requires a
         large number of cores due to, for example, memory or schedule
         constraints, or whether it is simply desired.

-  There should exist queues with different priority levels usable by
   the scheduling algorithm.

   -  At the very least, run-time variability would need to be assessed
      before we could even think of implementing this.

-  Recommendations

   -  Use a fair-share algorithm that can throttle scheduling priority
      by comparing how much of a particular allocation has been used at
      a given time with how much should have been used, assuming
      constant proportional usage. This will promote steady usage
      throughout the month.
   -  Use two separate allocations, renewed monthly, with multiple
      queues drawing down each of them:

      -  50% of the available time for **high-priority** persistent and
         urgent work, that should minimize queue wait time. Queues are:

         -  *Persistent*, for job streams that are intended to stay in
            the system for “long” periods of time with virtually no wait
            time when new job segments are submitted.
         -  *Urgent*, for schedule-driven work needing to be completed
            ASAP.
         -  *Novel*, for jobs that have unusual resource requirements,
            typically needing more than 25% of the system’s cores. These
            can be run during an 8-hour period immediately after
            Preventative Maintenance is complete, since no other jobs
            will be running at that time.

      -  50% for all other \**normal-priority*\* allocated work. Queues
         would be:

         -  *Batch*, for regular allocated jobs
         -  *Debugging/Interactive* work

      -  A *windfall* quality of service (QOS) tagis for work that will
         not be charged against an allocation. As of Jan. 15, 2013,
         windfall can only be specified with -l qos=windfall.

::

   &gt; msub -l qos=windfall scriptName

or in your job script:

::

   #PBS -lqos=windfall

-  Priorities between queues:

   -  Normally, *Persistent* and *Urgent* queues will have the highest
      priority, but remain subject to the fair-share algorithm. This
      will discourage groups from hoarding high-priority time for the
      end of the month.
   -  Within a group/project, jobs in the *Urgent* queue are higher
      priority than jobs in the *Persistent* queue, with each group
      expected to manage the intra-group mix per their allocation.
   -  Between groups/projects, jobs in the *Persistent* and *Urgent*
      queue are the same priority.
   -  At any given time, the suite of jobs drawn from the *Persistent*
      and *Urgent* queues and running on the system should use about 50%
      of the available cores (per the fair-share algorithm), but that
      suite is permitted to use more than 50% as needed (with the
      implication that less than 50% will be used at other times of the
      month).

-  Limit the largest job to 25% of the available cores except in the
   Novel queue.
-  Limit time requested for individual job segments to 12 hours.
-  Interactive/debugging jobs have a tiered limit:

   -  < or = 72 cores (3 nodes) 12 hour limit
   -  < or = 504 cores (21 nodes) 6 hour limit
   -  can't go over 504
   -  (These limits supersede the previous intent to limit
      interactive/debugging jobs to 2 node-days or 1152 core-hours.).

-  Partitions
-  Users are encouraged to add the following to their job submissions
   and/or job script -l partition=c3

::

   &gt;msub -l partition=c3 /path/to/job/script

or in your job script:

::

   #PBS -l partition=c3

.. _debug_batch_queues:

Debug & Batch Queues
====================

-  **Interactive / Debug**

   -  Interactive/Debug

      -  **Interactive queue job time limits**

         -  24-72 processors = 12 hours
         -  96-504 processors = 6 hours
         -  Over 528 processors = 4 hours

-  **Debug queue job time limits**

   -  1 hour

-  **Batch** - Default queue for all compute partitions.

-  **Novel** - jobs larger than 18015 on c3 and 18432 on c4 will be
   shunted to the novel queue. The novel queue does not run until after
   a periodic maintenance in order to prevent large amounts of the
   system being idled as jobs complete naturally to make room for the
   novel jobs.

.. _priority_queues:

Priority Queues
===============

Priority queues are allocated one per group, and allow for a single
eligible job per user. These only work for compute partitions (c3 & c4).
They do not work on the es partition (eslogin, ldtn, and rdtn queues).

-  **Persistent** - The persistent queue was for workstreams that need
   to run at a consistent rate on the partition. The persistent queue
   currently holds the same weight as the batch queue, so no priority
   boost.
-  **Urgent** - The urgent queue is for work of the highest priority and
   holds the highest weight. It is for schedule-driven work needed to be
   completed ASAP.

.. _queues_per_partition:

Queues per Partition
====================

-  es

   -  eslogn (compiling)
   -  ldtn (combining model output, other postprocessing)
   -  rdtn (data transfers to/from non-Gaea resources)

-  c3 and c4 (compute)

   -  batch
   -  interactive
   -  debug (1 hour limit)
   -  persistent
   -  urgent
   -  novel (large jobs - >18015 cores on c3 and >18432 on c4)

.. _schedulerpriority_specifics:

Scheduler/Priority Specifics
============================

NOTE: An increase in large job priority is being tested for 1 week
starting 11:20am 1/9/13. Please see Frank Indiviglio for questions. This
was discussed in the User Meeting on 1/7.

+----------------+----------------+----------------+----------------+
| \**Factor \*\* | \**Unit of     | \**Actual      | **Value**      |
|                | Weight \*\*    | Weight         |                |
|                |                | (Minutes) \*\* |                |
+================+================+================+================+
| Class          | # of days      | 1440           | | Urgent (10)  |
|                |                |                | | Persistent   |
|                |                |                |   (1)          |
|                |                |                | | Deb          |
|                |                |                | ug/Interactive |
|                |                |                |   (2)          |
|                |                |                | | Batch (1)    |
|                |                |                | | Windfall     |
|                |                |                |   (-365)       |
+----------------+----------------+----------------+----------------+
| Account        | # of days      | 1440           | | Allocated    |
| Priority       |                |                |   Project (1)  |
|                |                |                | | No           |
|                |                |                |   Allocation   |
|                |                |                |   (Staff)      |
|                |                |                |   (-365)       |
|                |                |                | | No Hours     |
|                |                |                |   (-365)       |
+----------------+----------------+----------------+----------------+
| Fairshare      | # of minutes   | 1              | | (<>)5% user  |
|                |                |                |   (+/-) 30     |
|                |                |                |   minutes      |
|                |                |                | | (<>)5% class |
|                |                |                |   (+/-) 60     |
|                |                |                |   minutes      |
+----------------+----------------+----------------+----------------+
| Queue Time     | 1 Minute       | 1              | Provided by    |
|                |                |                | Moab           |
+----------------+----------------+----------------+----------------+

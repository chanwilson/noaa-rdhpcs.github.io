Introduction
============

Gaea is the largest of four NOAA research and development HPC systems.
Gaea is composed of two primary compute partitions hosted by DOE/ORNL.

.. figure:: gaea.jpg
   :alt: gaea.jpg

The Gaea System:

-  consists of 143,936 Intel cores.
-  contains 38 petabytes of memory and manufacturer Cray’s resilient
   Aries interconnect.
-  can perform more than 5.29 petaflops, or 5,290 trillion calculations
   each second.

Status information can also be found using SLURM commands. See: `Slurm
tips <Slurm_tips>`__.

.. _current_hardware:

Current Hardware
================

=========================== ===========================
C3                          C4
=========================== ===========================
| **​1.77 Petaflops**        | **3 Petaflops**
| \* 47,552 Cores           | \* 54,144 Cores
                            
-  32 cores per node        -  36 cores per node
-  1486 nodes               -  1504 nodes
-  92.8 TB of memory        -  98 TB of memory
-  Intel Haswell Processors -  Intel Haswell Processors
=========================== ===========================

.. table:: es partition

   +------------------------+------------------------+------------------+
   | **rdtn queue -- remote | **ltdn queue -- local  | **login nodes**  |
   | data transfer nodes**  | data transfer**        |                  |
   +------------------------+------------------------+------------------+
   | -  8 nodes (rdtn01-08) | -  16 nodes (ldtn1-16) | -  8 total       |
   | -  8 slots per node    | -  8 cores/node        | -  24 cores      |
   | -  64 total slots      | -  128 cores           | -  256 GB memory |
   +------------------------+------------------------+------------------+

-  RDTNS - to/from gaea to the outside world
-  LDTNS - I/O intensive operations
-  8 login nodes (gaea9-16) used for compiling
-  2 File Systems

   -  33PB f2 fast scratch filesystem
   -  NFS home file system

-  Connectivity @ 2x10Gb/s to NOAA N-Wave research network

Users can request the system in increments of 32 cores for c3 and 36
cores for c4. Please specify a single partition for your job, as c3 and
c4 have different node sizes

.. _system_architecture:

System Architecture
===================

.. _node_types:

Node types:
-----------

**Compute Nodes (C3)** *32 cores, intel hazwell based, 64GB memory, run
model executable, filesystem mount - F2* **Compute Nodes (C4)** *36
cores, intel broadwell based, 64GB memory, run model executable,
filesystem mount - F2* **Batch Nodes** *2 cores, 8GB memory, run scripts
only (cores are not charged, Note: Batch Nodes are not very powerful. Do
not write code/jobs that will use Batch nodes to do CPU intensive work)*
**ESLogin Nodes** *32 cores, 512GB memory, run interactive sessions,
Matlab, compiles* **LDTN Nodes** *16 cores, 24GB memory, I/O intensive
jobs (combines, etc.)* **RDTN Nodes** *8 cores, 48GB memory, Data
transfer jobs*

.. figure:: Gaea2.png
   :alt: Gaea2.png
   :width: 600px

Clusters
========

**C3** Gaea's Haswell based partition **C4** Gaea's larger compute
partition. Please see "System Architecture" and "Hardware" for
differences. **es** login nodes, local data transfer node queue (ldtn)
and remote data transfer node queue (rdtn)

Examples-

::

   sbatch --clusters=c3 scriptname
   #SBATCH --clusters=c4

::

   sbatch --clusters=es scriptname
   #SBATCH --clusters=es

.. _what_is_c3:

What is C3?
-----------

C3 is a Cray XC40 with 47872 Intel Haswell cores and 93.5TB of memory
(2GB/core). It is available from all Gaea login nodes.

To access these login nodes, ssh or sshg3 (Tectia CAC card authenticated
SSH) to the Gaea bastion of your choice (sshg3 gaea.rdhpcs.noaa.gov, ssh
gaea-rsa.princeton.rdhpcs.noaa.gov, sshg3 gaea.boulder.rdhpcs.noaa.gov,
or ssh gaea-rsa.boulder.rdhpcs.noaa.gov). If you want a specific Gaea
login node, wait for the list of nodes and press 'ctrl'+'c', then enter
the name of the login node you would like to use and press return. Your
ssh session will be forwarded to that specific node.

You can use C3 in batch or software mode.

.. _batch_system:

Batch System
~~~~~~~~~~~~

From gaea9-15 you can interact with C3's Slurm cluster. See `Slurm
Tips <Slurm_tips>`__ for details.

Your C3 job scripts will usually call srun or srun-multi if you have a
multi-executable model, e.g. a coupled model with different ocean and
atmospheric model executables.

Software
~~~~~~~~

Your shell init scripts (~/.cshrc , ~/.bashrc, etc.) will need access to
important software resident on Gaea. Make sure that your scripts include
the following lines:

::

   module use /sw/eslogin-c3/modulefiles
   module use /usw/eslogin/modulefiles-c3
   module use /sw/xc40/modulefiles
   module use /usw/xc40/modulefiles

**You must recompile your application, and all libraries it links to
must be compiled for C3.**

Remember to use the 'cc' and 'ftn' aliases provided by the PrgEnv
modules to compile statically linked executables for use on the c3 batch
nodes. The default PrgEnv module on c3 is PrgEnv-intel.

.. _site_specific_documentation_for_c3:

Site Specific Documentation for C3
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`GFDL Modeling Systems C3 On-boarding
Guide <http://wiki.gfdl.noaa.gov/index.php/C3_Guide_from_Modeling_Systems>`__

.. _what_is_c4:

What is C4?
-----------

C4 is a Cray XC40 with 95,616 Intel Broadwell cores and 166TB of memory
(1.78GB/core). There are an additional 4 login nodes with 24 cores and
256GB of memory each. The total cores for c4 and its login nodes are
95,712.

.. _accessing_the_c4_login_nodes:

Accessing the C4 login nodes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

C4 is available from all Gaea login nodes. To access these login nodes,
ssh or sshg3 (Tectia CAC card authenticated SSH) to the Gaea bastion of
your choice (sshg3 gaea.rdhpcs.noaa.gov, ssh
gaea-rsa.princeton.rdhpcs.noaa.gov, sshg3 gaea.boulder.rdhpcs.noaa.gov,
or ssh gaea-rsa.boulder.rdhpcs.noaa.gov). If you want a specific Gaea
login node, wait for the list of nodes and press 'ctrl'+'c', then enter
the name of the login node you would like to use and press return. Your
ssh session will be forwarded to that gaea login node.

You can use C4 in batch or software mode.

.. _batch_system_1:

Batch System
^^^^^^^^^^^^

From gaea9-15 you caninteract with c4's Slurm cluster. See `Slurm
Tips <Slurm_tips>`__ for details.

Your C4 job scripts will usually call srun or srun-multi if you have a
multi-executable model e.g. a coupled model with different ocean and
atmospheric model executables.

.. _software_1:

Software
^^^^^^^^

Make sure that your shell init scripts (~/.cshrc and/or ~/.bashrc, etc.)
include some or all of the following lines to allow your jobs access to
important software accessible on Gaea. You may need to rearrange or
remove some of these in order to access the exact builds of software
you're interested in using.

::

   module use /sw/xc40/modulefiles
   module use /usw/xc40/modulefiles
   module use /sw/xc40-c4/modulefiles
   module usw /sw/eslogin-c3/modulefiles
   module use /sw/eslogin-c4/modulefiles
   module use /usw/eslogin/modulefiles-c3
   module use /usw/eslogin/modulefiles-c4

**You must recompile your application and all libraries it links to must
be compiled for C4**

Remember to use the 'cc' and 'ftn' aliases provided by the PrgEnv
modules to compile statically linked executables for use on the c4
compute nodes. The default PrgEnv module on c4 is PrgEnv-intel.

.. _c4_known_issues:

C4 Known Issues
~~~~~~~~~~~~~~~

.. _intel_15_with_openmp_fails_with_segmentation_violations:

Intel 15 with OpenMP fails with segmentation violations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Modeling Systems group has identified a problem with the Intel
version 15 compiler installed on the c4 nodes. Models compiled with
Intel 15 with OpenMP enabled will fail with a segmentation error. ORNL
is aware there is an issue, and is working on a solution.

Workaround: Use the default Intel version 16 compiler (module
intel/16.0.3.210)

.. _gcp_module_not_available_on_c4_nodesgcp_does_not_work_on_c4_nodes:

GCP module not available on C4 nodes/GCP does not work on C4 nodes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The gcp modulefile is not yet available on the C4 nodes. This is due to
GCP is not yet fully configured to run on the C4 login/batch nodes and
software dependencies of GCP not being available on C4 yet. Modeling
Systems has requested the last few software packages to be installed on
the C4 nodes. Since a modulefile for GCP does not exist on the c4 nodes,
FRE generated run scripts will fail as they are unable to load GCP.

Workaround: Add the following to your user shell initialization scripts
(e.g. ~/.cshrc, ~/.bashrc) and/or job scripts:

::

   module use -a /usw/eslogin/modulefiles-c3

If the production workflow requires gcp to be called on the c4 batch
nodes, these calls may need to be commented out, and the files
transferred by those calls should be done manually from a c3 login node.

.. _usw_modules_not_available_on_c4:

/usw modules not available on C4
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In addition to gcp several other modules provisioned via /usw are not
available in the default shell environment on C4. Some of the software
packages in the C3 /usw location need to be recompiled to work on the
newer operating system present on C4.

.. _site_specific_documentation_for_c4:

Site Specific Documentation for C4
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Modeling Systems C4 On-boarding
Guide <http://wiki.gfdl.noaa.gov/index.php/C4_Guide_from_Modeling_Systems%7CGFDL>`__

.. _c4_cpuinfo_and_memory:

C4 cpuinfo and memory
~~~~~~~~~~~~~~~~~~~~~

::

   processor    : 71
   vendor_id    : GenuineIntel
   cpu family    : 6
   model        : 79
   model name    : Intel(R) Xeon(R) CPU E5-2697 v4 @ 2.30GHz
   stepping    : 1
   microcode    : 0xb000021
   cpu MHz        : 2301.000
   cache size    : 46080 KB
   physical id    : 1
   siblings    : 36
   core id        : 27
   cpu cores    : 18
   apicid        : 119
   initial apicid    : 119
   fpu        : yes
   fpu_exception    : yes
   cpuid level    : 20
   wp        : yes
   flags        : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc aperfmperf eagerfpu pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid dca sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch ida arat epb invpcid_single pln pts dtherm intel_pt kaiser tpr_shadow vnmi flexpriority ept vpid fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 erms invpcid rtm cqm rdseed adx smap xsaveopt cqm_llc cqm_occup_llc
   bugs        :
   bogomips    : 4603.23
   clflush size    : 64
   cache_alignment    : 64
   address sizes    : 46 bits physical, 48 bits virtual
   power management:



   &gt; free -g
                total       used       free     shared    buffers     cached
   Mem:            62          3         59          2          0          2
   -/+ buffers/cache:          1         61
   Swap:            0          0          0

Filesystems
===========

Gaea has 2 filesystems: Home and F2, a lustre filesystem. Lustre is a
high performing parallel file system, but has certain limitations. For
example, performance will start to degrade after utilization exceeds 80%
on a file system. As a result managing the quota, using well-formed I/O,
and using the `lustre storage tools <Lustre_tools>`__ (when searching
your files or managing your space) is important. It is suggested that
users research and use lfs (lustre) version of commands on F2. Please
see `F2 Filesystem <F2_filesystem>`__ regarding information to the Gaea
lustre filesystem.

Home
----

The home filesystem is split into two sections which are backed up.
There is a home1 and home2 for load balance purposes. Each user has a
5GB limit.

Home is mounted on:

-  Batch nodes
-  LDTN
-  Login nodes (all)
-  RDTN

A nightly snapshot can be accessed at
/ncrc/home1|2/.snapshot/nightly.0/$USER

You can use this path to restore any files or sub-directories that are
contained within that directory from last night. Use nightly.1 for files
from 2 nights ago. All files and sub-directories contained there will
carry the same permissions as the originals. Users can simply copy from
that location to any destination.

Restores from tape are performed on a best-effect basis, typically the
next business day.

.. _lustre_filesystems_f2:

Lustre Filesystems (F2)
-----------------------

F2 is a 33PB Lustre filesystem. User directories are available at
/lustre/f2/scratch/$USER/ and /lustre/f2/dev/$USER. NCEP users'
directories are found in /lustre/f2/scratch/ncep/$USER and
/lustre/f2/dev/ncep/$USER. All files over 2 weeks old will be scrubbed
within the /lustre/f2/scratch/$USER/ and /lustre/f2/scratch/ncep/$USER
directories. Directories under /lustre/f2/dev are not swept. Files that
have not been accessed or used within 2 weeks will be scrubbed.

F2 is NOT backed up. Users are responsible for monitoring their files
and transferring what they do not want to lose to a location without a
scrubbing policy and with data back-ups. Please ensure data you need to
keep is copied to your archive.

Information on usage of F2 as related to your center, group, allocation
account allocation as a percentage of the available storage on F2 will
be able to be obtained from f1rpt, documented at the following link:
f1rpt

F2 is mounted:

-  C3 (batch and compute nodes)
-  C4 (batch and compute nodes)
-  LDTN
-  RDTN
-  Login nodes (all)

The directory /lustre/f2/pdata/ is used to store commonly accessed user
data that falls outside of the scope of ams data

You should have directories in the following locations:

-  /lustre/f2/scratch/$USER (symlinked from
   /lustre/f2/scratch/<YOUR_CENTER>/$USER)
-  /lustere/f2/dev/$USER (symlinked from
   /lustre/f2/dev/<YOUR_CENTER>/$USER)

.. _f2_specs:

F2 Specs
~~~~~~~~

-  Improved I/O performance
-  33 PB of usable storage
-  Automatic lossless compression of files

   -  To check the amount of compression, use du with and without the
      --apparent-size argument.

-  Additional metadata capacity

For more information on Lustre tools please reference `Lustre
Filesystems Tools <Lustre_tools>`__ page.

.. _environment_variables_for_f2_locations:

Environment Variables for F2 locations:
---------------------------------------

-  PDATA = /lustre/f2/pdata
-  DEV = /lustre/f2/dev
-  SCRATCH = /lustre/f2/scratch

.. _sweeping_and_other_policy:

Sweeping and other policy:
--------------------------

-  $SCRATCH files are swept at 21 days of inactivity.
-  $DEV files are not swept, but may be in future if $DEV usage is too
   high to support continued operations.
-  $PDATA files are not swept. Pdata is for common input files to reduce
   reliance of production runs on individual users' data. If you would
   like a pdata directory for your group, submit a help desk ticket
   asking for one. Please specify your center and the Unix group the
   directory should belong to.

.. _job_submission:

Job Submission
==============

Please see the following Slurm details.

There are two job types.

-  Batch

   -  Regular jobs - use sbatch

-  Interactive/Debug

   -  salloc --x11 --clusters=c3 --nodes=2 --ntasks-per-node=32

      -  Note: The size is the number of desired cores in increments of
         32 for c3 and 36 for c4.

Queues
======

There are currently 4 different queues.

-  batch - no specification needed
-  eslogin - compiles and data processing jobs
-  ldtn - data movement queue (local)
-  rdtn - data movement (remote)

Examples:

::

   sbatch --clusters=es --partition=eslogin scriptname
   sbatch --clusters=es --partition=ldtn scriptname

.. _job_monitoring:

Job Monitoring
==============

The following are job monitoring commands with examples:

-  squeue - displays the queues. All jobs are commingled

::

   squeue
   squeue -u $USER

scontrol show job - provides job information.

::

   scontrol show job jobid

-  sinfo - system state information

::

   sinfo

-  scontrol - control holds on jobs

::

   scontrol hold jobid
   scontrol release jobid

-  scancel - cancel jobs

::

   scancel jobid

Terminology
===========

Slurm
   The scheduler for all new NOAA research and development systems.
Cluster
   A section of Gaea that has its own scheduler. It is a logical unit in
   Slurm.
Partition
   A group of nodes with a specific purpose. Formerly (under Moab) a
   queue. It is a logical unit in Slurm.
DTN
   data transfer node
CMRS
   Climate Modeling and Research System; an alternate name for Gaea.
MPMD
   MPMD capability will not be supported on Gaea. Users who need MPMD
   functionality can open a help desk ticket. NCEP users should continue
   to filter tickets and requests through Kate.Howard@noaa.gov. Users
   requesting this support via help desk ticket will be given access to
   a Gaea application analysis who will assist them.

Environment
===========

Gaea is implemented to use the Environment Modules system. This tool
helps users manage their Unix or Linux shell environment. It allows
groups of related environment-variable settings to be made or removed
dynamically. Modules provides commands to dynamically load, remove and
view software.

More information on using modules is available at `Gaea
Modules <Modules>`__.

.. _dos_and_donts:

Do's and Don'ts
===============

Do
--

-  Compile on login nodes
-  Copy data back to archive location (off gaea) using RDTN's
-  Put source files and commonly used files in /lustre/f2/dev/$user
-  Put transient data in /lustre/f2/scratch/$user
-  Use gcp for transfers
-  Use lfs (lustre) version of commands on the F2 lustre filesystem

   -  `lfs
      manual <http://www.google.com/url?q=http://wiki.lustre.org/manual/LustreManual20_HTML/UserUtilities_HTML.html&sa=D&sntz=1&usg=AFrqEzeDu0zi9R_i9kGCe5kikkgwcO9cUQ>`__

Don't
-----

Don't use the following on Gaea:

-  combines on batch (they will be killed)
-  combines on compute nodes
-  compile on batch
-  cp
-  cron jobs (not permitted)
-  deep large scale use of "find" on the F2 lustre filesystem (please
   use 'lfs find' instead)
-  fs as permanent storage
-  module purge
-  recursive operations like ls -R
-  run applications natively
-  transfers on batch nodes
-  unalias\*

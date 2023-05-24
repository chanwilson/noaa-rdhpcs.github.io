Please be aware that Gaea is not like a usual Slurm cluster. Slurm
expects that all nodes are homogeneous and capable of being used for any
purpose. Gaea is a heterogeneous set of clusters (hence the need to
specify a cluster as shown below.) This also means that partitions
(queues) for resources with different purposes will need to set up your
job's environment to provide access to the software for that
purpose.(data transfer nodes being chief among these.) Under Slurm your
job will only have the system shell init scripts run if you specify
--export=NONE. The result is that --export=NONE is a required argument
to get your job to see software specific to a given node type, e.g.
HSI/HTAR for HPSS on the data transfer nodes.

For general information about SLURM, see `Introduction to
SLURM <https://rdhpcs-common-docs.rdhpcs.noaa.gov/wiki/index.php/Introduction_to_SLURM>`__
and subsequent topics in the Commondocs pages.

.. _to_find_the_accounts_to_which_you_belong:

To find the accounts to which you belong
========================================

sacctmgr show assoc where user=$USER
format=cluster,partition,account,user%20,qos%60

.. _to_c3:

To c3:
------

sbatch --clusters=c3 --nodes=1 --account=gfdl_z --qos=normal
--export=NONE /path/to/job/script

.. _to_c3_but_urgent:

To c3, but urgent
~~~~~~~~~~~~~~~~~

sbatch --clusters=c3 --nodes=1 --account=gfdl_z --qos=urgent
--export=NONE /path/to/job/script

.. _to_c4:

To c4:
------

sbatch --clusters=c4 --nodes=1 --account=gfdl_z --qos=normal
--export=NONE /path/to/job/script

.. _to_the_ldtns:

To the LDTNs:
-------------

sbatch --clusters=es --partition=ldtn --nodes=1 --ntasks-per-node=1
--account=gfdl_z --qos=normal --export=NONE /path/to/job/script

.. _to_the_rdtns:

To the RDTNs:
-------------

sbatch --clusters=es --partition=rdtn --nodes=1 --ntasks-per-node=1
--account=gfdl_z --qos=normal --export=NONE /path/to/job/script

.. _to_submit_interactive_work_to_c3:

To submit interactive work to c3:
---------------------------------

salloc --clusters=c3 --qos=interactive --nodes=1 --x11

If you’re using x2go the X forwarding won’t work without the following
workaround: gsissh -XY to another gaea login node and then run salloc.

.. _running_your_models:

Running your models:
--------------------

In your c3 job scripts or interactive sessions you will want to run your
model executable. If your model is simple (single component, etc) then
use srun. If it is a coupled model or otherwise has multiple execution
contexts and/or executables, you will need to use srun-multi.

srun ./executable

srun-multi --ntasks=1 --cpus-per-task=32 ./executable : --ntasks 128
--cpus-per-task=1 ./executable

Note:
-----

We are working an issue where modulecmd is not initialized in all
shells. If you find that modulecmd is missing, add the following to your
job script:

source /opt/modules/default/init/<your_job_script_shell_type>

.. _monitoring_your_jobs:

Monitoring your jobs:
=====================

.. _shell_setup:

Shell Setup
-----------

Do not set these in jobs/shells you intend to submit work from as they
will override your job submission script #SBATCH directives, causing
warnings and errors. Use them in shells you intend to monitor jobs from.

.. _in_tcsh:

In [t]csh:
~~~~~~~~~~

setenv SLURM_CLUSTERS t4,c3,c4,gfdl,es

.. _in_bash:

In bash:
~~~~~~~~

export SLURM_CLUSTERS=t4,c3,c4,gfdl,es

.. _jobs_in_the_queue:

Jobs in the queue:
------------------

squeue -a

.. _completed_jobs:

Completed Jobs:
---------------

Slurm does not keep completed jobs in squeue.

sacct -S 2019-03-01 -E now -a

If you don’t specify -S and -E options sacct gives you data from today.

.. _getting_details_about_a_job:

Getting details about a job:
----------------------------

Slurm only keeps information about completed jobs available via scontrol
for 5 minutes after completion. After that time, sacct is the currently
available way of getting information about completed jobs.

scontrol show job --clusters=es 5978

.. _fair_share_reporting:

Fair Share Reporting:
=====================

.. _summary_of_all_accounts:

Summary of all accounts
-----------------------

sshare

.. _summary_of_one_account:

Summary of one account
----------------------

sshare -A aoml

.. _details_by_user_of_one_account:

Details by user of one account
------------------------------

sshare -a -A gefs

.. _details_by_user_of_all_accounts:

Details by user of all accounts
-------------------------------

sshare -a

.. _priority_analysis_of_your_job:

Priority Analysis of Your Job:
==============================

sprio
-----

sprio -j 12345

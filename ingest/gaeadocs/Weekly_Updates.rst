.. raw:: html

   <h1>

Thursday, May 11, 2023

.. raw:: html

   </h1>

.. raw:: html

   <h2>

Announcements

.. raw:: html

   </h2>

.. raw:: html

   <h3>

New Filesystem — June-August 2023

.. raw:: html

   </h3>

ORNL is in the process of procuring a new file system for the Gaea
complex. This new file system will be used for the C5 cluster. Once this
new file system is in place, the F2 file system will no longer be
mounted read-only on C5. Migration between the two file systems will
need to be completed using the data transfer nodes (DTN).

To allow space for the new file system, the C3 cluster will be
decommissioned early. We are working with ORNL on the exact time. We
will let the user community know when we have an approximate date.

.. raw:: html

   <h3>

C5 in Production

.. raw:: html

   </h3>

This is a reminder that the C5 cluster is now in production, and
available to all users. Current usage on C5 is low, and some users may
find job throughput higher during this time.

.. raw:: html

   <h2>

Current Issues and Outages

.. raw:: html

   </h2>

.. raw:: html

   <h3>

C4 Job Failure — 10 May 2023

.. raw:: html

   </h3>

Yesterday, we received several reports of C4 jobs failing early with a
message indicating the ``MODULESHOME`` environment variable is not set.
ORNL is aware of the issue and is looking for the cause and a
resolution. The initial thought is this is tied to jobs submitted from
login nodes that had a module issue that appeared while pushing the
software update to the remainder of the Gaea C3/C4 login nodes
(gaea10-gaea15). It is possible that resubmitting the failed jobs will
resolve the issue. ORNL rebooted all the updated login nodes. We ask
users to resubmit the failed jobs, and to let the help desk know of any
continued failures. ORNL will continue to investigate to determine the
cause, and if any further actions are needed.

.. raw:: html

   <h3>

C3 Software Update — 08-12 May 2023

.. raw:: html

   </h3>

The C3 cluster is under maintenance, and is in the process of receiving
the same software update applied to C4 in April. After C3 is back in
production, all C3/C4 login nodes gaea10-gaea15 will have the same
updated image. While we strongly suggest using the updated login nodes
for new executables, the old image will remain on gaea9 to allow
compilation using the old image. Interactive logins on gaea9 is disabled
for all users. Users must submit a batch job to gaea9 to access the old
image. Use the ``--nodelist=gaea9`` ``sbatch`` option to submit jobs to
the gaea9 node.

::

   sbatch --cluster=es --partition=eslogin --nodelist=gaea9 --nodes=1 --export=NONE ...

Because of the software differences, we strong suggest not using an
interactive session to build on gaea9.

.. raw:: html

   <h2>

Upcoming Outages

.. raw:: html

   </h2>

None at this time.

.. raw:: html

   <h1>

Tuesday, April 19, 2023 — Updated April 20, 2023

.. raw:: html

   </h1>

.. raw:: html

   <h2>

Current Issues and Outages

.. raw:: html

   </h2>

.. raw:: html

   <h3>

C4 update complete

.. raw:: html

   </h3>

ORNL has completed the software and programming software update on C4.
As previously mentioned, the programming environment on C4 is different
than what is currently on C3. Users will need to ensure any existing run
scripts for C4 are updated. Other than what modules and versions are
available on this updated environment, C4 now uses LMOD. The switch to
LMOD has the same caveats that were previous mentioned C5. (See the `MSD
C5 Onboarding
Guide <https://docs.google.com/document/d/12tVJrDMon9tvvM1F-A5wn7oVHGxqRVWFzRcgctAkODQ>`__.)

At this time, the only gaea13 is configured with the new image. Please
use that node to compile new executables for C4. Over the next weeks,
gaea14 and gaea15 will be migrated to the new image.

At this time MSD has identified items that affect FRE users. MSD and the
FRE development team will send an additional email with details and
instructions.

Please submit HD tickets for newly discovered issues.

.. raw:: html

   <h2>

Past Outages

.. raw:: html

   </h2>

.. raw:: html

   <h3>

C4 Software Update — 19-24 April

.. raw:: html

   </h3>

ORNL updated the software on C4 to the last vendor-supported version for
the C4 hardware. This is the same update ORNL attempted during the March
outage.

.. raw:: html

   <h1>

Tuesday, April 19, 2023 — Updated April 20, 2023

.. raw:: html

   </h1>

.. raw:: html

   <h2>

Current Issues and Outages

.. raw:: html

   </h2>

.. raw:: html

   <h3>

C5 in Production

.. raw:: html

   </h3>

The C5 partition has returned from the software update and is now in
production. While C5 was available for use before the downtime, it was
not in production. Now that the system is in production, ORNL has
additional procedures to follow before taking the system down. Those
procedures will now be followed.

The GFDL Modeling System Division (MSD) has made a `C5 Onboarding
Guide <https://docs.google.com/document/d/12tVJrDMon9tvvM1F-A5wn7oVHGxqRVWFzRcgctAkODQ>`__
available with additional help when getting started on C5.

.. raw:: html

   <h3>

C5 module conflict cray-libsci/23.02.1.1 and
intel-{classic,oneapi}/2022.0.2

.. raw:: html

   </h3>

After the software update on C5, we know of a module incompatibility
with the cray-libsci/23.02.1.1 and the two Intel compiler modules
intel-classic/2022.0.2 and intel-oneapi/2022.0.2 modules. With these two
modules loaded the cc, CC, and ftn compiler wrappers will not work, and
you will get an error similar to:

::

   Error:  Unable to find cray-libsci/23.02.1.1 libraries compatible with intel-classic/2022.0.2 targeting 'x86-rome'.

To use intel-classic/2022.0.2 with cray-libsci, you must use the older
cray-libsci/22.10.1.2 module. You can unload that module if you know you
do not need the cray-libsci libraries.

.. raw:: html

   <h3>

F2 Performance – Ongoing

.. raw:: html

   </h3>

F2 performance is still suffering from intermittent performance
degradation. We continue requesting users modify certain usage and
behaviors contributing to performance degradation. These include not
sharing files among multiple job streams, typically using symbolic and
hard links, developing and using SCM (e.g., git) commands, and
installing and using software environments (e.g., conda, spack). Please
get in touch with the Gaea helpdesk if you require assistance.

.. raw:: html

   <h3>

F2 usage at 64% used

.. raw:: html

   </h3>

The current F2 utilization is at 64%. When the usage exceeds 70%, we can
see additional performance degradation. We request users remove data
that is no longer required off F2.

.. raw:: html

   <h3>

General Copy Tool (gcp) issues on C5

.. raw:: html

   </h3>

The GFDL-developed general copy (gcp) is not working from the C5 login
nodes. We are working on a solution. Please use the DTNs or one of the
C3/C4 login nodes (gaea9-gaea15).

.. raw:: html

   <h2>

Upcoming Outages

.. raw:: html

   </h2>

.. raw:: html

   <h3>

C4 Software Update — 19-21 April

.. raw:: html

   </h3>

ORNL will update the software on C4 to the last vendor-supported version
for the C4 hardware. This is the same update ORNL attempted during the
March outage.

.. raw:: html

   <h2>

Past Outages

.. raw:: html

   </h2>

.. raw:: html

   <h3>

ORNL Partial Facility Outage — 18 April

.. raw:: html

   </h3>

ORNL performed facility work requiring portions of the data center to be
without power. This work has been completed.

.. raw:: html

   <h1>

Tuesday, April 04, 2023

.. raw:: html

   </h1>

.. raw:: html

   <h2>

Current Issues and Outages

.. raw:: html

   </h2>

.. raw:: html

   <h3>

C5 Outage

.. raw:: html

   </h3>

ORNL is performing work on C5 to update the management system's
software. At this time, ORNL has not needed to stop running jobs on C5.
However, it is possible this work is causing more jobs to fail on C5.
Please continue to report job failures so we can identify the cause.

Later this week, possibly as early as Wednesday afternoon, ORNL will
need to stop running jobs. Jobs currently running, if requeable, should
be requeued.

.. raw:: html

   <h3>

F2 Performance – Ongoing

.. raw:: html

   </h3>

F2 performance is still suffering from intermittent performance
degradation. We continue requesting users modify certain usage and
behaviors contributing to performance degradation. These include not
sharing files among multiple job streams, typically using symbolic and
hard links, developing and using SCM (e.g., git) commands, and
installing and using software environments (e.g., conda, spack). Please
get in touch with the Gaea helpdesk if you require assistance.

.. raw:: html

   <h2>

Upcoming Outages

.. raw:: html

   </h2>

.. raw:: html

   <h3>

C4 Software Update — 18-21 April (Tentative)

.. raw:: html

   </h3>

ORNL will update the software on C4 to the last vendor-supported version
for the C4 hardware. This is the same update ORNL attempted during the
March outage.

.. raw:: html

   <h3>

ORNL Partial Facility Outage — 18 April

.. raw:: html

   </h3>

ORNL will perform facility work that will require portions of the data
center to be without power. Gaea is in the area that will be without
power. ORNL will power down the Gaea complex prior to the facility work.

.. raw:: html

   <h1>

Monday, March 20, 2023

.. raw:: html

   </h1>

.. raw:: html

   <h2>

Current Issues

.. raw:: html

   </h2>

.. raw:: html

   <h3>

C4 Outage

.. raw:: html

   </h3>

C4 will be down for the scheduled software update this week. This will
place C4 on the latest supported OS and support software on the C4
hardware. As previously announced, C3 will receive the same OS and
software in April.

.. raw:: html

   <h3>

F2 Performance – Ongoing

.. raw:: html

   </h3>

F2 performance is still suffering from intermittent performance
degradation. We continue to request users modify certain usage and
behaviors that contribute to performance degradation. These include not
sharing files among multiple job streams, typically using symbolic and
hard links, developing and using SCM (e.g., git) commands, and
installing and using software environments (e.g., conda, spack). Please
get in touch with the Gaea helpdesk if you require assistance.

.. raw:: html

   <h3>

C5 Issues and Software Update

.. raw:: html

   </h3>

ORNL and the C5 vendor modified the C5 slingshot network. That work
appears to have resolved the MPI failures that several users hit after
the last C5 outage. ORNL is still investigating the SLURM port
exhaustion.

C5 will receive an updated OS and support software. This is being done
to ensure C5's software has long-term vendor support.

.. raw:: html

   <h2>

Current Outages

.. raw:: html

   </h2>

.. raw:: html

   <h3>

20-24 March 2023 – C4 OS and PrgEnv update

.. raw:: html

   </h3>

HPE Cray no longer supports the OS and Programming Environment (PrgEnv)
currently on C3 and C4. This causes issues when working with HPE and the
Lustre hardware vendor. C3 and C4 must be updated to ensure we continue
receiving support. This outage will update C4 to the latest supported OS
and PrgEnv. Testing has determined that users will not need to recompile
their executables, and these older executables should reproduce the
current results. Compilations on the new environment will not reproduce
previous results. This is due to differences in compiler versions and
system libraries. The available compilers on the new PrgEnv are listed
in the document:
https://docs.google.com/document/d/1YabQ3ZljYRVFyilIG6fimyFd-TaHkDxHtz6ScPZrYzw.

Please send questions to the Gaea Help Desk.

.. raw:: html

   <h2>

Upcoming Outages

.. raw:: html

   </h2>

.. raw:: html

   <h3>

01-17 April 2023 - C5 OS update

.. raw:: html

   </h3>

To ensure the OS and support software on C5 is supported long-term, ORNL
and the hardware vendor will update the OS and software on C5 to the
latest version. We are doing this work now as NOAA does not consider C5
in production. After installing the software, ORNL will run the full
acceptance suite to ensure the new software does not deprecate the C5
performance.

.. raw:: html

   <h3>

14-18 April 2023 – C3 OS and PrgEnv update

.. raw:: html

   </h3>

C3 will receive the same update as performed on C4 during the 20-24
March outage.

.. raw:: html

   <h1>

Thursday, March 09, 2023

.. raw:: html

   </h1>

.. raw:: html

   <h2>

Current Issues

.. raw:: html

   </h2>

.. raw:: html

   <h3>

F2 Performance – Ongoing

.. raw:: html

   </h3>

F2 performance is still suffering from intermittent performance
degradation. As previously reported, we have found that the usage of
hard and soft links in users' workflows, particularly for files shared
by multiple job streams, is one of the causes of this degradation. We
request users update their workflow to ensure jobs streams do not access
the same files. The GFDL FRE workflow, version bronx-20, is updated to
use a single copy per experiment. Please get in touch with the Gaea
helpdesk if you require assistance.

.. raw:: html

   <h3>

C5 Issues and Testing

.. raw:: html

   </h3>

Last weekend, we paused the scheduler on C5 to check if a bug in the
lustre client software affected work on C3 and C4. The test was
inconclusive. However, earlier this week, ORNL received a patch for the
C5 lustre client that fixed the bug. This patch is now in place. Testing
indicates this issue is resolved.

Jobs on C5 are currently hitting two unrelated problems:

#. SLURM port exhaustion
#. MPI failures

ORNL is continuing to investigate the port exhaustion. ORNL has modified
the C5 configuration to increase the ports available to SLURM. ORNL is
also in contact with SchedMD, the developers of SLURM, for further
assistance.

The MPI failures might be tied to an issue with the slingshot network.
Portions of the network were reconfigured for the new C5 nodes. HPE ran
tests on the reconfigured network but did not run a test on the full
network. ORNL began running the tests yesterday. The tests indicate that
there is something misconfigured.

ORNL and HPE have taken C5 to investigate the issue further. If needed,
C5's network will be restored to the state before the new nodes are
added. C5 will likely be down for the remainder of today and possibly
tomorrow. ORNL will let us know a time after they have performed more
tests and begun the required work.

When attempting to requeue the work on C5, unfortunately, the command
was incorrect and instead canceled the work. In addition, the command
also cancelled jobs on the other gaea clusters c3, c4, and es. ORNL has
apologized for this mistake.

.. raw:: html

   <h2>

Upcoming Outages

.. raw:: html

   </h2>

.. raw:: html

   <h3>

20-24 March 2023 – C4 OS and PrgEnv update

.. raw:: html

   </h3>

HPE Cray no longer supports the OS and Programming Environment (PrgEnv)
currently on C3 and C4. This causes issues when working with HPE and the
Lustre hardware vendor. C3 and C4 must be updated to ensure we continue
receiving support. This outage will update C4 to the latest supported OS
and PrgEnv. Testing has determined that users will not need to recompile
their executables, and these older executables should reproduce the
current results. Compilations on the new environment will not reproduce
previous results. This is due to differences in compiler versions and
system libraries. The available compilers on the new PrgEnv are listed
in the document:
https://docs.google.com/document/d/1YabQ3ZljYRVFyilIG6fimyFd-TaHkDxHtz6ScPZrYzw.
The new environment is available on the gaea16 login node. Users can
access this node using ``gsissh gaea16`` from one of the other gaea
login nodes.

After C3 and C4 are updated, one login node will remain on the old
image, allowing users to recompile and reproduce previous results. This
node will only be accessible via a SLURM job – no direct login.

Questions should be sent to the Gaea Help Desk.

.. raw:: html

   <h3>

14-18 April 2023 – C3 OS and PrgEnv update

.. raw:: html

   </h3>

If the C4 update works as expected, C3 will receive the same update.

.. raw:: html

   <h1>

Monday, February 27, 2023

.. raw:: html

   </h1>

.. raw:: html

   <h2>

Current Issues

.. raw:: html

   </h2>

.. raw:: html

   <h3>

F2 Performance – Ongoing

.. raw:: html

   </h3>

This is a reminder that we still see intermittent performance issues
tied to F2 usage. We have worked with a few users to change their
workflow to use individual files per job. Monitoring has indicated this
has lowered the load on F2. We request users update their workflow not
to use shared files directly but to copy them into their run directory.
The GFDL FRE workflow, version bronx-20, is updated to use a single copy
per experiment. Please get in touch with the Gaea helpdesk if you
require assistance.

Last week, we were alerted of a few MDT issues that were resolved
quickly. These issues may have caused jobs to hang, and possibly time
out.

.. raw:: html

   <h2>

Past Outages

.. raw:: html

   </h2>

.. raw:: html

   <h3>

14 February 2023 – Slurm and F2 Bios Update

.. raw:: html

   </h3>

During the 14 Feb outage, an issue occurred that forced ORNL to not
perform the F2 bios update. The F2 vendors are working on the issue, and
will supply an update to ORNL to be performed at the March outage.</p<

During this outage, ORNL discovered issues with the slingshot cabeling
on C5. ORNL and HPE reworked the cabeling, which required C5 to be
unavailable longer than expected.

``C5 remained in maintenance through the start of the scheduled 17 Feb C5 maintenance.  The SLURM configuration on C5 was updated to use a new option ``\ ``numa_node_as_socket``\ ``.  This option will use the AMD Epyc NUMA zones when distributing the MPI processes, as opposed to the smaller L3 cache.  More information is in the ``\ ```SLURM Configuration`` <https://slurm.schedmd.com/slurm.conf.html#OPT_SlurmdParameters>`__\ `` Documentation.``

.. raw:: html

   <h3>

17-28 February 2023 – C5 additional acceptance testing

.. raw:: html

   </h3>

Acceptance of the additional 128 C5 nodes is still progressing. When
finished, access to C5 will be opened to all gaea users.

.. raw:: html

   <h2>

Upcoming Outages

.. raw:: html

   </h2>

.. raw:: html

   <h3>

20-24 March 2023 – C4 OS and PrgEnv update

.. raw:: html

   </h3>

HPE Cray no longer supports the OS and Programming Environment (PrgEnv)
currently on C3 and C4. This causes issues when working with HPE and the
Lustre hardware vendor. C3 and C4 need to be updated to ensure we
continue to receive support. This outage will update C4 to the latest
supported OS and PrgEnv. Testing has determined that users will not need
to recompile their executables, and these older executables should
reproduce the current results. Compilations on the new environment will
not reproduce previous results. This is due to differences in compiler
versions and system libraries. The available compilers on the new PrgEnv
are listed in the document:
https://docs.google.com/document/d/1YabQ3ZljYRVFyilIG6fimyFd-TaHkDxHtz6ScPZrYzw.
The new environment is available on the gaea16 login node. Users can
access this node using ``gsissh gaea16`` from one of the other gaea
login nodes.

After C3 and C4 are updated, one login node will remain on the old
image, allowing users to recompile and reproduce previous results. This
node will only be accessible via a SLURM job – no direct login.

Questions should be sent to the Gaea Help Desk.

.. raw:: html

   <h3>

14-18 April 2023 – C3 OS and PrgEnv update

.. raw:: html

   </h3>

If the C4 update works as expected, C3 will receive the same update.

.. raw:: html

   <h1>

Monday, February 13, 2023

.. raw:: html

   </h1>

.. raw:: html

   <h2>

Current Issues

.. raw:: html

   </h2>

.. raw:: html

   <h3>

F2 Performance – Ongoing

.. raw:: html

   </h3>

This is a reminder that we still see intermittent performance issues
tied to F2 usage. We have worked with a few users to change their
workflow to use individual files per job. Monitoring has indicated this
has lowered the load on F2. We request users update their workflow not
to use shared files directly but to copy them into their run directory.
The GFDL FRE workflow, version bronx-20, is updated to use a single copy
per experiment. Please get in touch with the Gaea helpdesk if you
require assistance.

.. raw:: html

   <h2>

Upcoming Outages

.. raw:: html

   </h2>

.. raw:: html

   <h3>

14 February 2023 – Slurm and F2 Bios Update

.. raw:: html

   </h3>

ORNL will update the BIOS on the Lustre system to address security
issues.

Gaea and GFDL’s PAN will upgrade SLURM to the latest version, 22.05.8.
This will address several bugs, one of which may affect the C5 cluster.
All work will be requeued before the outage.

During this update, SLURM on C5 will have a configuration change. SLURM
on C5 is currently using the option ``l3cache_as_socket`` to instruct
SLURM on distributing the MPI processes. With 22.05.08, C5 will be
configured with a new option ``numa_node_as_socket``. This option will
use the AMD Epyc NUMA zones when distributing the MPI processes, as
opposed to the smaller L3 cache. More information is in the `SLURM
Configuration <https://slurm.schedmd.com/slurm.conf.html#OPT_SlurmdParameters>`__
Documentation.

.. raw:: html

   <h3>

17-24 February 2023 – C5 additional acceptance testing

.. raw:: html

   </h3>

C5 is getting an additional 128 nodes. ORNL will need to run these new
nodes through their acceptance testing. After this outage, C5 will be
available for all users. However, C5 will still not be in production.
The system may be taken for maintenance without notification. Dual run
all Important work run on C5.

.. raw:: html

   <h3>

20-24 March 2023 – C4 OS and PrgEnv update

.. raw:: html

   </h3>

HPE Cray no longer supports the OS and Programming Environment (PrgEnv)
currently on C3 and C4. This causes issues when working with HPE and the
Lustre hardware vendor. C3 and C4 need to be updated to ensure we
continue to receive support. This outage will update C4 to the latest
supported OS and PrgEnv. Testing has determined that users will not need
to recompile their executables, and these older executables should
reproduce the current results. Compilations on the new environment will
not reproduce previous results. This is due to differences in compiler
versions and system libraries. The available compilers on the new PrgEnv
are listed in the document:
https://docs.google.com/document/d/1YabQ3ZljYRVFyilIG6fimyFd-TaHkDxHtz6ScPZrYzw.
The new environment is available on the gaea16 login node. Users can
access this node using ``gsissh gaea16`` from one of the other gaea
login nodes.

After C3 and C4 are updated, one login node will remain on the old
image, allowing users to recompile and reproduce previous results. This
node will only be accessible via a SLURM job – no direct login.

Questions should be sent to the Gaea Help Desk.

.. raw:: html

   <h3>

14-18 April 2023 – C3 OS and PrgEnv update

.. raw:: html

   </h3>

If the C4 update works as expected, C3 will receive the same update.

.. raw:: html

   <h1>

Monday, February 06, 2023

.. raw:: html

   </h1>

.. raw:: html

   <h2>

Current Issues

.. raw:: html

   </h2>

.. raw:: html

   <h3>

F2 Performance – Ongoing

.. raw:: html

   </h3>

Intermittent performance issues tied to F2 are ongoing. Some of these
issues are tied to users with several concurrent jobs using the same
files. This is especially true if the files are in a public area, e.g.
``/lustre/f2/pdata``, and not copied to a single-job area. Using a
single copy of a file per job stream alleviates some of the IO pressure.
The GFDL FRE workflow, version bronx-20, is updated to use a single copy
per experiment. Non-FRE workflows should be modified to do something
similar. If you require assistance with this type of update, please
contact the help desk.

.. raw:: html

   <h3>

NFS area, ``/ncrc/proj``, usage

.. raw:: html

   </h3>

In past Gaea Update emails, the new ``/ncrc/proj`` area was announced.
The information on the type of files to be placed in that area was not
as clear as it needed to be. The ``/ncrc/proj`` file system is small
(2TB) and should only be used for shared (group or project) software
environments. Personal software environments should be placed in the
user’s home space. Groups should not store large files or data sets in
``/ncrc/proj``. The ``/lustre/f2`` file system should be used for
job-related data.

The /ncrc/proj area should not be used for user development. User
development should be done in the ``/ncrc/home[12]`` areas. The user
quota for home directories is now 50GB, which increased from 10GB. We
realize more than 50GB may be needed for some users. If you find 50GB
insufficient, please submit an HD ticket. The documentation on the
gaeadocs wiki will be updated with this information.

.. raw:: html

   <h2>

Upcoming Outages

.. raw:: html

   </h2>

.. raw:: html

   <h3>

14 February 2023 – Slurm and F2 Bios Update

.. raw:: html

   </h3>

ORNL will update the BIOS on the Lustre system to address security
issues.

Gaea and GFDL’s PAN will upgrade SLURM to the latest version, 22.05.8.
This will address several bugs, one of which may affect the C5 cluster.
All work will be requeued before the outage.

.. raw:: html

   <h3>

17-24 February 2023 – C5 additional acceptance testing

.. raw:: html

   </h3>

C5 is getting an additional 128 nodes. ORNL will need to run these new
nodes through their acceptance testing. After this outage, C5 will be
available for all users. However, C5 will still not be in production.
The system may be taken for maintenance without notification. Dual run
all Important work run on C5.

.. raw:: html

   <h3>

20-24 March 2023 – C4 OS and PrgEnv update

.. raw:: html

   </h3>

HPE Cray no longer supports the OS and Programming Environment (PrgEnv)
currently on C3 and C4. This causes issues when working with HPE and the
Lustre hardware vendor. C3 and C4 need to be updated to ensure we
continue to receive support. This outage will update C4 to the latest
supported OS and PrgEnv. Testing has determined that users will not need
to recompile their executables, and these older executables should
reproduce the current results. Compilations on the new environment will
not reproduce previous results. This is due to differences in compiler
versions and system libraries. The available compilers on the new PrgEnv
are listed in the document:
https://docs.google.com/document/d/1YabQ3ZljYRVFyilIG6fimyFd-TaHkDxHtz6ScPZrYzw.
The new environment is available on the gaea16 login node. Users can
access this node using ``gsissh gaea16`` from one of the other gaea
login nodes.

After C3 and C4 are updated, one login node will remain on the old image
to allow users to recompile to reproduce previous results. This node
will only be accessible via a SLURM job – no direct login.

Questions should be sent to the Gaea Help Desk.

.. raw:: html

   <h3>

14-18 April 2023 – C3 OS and PrgEnv update

.. raw:: html

   </h3>

If the C4 update works as expected, C3 will receive the same update.

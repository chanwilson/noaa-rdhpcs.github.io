Overview
========

The Gaea /lustre/f2 is a lustre file system. Lustre is a parallel file
system has some some custom tools to work with it. Users should employ
these tools rather than the operating system equivalent tools when
working on the f2 filesystem.

lfs
===

lfs offers a few lustre specific versions of unix tools such as df and
find. For more information on these tools, do a "man lfs." These Lustre
specific tools are safer than general POSIX commands because they are
specifically designed for the Lustre filesystems. Please use lfs find
and lfs df within /lustre/f2 on Gaea.

.. _lfs_find:

lfs find
--------

::

   lfs find [[!] --atime|-A [-+]N] [[!] --mtime|-M [-+]N]
                  [[!] --ctime|-C [-+]N] [--maxdepth|-D N] [--name|-n pattern]
                  [--print|-p] [--print0|-P] [[!] --obd|-O &lt;uuid[s]&gt;]
                  [[!] --size|-S [-+]N[kMGTPE]] [--type |-t {bcdflpsD}]
                  [[!] --gid|-g|--group|-G &lt;gname&gt;|&lt;gid&gt;]
                  [[!] --uid|-u|--user|-U &lt;uname&gt;|&lt;uid&gt;]
                  &lt;dirname|filename&gt;

Searches the directory tree rooted at the given directory/filename for
files that match the given parameters. Using ! before an option negates
its meaning (files NOT matching the parameter). Using + before a numeric
value means files with the parameter OR MORE. Using - before a numeric
value means files with the parameter OR LESS.

.. _lfs_df:

lfs df
------

::

   lfs df [-i] [-h] [--pool|-p &lt;fsname&gt;[.&lt;pool&gt;] [path]

Report file system disk space usage or inode usage (with **-i**) of each
MDT/OST or a subset of OSTs if a pool is specified with **-p**. By
default, prints the usage of all mounted Lustre file systems. Otherwise,
if **path** is specified, prints only the usage of that file system. If
**-h** is given, the output is printed in human-readable format, using
SI base-2 suffixes for **M**\ ega-, **G**\ iga-, **T**\ era-,
**P**\ eta-, or **E**\ xabytes.

lustredu
========

The new version of lustredu with NOAA research group reporting features
is now installed on the Gaea login nodes. It is not default, but can be
loaded via module:

::

   module load lustredu/1.3

Description
-----------

Lustredu was written to give the user the ability to view that last
‘recorded’ size of a directory. The advantages of lustredu is the query
does not hit the lustre metadata at all as a normal du would. Instead,
the query goes to a separate database to give the last known size of the
directory.

This should be useful when using htar to archive directories to HPSS.
This can help ensure the total size written to HPSS is a reasonable
size. It should also be useful if there is a curiousity about the number
of files or size used in a directory (you want to know how much data a
job generated).

Notes
-----

#. Quotas for each NOAA research group on a file system are calculated
   from 'Adjusted Monthly Allocation' output from your HPCRPT tool. This
   means that research groups over their file system soft quota(s) are
   essentially using storage resources that are disproportional to their
   CPU allocation, as set by NOAA. Groups with no entry in HPCRPT have a
   "0" quota, but other attributes are still displayed.
#. The DB queries are fairly large for the new features, so it takes a
   few minutes to run. Recall that the underlying DB data is only
   changing once every 12 hours.
#. The old features from previous versions of lustredu remain unchanged.

Please submit a GFDL help desk ticket if you encounter any issues with
these new features.

Usage
-----

Summarize disk usage of each DIRECTORY recursively.

Mandatory arguments to long options are mandatory for short options too.

::

          -B,    print sizes in bytes instead of human readable format (e.g., 1KB 234MB 2GB)
          -n,    do not print headings on listing
          -v,    display version information and exit

          -q,    group based quotas

          --help display help information and exit

          SIZE may be (or may be an integer optionally followed by) one of following: KB 1024, MB 1024*1024, and so on for G, T, P, E.

.. _new_feature:

New Feature
-----------

Then to see group based quota summaries:

::

   lustredu -q

f1rpt
=====

f1rpt will provide another tool for monitoring usage of the f2
filesystem that is more closely tied to the compute allocations and user
groups than lustredu. It currently does not work, due to lustredu not
working with F2. We will update this when lustredu works with F2.

::

   &gt;module load f1rpt
   &gt;f1rpt --help
   Usage: f1rpt [options]

   Options:
     -h, --help  show this help message and exit
     -s          summary - defaults to centers
     -c          report on center usage
     -g          report on group usage
     -r          human-readable sizes with suffixes (KB, MB, GB, TB, etc.)
     -l          report on location usage
     -a          report on account usage
     -u          report on user usage

   &gt;f1rpt -r -s
   Time of report: 2014-07-29 17:05:39
   Center      Allocation % Allocation (Bytes) % of Allocation Used   Time To Fill Quota Bytes Used Delta Bytes/Day  File Count Delta Files/Day    Newest Datestamp
               %%%%%%%%%%%% ================== %%%%%%%%%%%%%%%%%%%% TTTTTTTTTTTTTTTTTTTT ========== ddddddddddddddd =========== ddddddddddddddd DDDDDDDDDDDDDDDDDDD
   AOML               0.31%             18.1TB               26.38%    26 days, 07:08:27      4.8TB         517.9GB      93,235           2,198 2014-07-29 17:05:39
   CPO                6.11%            361.4TB              195.98%                  N/A    708.2TB          -3.8TB  40,277,916       1,553,551 2014-07-29 17:05:39
   ESRL               0.37%             21.7TB                1.41% 13066 days, 20:40:22    312.6GB           1.7GB      54,531           2,274 2014-07-29 17:05:39
   GFDL              86.81%           5131.2TB               85.97%     4 days, 22:26:10   4411.4TB         145.9TB  48,769,399       1,605,531 2014-07-29 17:05:39
   NCEP               6.39%            377.9TB               59.86%    18 days, 09:27:21    226.2TB           8.2TB  21,091,641         718,424 2014-07-29 17:05:39
   WIND               0.00%              0.0 B                  N/A                  N/A    324.8TB           1.9TB  19,744,330         104,020 2014-07-29 07:42:01
               %%%%%%%%%%%% ================== %%%%%%%%%%%%%%%%%%%% TTTTTTTTTTTTTTTTTTTT ========== ddddddddddddddd =========== ddddddddddddddd DDDDDDDDDDDDDDDDDDD
   All centers       99.99%           5910.2TB               96.03%                  N/A   5675.7TB         152.7TB 130,031,052       3,985,999 2014-07-29 17:05:39

Please note that neither f1rpt nor lustredu are capable of detecting and
accounting for hard links of files across major subdirectories within
f2. If I have a large file in my /lustre/f2/scratch/$USER directory and
a hard link to it in my /lustre/f2/dev/$USER directory and I then run

::

   lustredu /lustre/f2/scratch/$USER /lustre/f2/dev/$USER

lustredu will report two summaries, one for each location, and will
include the same large file twice. This is an artifact of how du works.
Hard links confound it.

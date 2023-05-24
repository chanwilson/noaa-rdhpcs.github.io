Summary
=======

This article describes the process of configuring and utilizing GridFTP
directly for file transfers. Please note that in most cases users should
rely on GCP for file transfers. The GridFTP tools are located in the
globus module:

::

   module load globus

The main command is:

::

   globus-url-copy

Security
========

GridFTP, like standard FTP, divides transfer data into two channels. The
control channel sends instructions between the client and server, while
the data channel is responsible for transferring the specific data
requested. Authentication can be performed in the control channel via
SSH (gsissh:*) or GSI (gsiftp:*). SSH utilizes existing ssh certificates
and is the simpler of the two to configure in most environments. GSI
relies on your analysis certificate and is simple to utilize at GFDL. It
is recommended that the GSI protocol be used, as it provides a wealth of
additional GridFTP options that are unsupported by the ssh
authentication mechanism. If you see certificate failure messages when
trying to use gsiftp, check the output of the grid-proxy-info command.
If all looks well there, contact the GridFTP administrator to ensure
that GridFTP is configured to allow the transfer of files to your chosen
destination.

.. _firewall_configuration:

Firewall Configuration
======================

You can use the environmental variables GLOBUS_TCP_PORT_RANGE=min,max
and GLOBUS_TCP_SOURCE_RANGE=min,max to control the inbound and outbound
ports to the client, respectively. Globus recommends a set of at least
1000 ports (e.g., 40000-46999).

.. _transfer_options:

Transfer Options
================

.. _small_file_performance:

Small File Performance
----------------------

Transferring many small files via globus-url-copy greatly diminishes its
performance. For most copy tools, the usual solution is to tar the files
prior to transfer and untar once they have arrived at the destination.
Globus has implemented some functionality called pipelining into the
globus-url-copy command (only usable when gsiftp is the authentication
mechanism), which instructs GridFTP to not wait for an acknowledgment
after a single file has been transferred. The result is that many files
can be in transit to the destination, thus making efficient use of
available bandwidth. The pipelining option is -pp.

Recovery
--------

Globus-url-copy has a few options to recover transfers should problems
arise. The -rst argument can be passed which instructs GridFTP to retry
failed transfers. The number of retries is specified by the -rst-retries
<retries> option, which has a default value of 5 if not provided on the
command line (use 0 for unlimited). To instruct GridFTP to only retry
sending the files that were not sent prior to failure (rather than the
entire file list again), use the -df <file> option. This option saves
all failed transfer URLs to a file, which is used by globus-url-copy if
a retry is needed.

You can use --stall-timeout <time> to specify how long to wait before
idle transfers will be killed.

.. _bulk_transfers:

Bulk Transfers
--------------

If you want to transfer entire directories or lists of files, there are
two options. Use -r to recursively transfer a directory in the normal
way. Alternatively, specify -f <file> to instruct GridFTP to look in the
file indicated for a list of source-destination URL pairs:

::

   &quot;gsiftp://nfs02.princeton.rdhpcs.noaa.gov/archive/keo/file1.nc&quot; &quot;gsiftp://pcmdi@data1.gfdl.noaa.gov/home/keo/&quot;
   &quot;gsiftp://nfs02.princeton.rdhpcs.noaa.gov/archive/keo/file2.nc&quot; &quot;gsiftp://pcmdi@data1.gfdl.noaa.gov/home/keo/&quot;
   &quot;gsiftp://nfs02.princeton.rdhpcs.noaa.gov/archive/keo/file3.nc&quot; &quot;gsiftp://pcmdi@data1.gfdl.noaa.gov/home/keo/&quot;

.. _network_options:

Network Options
===============

.. _buffer_size:

Buffer Size
-----------

You can specify the tcp buffer size with the -tcp-bs <size> command. To
calculate an appropriate value for <size> use the bandwidth delay
product:

::

   buffer_size = bandwidth in Megabits per second (Mbs) * RTT in milliseconds (ms) * 1000 / 8

Where RTT can be obtained via the ping or traceroute command and
bandwidth is determined as the maximum bandwidth between the source and
destination (best determined by talking to your network administrator).

Parallelism
-----------

You can specify the number of parallel data connections using -pp
<streams>. A good default value is 4, and there is no formula for
determining the ideal number for your network. The GridFTP user's manual
specifies that values between 2 and 10 generally provide the best
performance. When in doubt, use the defaults! There is a reason why they
are defaults!

Using the -p <streams> option with gsiftp will put GridFTP in a special
transfer mode called "Mode E" (also specified via the -fast option).
This mode utilizes data channel caching to keep the data channel open
for multiple file transfers. It is also needed for parallelism as it
allows data to arrive in any order.

.. _misc_options:

Misc Options
============

Some other important options are -vb (verbose) and -cd (create
directories at the destination).

Examples
========

Here is a sample GridFTP transfer utilizing the transfer file (-f)
option:

::

   globus-url-copy -bs 6MB -pp -p 4 -vb -stall-timeout 14400 -rst -cd -df /tmp/grid-state -f /tmp/grid-transfer

This command specifies that we should transfer with the block size at
6MB, pipelining enabled, 4 parallel streams, verbose, idle timeout at
14400 seconds (4 hours), retry on failures, create directories, a retry
file holding failed URLs, and a transfer file holding URL pairs of files
to be transferred. Perhaps the last command was more than you require. A
simple transfer can be accomplished via a job on the RDTNs:

::

   set hn=`hostname --fqdn`
   globus-url-copy gsiftp://rdtn.lb.princeton.rdhpcs.noaa.gov/archive/$user/file gsiftp://${hn}/lustre/f2/dev/${user}/

or from Zeus:

::

   set hn=`hostname --fqdn`
   globus-url-copy gsiftp://dtn-zeus.rdhpcs.noaa.gov/archive/$user/file gsiftp://${hn}/lustre/f2/dev/${user}/

.. _external_links:

External Links
==============

http://en.wikipedia.org/wiki/GridFTP -- GridFTP on Wikipedia

http://www.globus.org/toolkit/docs/5.0/5.0.2/data/gridftp/user/#gridftpUser
-- GridFTP User's Guide (version 5.0.2)

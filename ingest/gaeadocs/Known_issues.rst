GAEA
====

.. _cac_bastions_refusing_login_attempts_without_asking_for_pin:

CAC bastions refusing login attempts without asking for PIN
-----------------------------------------------------------

We have had reports of users being unable to connect to the CAC bastions
via TECTIA client. As documented, CAC bastions are the servers you
connect to with the sshg3 gaea.rdhpcs.noaa.gov. They maintain your
Globus certificate and put your connection through to the Gaea login
nodes. On Linux clients one workaround is to kill the ssh-broker-g3
process and try your login again.

::

   ps -ef | grep ssh-broker-g3
   4060     15451 15184  0 14:05 pts/4    00:00:00 grep ssh-broker-g3
   4060     29775 29765  0 Dec22 ?        00:00:42 /opt/tectia/bin/ssh-broker-g3 --run-on-demand
   kill -9 29775
   sshg3 gaea

.. _c3_c4_shells_hang_on_login_x2go_connections_hang_at_connecting:

C3 & C4 shells hang on login & X2Go connections hang at "connecting"
--------------------------------------------------------------------

Users have often reported issues where their sessions freeze or hang on
C3 login nodes (gaea9-gaea12) unless Ctrl+c is pressed.

Furthermore, X2Go connections hang (for more than the usual 10 seconds
or so) at "connecting".

This issue can also result in your jobs timing out either at the start
of the job or the end.

A fix for this is
`known <https://bugzilla.redhat.com/show_bug.cgi?id=885901>`__ to the
Linux community but has yet to be released for the Linux distro on Gaea.

The workaround is to delete or move the ~/.history file.

.. _potential_workaround_for_current_gaea_slowness:

Potential workaround for current Gaea slowness
----------------------------------------------

Many jobs on Gaea are currently experiencing longer than normal run
times.

One user has gotten his jobs to complete successfully again by
increasing io_layout\* (thereby decreasing the load on the I/O
server/node).

This isn't a guaranteed workaround, but we wanted to share with everyone
in case it helps others.

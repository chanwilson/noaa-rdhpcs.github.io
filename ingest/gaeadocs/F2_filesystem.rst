.. _f2_background:

F2 Background
=============

ORNL replaced f1 with a Lustre filesystem called "F2". F2 is currently
mounted on all partitions of Gaea. Performance will degrade as the
filesystem exceeds 80% utilization, and jobs will be effected with I/O
errors at 85% utilization.

F2 is not backed-up. It is not possible to restore deleted or swept
data. Please ensure data you need to keep is copied to your archive.

You should have directories in the following locations:

-  /lustre/f2/scratch/$USER (symlinked from
   /lustre/f2/scratch/<YOUR_CENTER>/$USER)
-  /lustere/f2/dev/$USER (symlinked from
   /lustre/f2/dev/<YOUR_CENTER>/$USER)

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

.. _f2_specs:

F2 Specs
========

-  Improved I/O performance
-  33 PB of usable storage
-  Automatic lossless compression of files

   -  To check the amount of compression, use du with and without the
      --apparent-size argument.

-  Additional metadata capacity

For more information on Lustre tools please reference `Lustre
Filesystems Tools <Lustre_tools>`__ page.

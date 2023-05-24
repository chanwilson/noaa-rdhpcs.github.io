.. figure:: Gaea_08_03.png
   :alt: NOAA Gaea supercomputer located in Oak Ridge, TN

`Gaea <https://www.noaa.gov/organization/information-technology/gaea>`__
is an `NOAA Research and Development High-Performance Computing System
(RDHPCS) <https://www.noaa.gov/information-technology/hpcc>`__ operated
by the `National Climate-Computing Research Center
(NCRC) <https://www.ncrc.gov/>`__. The NCRC is located within the
`National Center for Computational Sciences
(NCCS) <https://www.ornl.gov/division/nccs>`__ at the `Oak Ridge
National Laboratory (ORNL) <https://www.ornl.gov/>`__. The NCRC is a
collaborative effort between the `Department of
Energy <https://www.energy.gov/>`__ and the `National Atmospheric and
Oceanic Administration <https://www.noaa.gov/>`__.

The Gaea System consists of two HPE Cray XC40 supercomputers and an HPE
Cray EX supercomputer. The XC40 systems have an aggregate of more than
200 terabytes of memory and a peak calculating capacity greater than
5.25 petaflops. The EX system has 482 terabytes of memory and a peak
calculating capacity of 10.2 petaflops.

Gaea uses a high-capacity Lustre file system with over 32 petabytes of
storage. The file system is connected to the Gaea system using FDR
InfiniBand.

Access to Gaea is managed through two 10-gigabit lambdas, or optical
waves, connected to `NOAA's NWAVE <https://noc.nwave.noaa.gov/>`__
network through peering points at Atlanta, GA and Chicago, IL.

.. raw:: html

   <table style="width: 60%; border-collapse: collapse;">

.. raw:: html

   <tr>

.. raw:: html

   <th style="border-top: 1px solid #dee2e6; border-bottom: 2px solid #dee2e6; vertical-align: bottom; padding: 0.75rem;">

C3 Stats

.. raw:: html

   </th>

.. raw:: html

   <th style="border-top: 1px solid #dee2e6; border-bottom: 2px solid #dee2e6; vertical-align: bottom; padding: 0.75rem;">

C4 Stats

.. raw:: html

   </th>

.. raw:: html

   <th style="border-top: 1px solid #dee2e6; border-bottom: 2px solid #dee2e6; vertical-align: bottom; padding: 0.75rem;">

C5 Stats

.. raw:: html

   </th>

.. raw:: html

   <th style="border-top: 1px solid #dee2e6; border-bottom: 2px solid #dee2e6; vertical-align: bottom; padding: 0.75rem;">

F2 Stats

.. raw:: html

   </th>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

#. Cray XC40-LC Haswell
#. 1,504 compute nodes (2 x Intel Haswell 16-cores per node)
#. 64GB DDR4 per node; 96TB total
#. 1.77 PF peak

.. raw:: html

   </td>

.. raw:: html

   <td>

#. Cray XC40-LC Broadwell
#. 2,656 compute nodes (2 x Intel Broadwell 18-cores per node)
#. 64GB DDR4 per node; 145TB total
#. 3.52 PF peak

.. raw:: html

   </td>

.. raw:: html

   <td>

#. HPE EX
#. 1920 compute nodes (2 x AMD Rome 64-cores per node)
#. 251 GB DDR5 per node; 449TB total
#. 10.2 PF peak

.. raw:: html

   </td>

.. raw:: html

   <td>

#. DDN Lustre
#. 32 PB total usable; ZFS compression
#. 36 OSS; 72 OST; 4 MDS

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

Gaea is the largest of the four NOAA RDHPCS, and is used to study the
earth's notoriously complex climate from a variety of angles by enabling
scientists to:

-  understand the relationship between

   -  climate change and extreme weather such as hurricanes;
   -  the atmosphere’s chemical makeup and climate

-  help unlock the climate role played by the oceans that cover nearly
   three-quarters of the globe.

.. _other_rdhpcs_documentation:

Other RDHPCS Documentation
==========================

.. raw:: mediawiki

   {{RDHPCS_Sites}}

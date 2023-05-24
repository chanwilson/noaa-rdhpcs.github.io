`Getting Help <getting_help>`__

.. _obtain_an_account:

Obtain an Account
=================

`New Account
Process <https://rdhpcs-common-docs.rdhpcs.noaa.gov/wiki/index.php/Getting_an_RDHPCS_Account>`__

#.  User gets NEMS/Gmail account from sponsoring lab's process.  (Get
   this done before starting the Gaea account request process.)
#. User uses NEMS/Gmail First.Last username and password to access
   https://aim.rdhpcs.noaa.gov and requests access to one or more
   projects.
#. PI of project approves.
#. HR approves.
#. ISSO (Information System Security Officer) approves.
#. RM (Resource Manager) approves. This last is the system owner for
   e.g. Gaea, Hera, Jet, Niagara.
#. Automation and manual account creation processes proceed.  If needed,
   an RSA fob is issued.

Note: NOAA RDHPCS systems use a "long user name" which is usually the
same as your NOAA email user name. These pages frequently refer to this
long user name as "First.Last" or <First.Last>.

.. _first_time_login:

First Time Login
----------------

-  `Logging
   In <https://rdhpcs-common-docs.rdhpcs.noaa.gov/wiki/index.php/Logging_in>`__
-  For those with CAC cards, use TECTIA: sshg3
   <First.Last>@gaea.rdhpcs.noaa.gov
-  For those without CAC cards or on Apple Macintosh clients: ssh
   <First.Last>@gaea-rsa.princeton.rdhpcs.noaa.gov or ssh
   <First.Last>@gaea-rsa.boulder.rdhpcs.noaa.gov

   -  You should now see a message to enter the PASSCODE from the RSA
      FOB
   -  Make sure the FOB has at least 3 bars on the left corner of the
      screen and enter the 6 digits as displayed on the screen and press
      enter
   -  A message should appear stating that to continue you must enter a
      new pin of at least 8 alphanumeric characters
   -  Enter the new pin (8 alphanumeric characters) and press enter.
   -  Then re-enter the same pin & press enter
   -  If the pins compare, you should see a message stating that the new
      pin has been accepted.
   -  You will now see a message asking to enter the PASSCODE from the
      FOB again. This time you will need to add your pin to the PASSCODE
      and Press enter.

      -  (e.g. if your pin was abcd1234 you would enter "abcd1234xxxxxx"
         where the x's are randomly generated numbers from the rsa fob)

-  At this point the prompt will ask you to create a passphrase. Create
   a minimum of 3 words pass phrase for your grid certificate. This only
   occurs if you did not already generate a passphrase.
-  Confirm the passphrase. Once confirmed it will take up to 24 hours
   for the certificate to be processed. Once the certificate is
   processed, login using the regular login instructions.

   -  Note: If your certificate is not processed in a timely manner,
      please contact support: `Getting Help <:getting_help>`__

Certificates
------------

Gaea, and the other NOAA RDHPCS systems use the Globus Toolkit, an X.509
certificate-based Public Key Infrastructure (PKI) authentication system
for your jobs to authenticate hands-free to both the machines they run
on and to other RDHPCS computers that your jobs may need to interact
with (e.g. the GFDL archive [the HPSS archive is accessed via hsi/htar
instead.])

When a user first logs into Gaea, a 1-year master certificate and a
30-day proxy certificate is generated. Every login before expiry renews
the 30-day proxy certificate to a fresh 30 day expiration date or the
expiration date of the master certificate, whichever is sooner. Users
need to have a valid master and proxy certificate to properly
authenticate and connect to Gaea. If you do not log in Gaea over a span
of 30 days then your proxy certificate will expire and Gaea will require
that a new proxy certificate is generated. This is the scenario in which
the user generated passphrase is used. Users will be prompted to renew
their proxy certificate with their passphrase. Users who cannot remember
their passphrase will need to enter it incorrectly until they are
prompted to also create a new master certificate and a corresponding new
passphrase. Only during this process of making a new master
certificate/passphrase will a user have to go through the certificate
signing delay again just as in the steps of first-time login process.

**Generating a Master Certificate (done in the "First Time Login"
section above)** Each RSA fob (comes with account) is distributed with
an "RSA Fob Activation" instruction sheet. Follow these instructions to
set your PIN and do your first login to Gaea. You will be prompted to
establish a certificate passphrase as documented above. Please read the
text and follow the prompts. Your certificate passphrase must be at
least 3 words. Your certificate must be signed before further access is
allowed. Please allow 24-48 hours for the certificate to be signed. You
will receive an email when you can proceed.

**You will have to remember your certificate passphrase one year from
now to renew your certificate.** Otherwise, one year from now, you will
have to create a new certificate and wait for it to be signed. If you do
remember your passphrase and successfully regenerate your master
certificate, a new proxy certificate will automatically be created and
used on your next login.

**Again, it is critical that you remember your certificate passphrase.
If you have to have a new certificate signed by an administrator, your
jobs will fail during the window of time between when you request the
new certificate and when you log in and a fresh proxy certificate is
created from your newly-signed certificate and put on Gaea for you.**
This could mean up to 2 days worth of job failures which equates to all
of your work falling out of the queues.

.. _regular_login:

Regular Login
-------------

Once a user has gone through the initial login steps and generated a
valid certificate, logging into Gaea is much simpler.

-  sshg3 <First.Last>@gaea.rdhpcs.noaa.gov
-  ssh <First.Last>@gaea-rsa.princeton.rdhpcs.noaa.gov (or ssh
   <First.Last>@gaea-rsa.boulder.rdhpcs.noaa.gov)

   -  Enter your pin and passcode from the RSA FOB.

      -  (ex. if you pin was abcd1234 you would enter "abcd1234xxxxxx"
         where x's are the randomly generated numbers from the rsa fob)

With ssh connection sharing enabled, you may do additional logins from
the same GFDL host without entering a passcode. To turn off ssh
connection sharing for just one login, do "ssh -S none gaea".

The gaea bastion host will then display the menu:

::

   The Gaea destinations are:
   Hostname            Description
   gaea                gaea head nodes
   gaea10              c3 head node
   gaea11              c3 head node
   gaea12              c3 head node
   gaea13              c4 head node
   gaea14              c4 head node
   gaea9               c3 head node

   You will now be connected to OneNOAA RDHPCS: Gaea (CMRS/NCRC) system.
   To select a specific host, hit ^C within 5 seconds.

To login to a specific host, hit control-c and enter the host name. By
default the load balancer with only connect you to a c1&c2 login node
(gaea1-8).

.. _x11_graphics:

X11 Graphics
------------

After login to gaea, you may run X11 terminal programs such as xterm or
gnome-terminal. These should open windows on your workstation that
perform reasonably well.

Other X11 graphics applications will run with limited performance. For
faster X11 graphics, use `X2go <X2go>`__.

.. _globus_using_your_proxy_certificate:

Globus (using your proxy certificate)
-------------------------------------

Once you are logged into a Gaea login node, you can use the Globus ssh
client to ssh between Gaea login nodes without manual authentication.

::

   gaea1&gt; gsissh gaea2
   banner…
   gaea2&gt;

.. _setting_up_ssh_port_tunnels:

Setting up SSH Port Tunnels
---------------------------

In a Gaea ssh session, run the following command to get your user ID
number:

::

   id -u

.. _linux_workstation_.sshconfig:

Linux workstation ~/.ssh/config
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you connect to Gaea from a Linux workstation, you may want to use the
following example ~/.ssh/config file to help make connecting to and
using Gaea via ssh easier.

::

   Host gaea*
   HostName gaea.rdhpcs.noaa.gov
   User &lt;First.Last&gt;
   ControlMaster auto
   LocalForward &lt;local_port&gt; localhost:&lt;local_port&gt;
   RemoteForward &lt;remote_port&gt; localhost:22

   Host *
   ControlMaster no
   ControlPath ~/.ssh/%r@%h:%p
   CheckHostIP yes
   ForwardAgent yes
   ForwardX11 yes
   AddressFamily inet

   NoHostAuthenticationForLocalhost yes

-  <First.Last> is your long username
-  <local_port> is 30000 plus your Gaea uid number
-  <remote_port> is 20000 plus your Gaea uid number

.. _gaea_.cshrc:

gaea ~/.cshrc
~~~~~~~~~~~~~

On Gaea you may want to adopt something like the below examples in your
~/.cshrc file. If your default shell is bash, you will need to alter
them for bash syntax.

::

   #add this near the top of your .[t]cshrc file for users whose default shell is [t]csh.

   #exit from processing ~/.cshrc if running on a Gaea RDTN - this prevents data transfer failures for users with rich environments set up via their ~/.cshrc

   if (`hostname –fqdn` =~ rdtn0[1-8].ncrc.gov) then
   exit
   endif

GFDL users, or other users interested in using the GFDL workflow
software, may want to add the following line to their ~/.cshrc file if
your default shell is [t]csh, or your ~/.bashrc file if your default
shell is bash. You can change your RDHPCS default shell via AIM.

::

   module use -a /ncrc/home2/fms/local/modulefiles

.. _gaea_.sshconfig:

gaea ~/.ssh/config
~~~~~~~~~~~~~~~~~~

On Gaea you may want to adopt something like the below example
~/.ssh/config file, substituting your user name and user ID (UID) number
as appropriate

::

   Host gfdl
     HostName localhost
     Port &lt;remote_port&gt;
     User &lt;GFDL_username&gt;
   LogLevel ERROR
   ForwardAgent yes
   ForwardX11 yes

-  <remote_port> is 20000 plus your GFDL uid number
-  <GFDL_username> is your GFDL short username

Accounting
==========

Gaea uses Slurm Fairshare to allocate the machine. More information is
available at: `Allocations_and_quotas <Allocations_and_quotas>`__

For accounting details and/or questions, please contact:

-  Daniel Gall (609) 651-7744

.. _setting_up_the_environment:

Setting up the Environment
==========================

Gaea is implemented using the Environment Modules system. This tool
helps users manage their Unix or Linux shell environment. It allows
groups of related environment-variable settings to be made or removed
dynamically. Modules provide commands to dynamically load, remove and
view software.

More information on using modules is available at `Gaea
Modules <Modules>`__.

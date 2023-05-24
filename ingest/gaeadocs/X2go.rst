Introduction
============

`X2Go <https://wiki.x2go.org/doku.php>`__ is an open-source remote
desktop software for Linux that uses a modified NX 3 protocol.

X2Go is the chosen remote desktop solution for gaea and other RDHPCS
systems. Please refer to the `RDHPCS Common Docs X2Go
documentation <https://rdhpcs-common-docs.rdhpcs.noaa.gov/wiki/index.php/X2go>`__
for general installation and configuration instructions.

**Note** Gaea uses a different window manager than the other RDHPCS
sites. At this time, Gaea only supports
`IceWM <https://ice-wm.org/>`__). Also, your port tunnel ports will be
different on Gaea.

.. _x2go_troubleshooting_tips:

X2go Troubleshooting Tips
=========================

As many are not familiar with the use of IceWM, and the use of IceWM on
gaea can be troublesome, below are some troubleshooting tips on how to
get around some of the known issues with IceWM and X2Go on Gaea.

.. _icewm_does_not_start:

IceWM Does Not Start
--------------------

If you get a black, empty screen without window manager controls, try
using the *Custom Desktop* X2Go session type, and manually enter
``icewm``.

.. _host_key_for_server_changed:

Host key for server changed
---------------------------

If a warning appears stating the host key for server 127.0.0.1:[port]
changed, this is due to SSH checking the host key for the localhost. To
get past this, run the command ``ssh-keygen -R 127.0.0.1:[port]`` or
``ssh-keygen -R localhost:[port]``, be sure to replace ``[port]`` with
the port number in the message. It should be your local port number. You
can also place the option and value
``NoHostAuthenticationForLocalhost yes`` in your ``~/.ssh/config`` file.

.. _term_set_in_shell_init:

TERM set in shell init
----------------------

Setting the ``TERM`` environment variable in the shell initialization
scripts (e.g. ``~/.cshrc``, ``~/.login``, ``~/.bash_profile``,
``~/.profile``, or ``~/.bashrc``), may cause issues with X2Go, and may
print the message “Connection failed. TERM: Undefined variable." To get
around this issue, we suggest wrapping the setting of TERM in a
protective if block, as shown below:

::

   # [t]csh                          | # [{ba,k,z,a}]sh
   if (! $?TERM) then                | if [ -z ${TERM+x} ]
     setenv TERM xterm-256color      | then
   else                              |   TERM=xterm-256color
     if ("$TERM" == "xterm") then    | else
       setenv TERM xterm-256color    |   if [ "$TERM" == "xterm" ]
     endif                           |   then
   endif                             |     TERM=xterm-256color
                                     |   fi
                                     | fi
                                     | export TERM

.. _changing_terminal_settings_with_stty_in_shell_initialization:

Changing terminal settings with stty in shell initialization
------------------------------------------------------------

The use of the ``stty`` command in shell initialization scripts (e.g.
``~/.cshrc``, ``~/.login``, ``~/.bash_profile``, ``~/.profile``, or
``~/.bashrc``) to change terminal settings may cause X2Go to not run
properly. The use of ``stty`` for X2Go sessions should be unnecessary.
If you do need to change shell settings for non-X2Go sessions, we
strongly suggest wrapping the calls of ``stty`` in if blocks. The
following is an example:

::

   # [t]csh                          | # [{ba,k,z,a}]sh
   test -t 0                         | test -t 0
   if ($? == 0) then                 | if [ $? -eq 0 ]
     # stty commands here            | then
   endif                             |   # stty commands here
                                     | fi

.. _x2go_authenticated_but_still_not_starting:

X2Go Authenticated, but still not starting
------------------------------------------

If you entered the wrong passcode (PIN + RSA tokencode) too many times,
or the RSA fob and server are out of sync, you may get a connection
error may get an error stating that other authentications may proceed,
or you might be prompted for a “verification code”. In either of these
cases, cancel the X2Go login attempt. Then from a terminal window, run
the command ``ssh -p [port] 127.0.0.1``, be sure to replace ``[port]``
with your local forward port. When prompted, authenticate with your RSA
PIN + tokencode. After the passcode is accepted, you will be prompted to
let the tokencode rollover, and enter a new code. Enter the new RSA
tokencode, without the PIN. Once authenticated to the login node, you
can close the connection and retry starting an X2Go session.

.. _x2go_client_hangs_while_connecting:

X2Go client hangs while connecting
----------------------------------

An X2Go connection that hangs at the connecting step is usually the same
issue that causes [t]csh shells to `hang during
initialization <Known_issues#C3_.26_C4_shells_hang_on_login_.26_X2Go_connections_hang_at_.22connecting.22>`__.
The workaround is to delete, or rename, the ``~/.history`` file on Gaea.

.. _change_icewm_preferences:

Change IceWM preferences
------------------------

To change IceWM settings, run the ``iceWMCP`` command from a terminal.
This will launch a GUI application with many of the IceWM
user-changeable preferences. When finished close the GUI, and run
``icewmbd -r`` to reload IceWM’s preferences in the current session.

IceWM preferences can be changed by editing the IceWM preference text
files. Please refer to the `IceWM FAQ and
Howto <https://ice-wm.org/FAQ/>`__ for more information. The IceWM FAQ
and Howto also lists many preferences settings, including changing the
mouse focus.

**Note**: *IceWM does not allow custom background color if set in the
IceWM theme. The workaround we have found is to create a custom theme,
and then modify the theme color. Please refer to* `IceWM Themes
page <https://ice-wm.org/themes/>`__ *for more information.*

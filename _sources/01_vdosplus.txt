.. _vdosplus:

#############################
WARES Execution Alternatives
#############################

The move to 64-bit Windows 7, 8, and 10 eliminates running WARES natively on a
Windows operating system. There are other options, however. These are:
 
*  DOS emulation using :program:`vDosPlus` on Windows 7, 8, and 10
*  :program:`VmWare` or similar virtual machine execution of DOS/WARES 
*  Microsoft's :program:`Virtual Windows XP` emulation (32-bit Windows only)
*  Remote desktop access to WARES on an ADDS Server (32-bit Windows only)
*  Linux Ubuntu desktop operating system, and :program:`DOSEMU`

Of these options, the easiest and most effective solution is the first one, 
:program:`VDosPlus`.

vDosPlus Emulation Program
=============================

:program:`VDosPlus`, subsequently referred to as :program:`VDP`, addresses the 
following concerns with running DOS applications today:

*  DOS programs cannot run on 64-bit Windows systems
*  DOS uses Windows Short File Names (SFN) and not Long File Names (LFN)
*  DOS does not print directly to Windows printers
*  DOS characters do not scale, the resulting display may be illegible
*  Programs requiring EMS memory (e.g., :program:`WARES`) may not work
*  NETBIOS networking (SMBv1) is deprecated and may not work

:program:`VDP` is an emulation, and therefore it runs more slowly than native 
DOS would. The other benefits of :program:`VDP` far outweigh the performance 
cost when using :program:`WARES`.

program:`VDP` is freeware, but its developers would appreciate any donation 
you would make. Donate `here <https://www.paypal.com/donate/?token=NVfuTMJzDGqiJ66VJ25gDNZcnTj_FU61I06AZCj11uGuhmlFCJWT9Pv1O28gQh6uE6ixhW&country.x=US&locale.x=US>`_.

Installing vDosPlus
=============================

*  First, download the latest version of vDosPlus from 
   http://files.vdosplus.org/vDosPlus-current-setup.exe. 
   Windows will probably save this file in your :file:`Downloads` folder
*  Open the download link in the browser to begin a default install, or open 
   your :file:`Downloads` folder in File Explorer, Right-Click file 
   :file:`vDosPlus-current-setup.exe`, and choose :guilabel:`Run`. Do not run 
   as administrator.
*  Click :guilabel:`Next` to start the installer. If necessary, click
   :guilabel:`I Agree` to accept the license terms, and :guilabel:`Next` to 
   continue ... 
*  At the :guilabel:`Destination Folder`, just click :guilabel:`Install` to
   use the default location :file:`C:\\vDOSPlus`
*  Accept any other options, particularly the option to create a desktop icon
*  Click :guilabel:`OK` to exit the installer when finished.

Configuring vDosPlus
=============================

In the same way as traditional DOS programs, :program:`vDosPlus` uses two files 
to set the system configuration: :file:`config.txt` and :file:`autoexec.txt`. 
:program:`vDosPlus` ships with a default files :file:`config.txt` and
:file:`autoexec.txt`, and these files must be replaced to run :program:`WARES`.

The following sample files have been tested to work with :program:`WARES` for 
most installations. (Call support if these do not work correctly.) Install 
these files as follows:

*  Open Windows :program:`File Explorer`, and navigate to folder directory
   :menuselection:`This PC --> Local Disk (C:) --> vDosPlus`
*  :kbd:`Right-click` file :file:`config.txt`, and rename it something like 
   :file:`config_orig.txt`
*  :kbd:`Right-click` file :file:`autoexec.txt`, and rename it something like 
   :file:`autoexec_orig.txt`
*  Download :download:`_downloads/config.txt`, saving it to the :file:`C:\vDosPlus` folder
*  Download :download:`_downloads/autoexec.txt`, saving it to the :file:`C:\vDosPlus` 
   folder
*  Start :program:`WARES` from the desktop icon for :program:`vDosPlus`


Modifying the Configuration
=============================

If the message appears, "The WARES.BAT command program cannot be found", then 
your :program:`WARES` installation is non-standard. You will have to edit file 
:file:`autoexec.txt` and change either the *AREVSHARE* or the *AREVLOCAL* 
entry to match the location where :program:`WARES` is installed. 

If you are running in a multi-user environment, each :program:`WARES` user 
should have a unique identifier. Edit file :file:`autoexec.txt` and change the 
*AREVUSER* entry to USER01, USER02, ... as desired.

There are many other display options in :program:`vDosPlus`, some of which are 
included in the configuration files but commented out (lines starting with '#'
or 'rem'). If you are good with DOS, change these settings to your liking. But 
read the :file:`README.TXT` file for :program:`vDosPlus` before making changes.

The sample text for :file:`config.txt` follows:

.. codeblock:: 

   _downloads/config.txt

The sample text for :file:`autoexec.txt` follows:

.. include:`_downloads/autoexec.txt`

Change Desktop Icon
=============================

*  On the desktop, :kbd:`<Right-Click>` the :program:`VDosPlus` icon and click 
   the :guilabel:`Change Icon` button
*  Search either :file:`C:\\Atlas\\` or :file:`W:\\` to find the icon file 
   :file:`arev.ico`
*  Click :guilabel:`Apply` and :guilabel:`OK` to save the changes

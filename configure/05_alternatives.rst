.. _alternatives:

#############################
Alternatives to Run WARES
#############################

The move to 64-bit Windows 7 and Windows 8 eliminates running WARES natively on 
a Windows operating system. There are other options, however. These are:
 
*  DOS emulation using :program:`DOSBox` on Windows 7 and Windows 8
*  Microsoft's 32-bit :program:`Virtual Windows XP` emulation for Windows 7
*  Remote desktop access to WARES on an ADDS Server
*  Linux Ubuntu desktop operating system, and DOSEMU

DOSBOX emulation
=============================

.. note:: 
   Instructions in this section are intended for Windows 7, and are based 
   on DOSBOX version 0.74, which is the current release as of January, 2014. 
   This configuration was tested on one Windows 7 system, where it worked on the 
   local desktop and over rdp. DOSBox does not support NETBIOS record locking 
   required for multiuser operation.

The configuration described here will run a single program in :program:`DOSBox`, 
Specifically DOS program :program:`WARES`. WARES requires a custom DOSBox 
configuration file and start icon. To run other programs, create corresponding 
additional custom configuration files and icons.

Installing DOSBox
-----------------------------

`Download DOSBox <http://www.dosbox.com/download.php?main=1>`_ from your web 
browser. In Windows, this file will probably land in the :file:`Downloads` 
folder.

*  Double-Click the installer file :file:`DOSBox0.74-win32-installer.exe` 
*  Tell Windows to :command:`Run` the software
*  At :guilabel:`DOSBox v0.74 License`, click :guilabel:`Next` to accept the 
   GNU public license terms
*  At :guilabel:`Select components to install:`, check the 
   :guilabel:`Desktop Shortcut` box, then click :guilabel:`Next` to continue 
*  At the :guilabel:`Destination Folder`, just click :guilabel:`Install` to
   use the default location :file:`C:\\Program Files\\DOSBox-0.74`  
*  Click :guilabel:`Close` to exit the installer when finished.

Configuring DOSBox
-----------------------------

.. warning:: 
   Before configuring :program:`DOSBox`, determine the directory path for the 
   program to be run. Then in the following instructions, change the token 
   :kbd:`\{path\}` to the actual directory path. For example, if program WARES
   is started from directory :file:`C:\\ATLAS\\`, replace the line 
   :kbd:`mount w \{path\}` with the text :kbd:`mount w C:\\ATLAS\\`. DOSBox 
   requires an absolute path including the drive letter for this entry.

*  At the task bar :guilabel:`Start` menu, type :kbd:`cmd <Enter>` in the search 
   box. A cmd console window should appear.
*  At the console command line, enter::
   
      cd appdata\local\dosbox
      edit wares.conf
   
*  In the text editor, enter the following configuration text for WARES::

      [sdl]
      output=overlay
      
      [render]
      scaler=2xsai forced
      
      [autoexec]
      mount w {path}
      w:
      wares wares

*  Press :kbd:`<Alt-F>, S` to save, then :kbd:`<Alt-F>, X` to exit the editor.

Configuring desktop icon
-----------------------------

*  On the desktop, :kbd:`<Right-Click>` the :guilabel:`DOSBox 0.74` icon and 
   choose menu option :menuselection:`Properties`
*  Change the :guilabel:`Target` text to read as follows::
      
      "C:\Program Files\DOSBox-0.74\DOSBox.exe" -conf "%userprofile%\appdata\local\dosbox\wares.conf" -noconsole
    
*  Test the DOSBox configuration by double-clicking the desktop icon. 
*  After quitting the program, type :kbd:`EXIT` to close the DOSBox window.
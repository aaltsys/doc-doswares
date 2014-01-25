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

The configuration described here will run a single program in :program:`DOSBox`, 
Specifically DOS program :program:`WARES`. WARES requires custom DOSBox 
configuration files and start icon. To run other programs, create corresponding 
additional custom configuration files and icons.

Using DOSBox with printers requires :command:`net use` commands to map Windows 
printers to virtual LPT devices. See :ref:`Documentation for NET USE <netuse>`.

Installing DOSBox
-----------------------------

For DOSBox with printer support, download DOSBox_SVN_daum current version
:download:`from here <../resources/_downloads/DOSBox_daum-win32-installer.exe>`.
Windows will probably save this file in your :file:`Downloads` folder.

*  Open your :file:`Downloads` folder in Windows Explorer
*  Double-Click the installer file :file:`DOSBox_daum-win32-installer.exe` 
*  In the :guilabel:`User Account Control` window, click :guilabel:`Yes` to run 
   the installer
*  At :guilabel:`License Agreement`, click :guilabel:`Next` to accept the 
   GNU public license terms
*  At :guilabel:`Select components to install:`, check the boxes for
   :guilabel:`Desktop Shortcut` and :guilabel:`Font Files`, then click 
   :guilabel:`Next` to continue 
*  At the :guilabel:`Destination Folder`, just click :guilabel:`Install` to
   use the default location :file:`C:\\Program Files\\DOSBox_SVN-daum`  
*  Click :guilabel:`Close` to exit the installer when finished.

DOSBox keyboard configuration
-----------------------------

DOSBox uses function keys for program controls. Operating System functions 
override some of these controls, so the DOSBox operations cannot work. 
Other DOSBox key mappings conflict with key assignments for applications 
running in DOSBox, and so application functions cannot work. DOSBox includes a 
control menu which makes key mappings unnecessary anyway. Therefore WARES 
provides a custom keyboard mapper file which eliminates most DOSBox function key 
mappings. This configuration is installed in the next section.

DOSBox program configuration
-----------------------------

.. warning::
   DOSBox requires configuration to work with WARES.

.. sidebar:: DOSBox WARES Configuration 
   
   ::
   
      [sdl]
      windowresolution=960x600
      output=overlay
      autolock=false
      mapperfile=dosbox-wares.map
      
      [cpu]
      cycles=fixed 6000

      [joystick]
      joysticktype=none
      
      [printer]
      printout=printer
      
      [parallel]
      parallel1=file dev:lpt1
      parallel2=file dev:lpt2
      
      [autoexec]
      mount w {path}
      w:
      wares wares

Before configuring :program:`DOSBox`, determine the directory path for the 
program to be run. Then in the following instructions, change the token 
:kbd:`\{path\}` to the actual directory path. For example, if program WARES is
started from directory :file:`C:\\ATLAS\\`, replace the line 
:kbd:`mount w \{path\}` with the text :kbd:`mount w C:\\ATLAS\\`. DOSBox 
requires an absolute path including the drive letter for this entry.

*  Download the following files to your :file:`Downloads` folder:

  | :download:`dosbox-wares.conf <../resources/_downloads/dosbox-wares.conf>` 
  | :download:`dosbox-wares.map <../resources/_downloads/dosbox-wares.map>`

*  At the task bar :guilabel:`Start` menu, type :kbd:`cmd <Enter>` in the search 
   box. A :command:`cmd` console window should appear.
*  At the console command line, copy the files with the following commands::

      md AppData\Local\DOSBox
      copy Downloads\dosbox-wares.* appdata\local\dosbox
      edit dosbox-wares.conf

*  In the text editor, change the configuration line ``mount w {path}`` to 
   represent the path to your WARES files.
*  Press :kbd:`<Alt-F>, S` to save, then :kbd:`<Alt-F>, X` to exit the editor.

Configure desktop icon
-----------------------------

*  On the desktop, :kbd:`<Right-Click>` the :guilabel:`DOSBox SVN-daum` icon and 
   choose menu option :menuselection:`Properties`
*  Change the :guilabel:`Target` text to read as follows::
      
      "C:\Program Files\DOSBox SVN-Daum\DOSBox.exe" -conf "%userprofile%\AppData\Local\DOSBox\dosbox-wares.conf" -noconsole
    
*  Test the DOSBox configuration by double-clicking the desktop icon. 
*  After quitting the program, type :kbd:`EXIT` to close the DOSBox window.

.. note:: 
   (1) Instructions in this section are based on DOSBox_SVN_Daum, an extended 
   version of DOSBox official release 0.74. 
   
   (2) This configuration worked on Windows 7 system at the local desktop and 
   over rdp. 
   
   (3) DOSBox does not have native support for NETBIOS record locking as is 
   required for multiuser operation.
   
   (4) DOSBox local configuration files are saved at: 
   :file:`\%userprofile\%\\appdata\\local\\dosbox\\`. 

.. _downloads:

#############################
Downloads
#############################

WARES
=============================

DOS Command Files
-----------------------------

:download:`wares.pif <_downloads/WARES.pif>` desktop .pif file to start WARES.

:download:`wares.bat <_downloads/wares.bat>` revised to work with EMSmagic and 
netprint.bat.

:download:`netprint.bat <_downloads/netprint.bat>` revised sample printer 
sharing batch file.

:download:`netshare.bat <_downloads/netshare.bat>` revised sample file sharing 
batch file.

:download:`rdpprint.bat <_downloads/rdpprint.bat>` sample file for remote 
printer sharing.

Update Patches files
-----------------------------
   
:download:`Update patches to WARES 4.50E: <_downloads/patches.zip>`

Determine your WARES working directory:

#. Start WARES from your desktop, using your supervisor level login
#. Press :kbd:`F5` to display the :guilabel:`Command-WARES` window
#. Type :kbd:`PC <enter>` to show the DOS system command window
#. The command window last line displays your working directory, followed by a 
   :kbd:`>` symbol. Typical working directory is :file:`C:\\ATLAS`` or 
   :file:`W:\\`.
#. Type :kbd:`EXIT` to leave the DOS command window
#. Press :kbd:`esc` to leave the :guilabel:`Command-WARES` window

Install patches as follows:

.. note:: Where the following instructions show :file:`\{working directory\}`,
   substitute the working directory from the previous section, typically 
   :file:`W:` or :file:`C:\\ATLAS`.

#. Delete all files in directory :file:`\{working directory\}\\PATCHES`
#. Download archive file :file:`patches.zip`
#. In :guilabel:`My Computer`, Right-click :file:`Downloads\\patches.zip` and 
   chose :menuselection:`Extract all ...`
#. Follow the wizard directions, saving the files to directory 
   :file:`\{working directory\}\\PATCHES` when prompted
#. Login to WARES
#. From menu selection :menuselection:`Tools --> Utilities --> Bundle`, install 
   patches from volume :file:`PATCHES`, choosing whichever file is needed

Evaluation copy of 4.50E
-----------------------------

:download:`Download a demo version of WARES 4.50E <_downloads/waresdem.exe>`
   
Install this program at a Windows command prompt with the following commands::

   cd %USERPROFILE%\Downloads
   md .\waresdem
   waresdem.exe .\waresdem
   cd waresdem
   install c:

EDI Standards packages
=============================

The following EDI standards table data are available for download:

|  :download:`5010x12.exe <_downloads/5010x12.exe>` and
   :download:`5010x12.alm <_downloads/5010x12.alm>`
|  :download:`4010x12.exe <_downloads/4010x12.exe>` and 
   :download:`4010x12.alm <_downloads/4010x12.alm>`
|  :download:`3070x12.exe <_downloads/3070x12.exe>` and 
   :download:`3070x12.alm <_downloads/3070x12.alm>`
|  :download:`3060x12.exe <_downloads/3060x12.exe>` and 
   :download:`3060x12.alm <_downloads/3060x12.alm>`

Install these packages with the WARES update installer, as follows:

#. In MyComputer, create a folder at the root of drive C:, :file:`C:\\TEMP`. If 
   this directory exists already, delete any files within it.
#. Download a standards archive executable and the matching .alm instructions,
   saving the files in folder :file:`C:\\TEMP`.
#. From WARES menu selection :menuselection:`Tools --> Utilities --> Update`, 
   install the updates from file path :file:`C:\\TEMP`.


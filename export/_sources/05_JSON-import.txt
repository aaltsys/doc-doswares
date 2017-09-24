.. _JSON-import:

#############################
JSON Import Implementation
#############################

.. note::
   In the following documentation, replace the terms **{JSONshare}** and 
   **JSONshare** with the corresponding folder name in DropBox that is used for 
   file exchange.

Update Windows Workstations
=============================

Although WARES runs entirely from a server fileshare, using Dropbox for file 
exchange will require administrative changes for each computer or user who will 
perform a Dropbox exchange.

Mount Dropbox in User Space
-----------------------------

For every user requiring access to a Dropbox share, follow this link to the `Dropbox installer <https://www.dropbox.com/install>`_ to add Dropbox to their 
user path.

.. _JSON-integrate-view:

View or Setup JSON Share
-----------------------------

Open Windows File Explorer to view the contents of your Dropbox directory. 
Identify the {JSONshare} foldername which will be used for JSON orders 
exchange. Verify the contents of this folder. The following directory tree is 
required::

 ┌─────────────────────────────────────────────────────────────────────────┐
 │                       ┌────────────┐                    ┌────────────┐  │
 │                     ┌─┤  Folder 1  │                  ┌─┤  HISTORY   │  │
 │                     │ └────────────┘   ┌────────────┐ │ └────────────┘  │
 │                     │     . . .      ┌─┤  ORDERS    ├─┤ ┌────────────┐  │
 │                     │ ┌────────────┐ │ └────────────┘ └─┤  STREAMS   │  │
 │ User\Name\Dropbox\ ─┼─┤ JSONshare  ├─┤                  └────────────┘  │
 │                     │ └────────────┘ │ ┌────────────┐   ┌────────────┐  │
 │                     │     . . .      └─┤  SHIPPERS  ├───┤  HISTORY   │  │
 │                     │ ┌────────────┐   └────────────┘   └────────────┘  │
 │                     └─┤  Folder n  │                                    │
 │                       └────────────┘                                    │
 └─────────────────────────────────────────────────────────────────────────┘

.. note::
   You can move a folder tree from your local drive to Dropbox using File 
   Explorer. Right-drag the folder to Dropbox and select "Move here" to create 
   the share. Then setup sharing in Dropbox to configure the folder, or you 
   could use the following command::
   
      move "C:\path\to\folder" "%userprofile%\Dropbox"

Commands to Link a Folder
-----------------------------

Search for :command:`CMD.EXE` on your start menu, and right-click to select 
"Run as Administrator." In the DOS command window, type the following commands 
to set a permanent link to a shared Dropbox folder: [#]_ ::

   mkdir C:\Dropbox
   mklink /J "C:\Dropbox\{JSONshare}" "%userprofile%\Dropbox\{JSONshare}"
   dir C:\Dropbox\{JSONshare}

.. note::
   The :command:`mklink` command works with WINDOWS Vista and higher, and 
   Windows must have been installed using file system NTFS. Links may also be 
   created with the command::

      fsutil hardlink create "C:\Dropbox\{JSONshare}" "%userprofile%\Dropbox\{JSONshare}"

   If you are using WindowsXP it is probably time for an upgrade. Call for 
   advice on Windows upgrades.

Add JSON Import to WARES
=============================

Add JSON Import Features
-----------------------------

Use the instructions from topic :ref:`patches` to install patch sets **JSON** 
and **JSONIMPORT**. WARES will also require account customization as described 
following. (These changes may be forwarded in site-specific patch sets.)

Configure WARES Pathnames
-----------------------------

WARES saves import and export configuration data in control records. Use menu 
selections :menuselection:`eXchange --> Export-Import --> Exports` and 
:menuselection:`eXchange --> Export-Import --> JSON Imports` to access control 
records and change path settings.

+--------------+--------------------+------------------------------------------+
| Control Name | Entry Label        | Entry values to check                    |
+==============+====================+==========================================+
|| JSONIMPORT  || Export FileName   || null                                    |
|| ORDERS      || Export Directory  || C:\\DROPBOX\\{share}\\ORDERS\\          |
||             || History Directory || C:\\DROPBOX\\{share}\\ORDERS\\HISTORY\\ |
+--------------+--------------------+------------------------------------------+
|| EXPORT      || Export FileName   || {PO_NUMBER}                             |
|| JSONSHIPPERS|| Export Directory  || C:\\DROPBOX\\{share}\\SHIPPERS\\        |
||             || History Directory || null                                    |
+--------------+--------------------+------------------------------------------+

The control names given above are generic; actual control record names will be 
different and unique for each account. Replace {share} with an account ID and
append the account identifier to the control name to generate these controls. 
For example, account-specific controls for account **ABC** might be 
**JSONIMPORT\*ORDERS_ABC** and **EXPORT\*JSONSHIPPERS_ABC**.

.. tip::
   Menu selection :menuselection:`Tools --> Define --> Controls` may be used to 
   edit import controls (and any other controls) just as selections on the 
   :menuselection:`eXchange --> Export-Import` menu are used.

Add WARES Process Selections
-----------------------------

JSON orders import includes new processes **JSONIMPORT_ORDERS** and 
**EXPORT_JSONSHIPPERS** to import orders and create response documents. Custom 
versions of these processes are needed for each participating account. Use menu 
item :menuselection:`Tools --> Processes --> Processes Setup` to create the new
processes, as described here:

*  Display the :guilabel:`Processes` window from the menu.
*  Retrieve the first process, **JSONIMPORT_ORDERS**, then rename the process 
   by appending the account ID: for example, **JSONIMPORT_ORDERS_ABC**. Press 
   :kbd:`<return>` to start the new record.
*  Press :kbd:`<Alt-C>, <return>` to copy the last-displayed record into the 
   new record.
*  Change the :guilabel:`Execution` command to use the control name from the 
   previous section; that is, **ORDERS_ABC** instead of **ORDERS**. Change the 
   process title to reflect the customer account, as you will see this title in 
   the selection options.
*  Save the process.
*  Repeat the previous steps for process **JSON*EXPORTSHIPPERS**, where the 
   control name might be **JSONSHIPPERS_ABC** instead of just **JSONSHIPPERS**.

The options list at :menuselection:`eXchange --> Export-Import --> Processes` 
should be used to list these account-specific process choices, as follows:

*  At menu item :menuselection:`Tools --> Define --> Popups`, enter 
   :guilabel:`File name` **POPUPS** and :guilabel:`Popup name` **ECOM_PROCESS**
   to display the exchange processes list. 
*  Add process names created above to the process list, and save the changes.

WARES Uses Short Filenames
=============================

Windows has two file naming conventions: upper-cased 8-character short names, 
and 256-character case-sensitive long names. File operations may be performed 
using either the short name or the long name, as directory entries track both 
names. Using short names, when a file operation results in a name collosion, 
new files may overwrite previous files, resulting in data loss.

WARES performs file operations using 8-character short filenames. This is not 
a problem when using local files with distinct long names, because Windows 10
creates unique short names, as shown here::

   Directory of W:\ATLAS\IMPORT\ORDERS\HISTORY

   09/20/2017  03:55 PM    <DIR>                       .
   09/20/2017  03:55 PM    <DIR>                       ..
   09/20/2017  03:55 PM             1,149 3SUZMY~X.JSN 30000000223.JSN
   09/20/2017  03:55 PM               889              14915.JSN
   09/20/2017  03:55 PM               829 3927GZ~4.JSN 30000000104.JSN
   09/20/2017  03:55 PM               844              14921.JSN
   09/20/2017  03:55 PM             1,329 1MUCJR~M.JSN 30000000022.JSN
                  5 File(s)          5,000 bytes

Files linked to a Dropbox share use a different protocol for generating short 
filenames. The first 6 digits of the filename are followed by a tilde (~) and
then a single digit from 1 to 9. Sequenced filenames longer than 8 characters 
will have short name collisions, and WARES file operations on the short names 
will result in data loss. This is illustrated with the directory listing below, 
where the same file list has been run through Dropbox::

   Directory of C:\DROPBOX\SHARED\ORDERS\HISTORY

   09/21/2017  11:03 AM    <DIR>                       .
   09/21/2017  11:03 AM    <DIR>                       ..
   09/21/2017  11:03 AM             1,149 300000~1.JSN 30000000223.JSN
   09/21/2017  11:03 AM               889              14915.JSN
   09/21/2017  11:03 AM               829 300000~2.JSN 30000000104.JSN
   09/21/2017  11:03 AM               844              14921.JSN
   09/21/2017  11:03 AM             1,329 300000~3.JSN 30000000022.JSN
                  5 File(s)          5,000 bytes

.. warning::
   During file exchange, WARES requires unique filenames of 8 or fewer 
   characters to guarantee that data will not be lost.

WARES Stores Paths to Shares
=============================

For operational simplicity and reliability, WARES automates exchange processes 
by saving absolute file paths to directories on network shares. Dropbox cannot 
synchronize files mapped to network shares reliably; it can only synchronize 
with local file folders.

This presents some issues. First, multiuser WARES runs entirely from a network 
share. Second, Dropbox installs itself on the local user's directory path, and 
this path is different for every user. Third, Dropbox needs directories to be 
linked from the local user's system to the mounted Dropbox folders.

-----

.. rubric:: footnotes

.. [#] https://www.howtogeek.com/howto/16226/complete-guide-to-symbolic-links-symlinks-on-windows-or-linux/

.. DOS WARES Website Index, by sphinx-quickstart on Thu Mar 21 14:34:22 2013.

DOS WARES Site
=============================

DOS WARES has extensive user documentation integrated into the program, through 
the :menuselection:`Access --> Manuals` selections and the :kbd:`<F1>` and 
:kbd:`<Ctrl-F2>` key presses at all points in the program. Different from that 
sort of program documentation, this site covers issues with program execution 
on various Windows and other platforms.

WARES Multiuser Servers
=============================

A separate website, `AAltsys Servers <http://servers.aaltsys.info>`_, is 
dedicated to WARES server software and hardware.

Briefly, in a multiuser environment, WARES requires a server to host program 
files which are shared to users. Beneath WARES, the DOS-based 
:program:`Advanced Revelation` database performs sharing and record-locking 
services using Microsoft SMBv1 networking protocols. Microsoft has deprecated 
SMBv1 in current versions of Windows 10, so we sell an alternative server which 
does support these network protocols. The WARES server is a turnkey package of 
Apple Mac mini hardware hosting the Ubuntu Linux-based :program:`Zentyal Server` 
package.

vDosPlus Alternative to DOS
-----------------------------

Due to Microsoft's negligence, Windows has many barriers to executing DOS 
programs such as WARES. Many developers have worked on these problems, and as a 
result there is now an excellent tool for addressing Windows/DOS issues:

:ref:`vdosplus`.

Configuration
-----------------------------

Where WARES is running in a 32-bit Windows environment with only one or two 
configuration issues, some of these topics are addressed here: 

:ref:`configure:index`.

Support Documents
-----------------------------

Specific WARES problems are addressed at :ref:`support:index`.

Data Export Mapping
-----------------------------

The export mapper at :menuselection:`eXchange --> Export/import --> Exports` 
can define flat-file and structured text exports of WARES data records. WARES
can export individual records, selected groups, or entire files (tables), and 
exports may be batched, or be selected during printing, or be triggered when
transactions are saved. The Export Mapper can write JSON documents to interface 
DOSWARES with web applications. 

For details, see :ref:`export:index`.

JSON Orders Import 
-----------------------------

Part of export development has produced a JSON orders import for orders 
exchange with accounts. Implementation details are at :ref:`JSON-import`.

Resources
-----------------------------

:ref:`resources:downloads`

This page consolidates the various DOS support files for WARES, including:

+  Batch execution files
+  Program patch updates
+  A demo copy of WARES Warehousing
+  EDI standards table data

+  :ref:`resources:upd-450e`

+  Upgrade files and instructions to convert from version 4.34B to 4.50E

.. toctree::
   :maxdepth: 0

---

:ref:`search`


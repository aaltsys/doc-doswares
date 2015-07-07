.. _intro:

#############################
DOS WARES Export Mapper
#############################

DOS WARES is capable of writing flat-file and structured exports of individual 
transaction records, selected database cursors, and entire tables (files).

From menu selection :menuselection:`eXchange --> Export-Import --> Exports`, 
export maps may be defined to write masterfile and transaction text data in 
specialized formats, such as

*  JSON structured documents (.JSN).
*  QUICKBOOKS import format (.IIF).

Executing an Export
=============================

Export maps define both the structure of the exported data and the method for 
naming and locating the exported files. Demand exports are executed through the 
:program:`EXPORTDATA` command, which is usually managed through a control record 
for either a :program:`PROCESS` or a :program:`REPORT`.

WARES posting controls can generate transaction exports using database triggers. 
This alternative to demand exports will create export files from database 
activity without user interaction.

Add JSON Exporting to WARES
=============================

The WARES 450 patches bundle has been updated to include JSON exports. Use the 
patch instructions from :ref:`resources:patches` to install the :file:`JSON`
datafile from the patches. This bundle includes:

*  Revised programs :program:`EXPORTDATA` and :program:`POST_EXPORTDATA`.
*  Updated mapper window :program:`CTL_EXPORT` with added JSON features.
*  Export maps for setup files :file:`ADDRESSES`, :file:`ACCOUNTS`, and 
   :file:`PRODUCTS`.
*  Export maps for inventory transactions: :file:`RECEIPTS`, :file:`SHIPMENTS`, 
   :file:`ADJUSTS`, :file:`HISTORY`, :file:`DETAILS`, :file:`DETAIL_HISTORY`.
*  Export maps for billing files: :file:`TARIFFS`, :file:`CHARGES`,
   :file:`INVOICES`, and :file:`PAYMENTS`.
*  Dictionary updates adding fieldnames required for JSON exports.
*  Process records to perform batch exports of the files previously listed. 

.. note::
   For interactive export of transactions, changes to control records 
   :file:`POST_RECEIPTS`, :file:`POST_SHIPMENTS`, and :file:`POST_ADJUSTS` 
   to export transactions using database triggers.

.. note::
   On-line WARES documentation is not updated to explain JSON exporting or the 
   steps for transaction exporting as reports or through posting controls.

.. _execution:

Batch Export Processes
=============================

Transaction Export Reports
=============================

Database Trigger Exports
=============================

Export program :program:`POST_EXPORTDATA` is called from the file posting 
controls to perform exports automatically based on database actions. 
Implement an automatic transaction export as follows.

#. At :menuselection:`Tools --> Define --> Controls` enter a control 
   :guilabel:`Type` of :kbd:`POST` and enter a WARES filename such as 
   :file:`SHIPMENTS` in the :guilabel:`Identifier`. The current posting 
   control will display.
#. Select a location for the export call, and press :kbd:`<Ctrl-N>` to enter a 
   new line. Use the program name :program:`POST_EXPORTDATA`, and an export
   control identifier in the :guilabel:`Branch` column. 
#. Fill in the :guilabel:`Test`, :guilabel:`Value`, and :guilabel:`Occur` 
   entries to determine the rule or condition which will trigger the export.
   For example, *Test=GT*, *Value=1*, *Occur=Always* will write posted 
   transactions and update the exported file with each change.

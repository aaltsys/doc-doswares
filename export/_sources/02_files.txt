.. _files:

#############################
Export Files
#############################

Transaction Exports
=============================

When the :guilabel:`Export FileName` entry on an export map is left blank, 
selected records will be exported into individual files named by the WARES 
record key. A separate folder or directory should be used for each WARES file 
which is exported, and file system paths should conform to the 8-character 
naming limitations of DOS. Similarly, only the left-most 8 characters of a 
record key will be used as a filename during the export.

Due to the similarity of Report and Process functionality in WARES, transaction 
export commands may be executed as report forms, callable from the report group 
popups within windows and from menus. This allows records to be exported 
selectively as a step in data entry.

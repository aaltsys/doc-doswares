.. _json:

#############################
JSON Transaction Formatting
#############################

JSON encoding is enabled by control header settings for delimiters and 
preprocess, and special control and value entries in the export map details. 

Export map heading settings
=============================

The following table lists recommended settings for JSON in the export
map heading fields. 

+--------------+-----------+------------------+
| Entry        | JSON      | Char             |
+==============+===========+==================+
| Delim Table  | (blank)   |                  |
+--------------+-----------+------------------+
| Delim Row    | 0A        | \\n (NL)         |
+--------------+-----------+------------------+
| Delim Column | 0A        | \\n (NL)         |
+--------------+-----------+------------------+
| Delim Value  | 3A20      | : (colon/space)  |
+--------------+-----------+------------------+
| Delim Quote  | 22        | " (quote)        |
+--------------+-----------+------------------+
| Preprocess   | JSON,32,2 | 32=space, 9=tab  |
+--------------+-----------+------------------+

.. note::
   Delimiters show characters by hex value, but the preprocess JSON command
   requires the white-space character value to be expressed in decimal instead.

Export map detail entries
=============================

There are just seven entry patterns for a JSON encoding. Three of these produce 
opening or closing brackets "[]" and braces "{}", and two more patterns provide
labeled brace and bracket lines. The remaining two lines are the standard data 
lines for static values or data values, but with name labels in the Heading 
column.

+---------+---------+-------+--------+---------+--------+-----------------------------+
| Heading | Control | Value | Field  | Command | Format | Result                      |
+=========+=========+=======+========+=========+========+=============================+
| (blank) | JSON    | {     |         (blank)           | { ; \\n ; indent +=         |
+---------+---------+-------+--------+---------+--------+-----------------------------+
| label   | JSON    | {     |         (blank)           | "label": { ; \\n, indent += |
+---------+---------+-------+--------+---------+--------+-----------------------------+
| label   | JSON    | [     |         (blank)           | "label": [ ; \\n, indent += |
+---------+---------+-------+--------+---------+--------+-----------------------------+
| label   |         | value |         (blank)           | "label": "value", ",", \\n  |
+---------+---------+-------+--------+---------+--------+-----------------------------+
| label   |         | value | name   | command |        | "label": "@ANS", ",", \\n   |
+---------+---------+-------+--------+---------+--------+-----------------------------+
|         | JSON    | ]     |         (blank)           | ], ; indent -=              |
+---------+---------+-------+--------+---------+--------+-----------------------------+
|         | JSON    | }     |         (blank)           | }, ; indent -=              |
+---------+---------+-------+--------+---------+--------+-----------------------------+

Recommended Configurations
=============================

#. Uordered list entries will be suppressed when a :guilabel:`Field name` 
   returns null.
#. Arrays containing static :guilabel:`Value` entries will omit corresponding 
   :guilabel:`Field` entries where the *Field* result is null.
#. If a :guilabel:`Value` and a :guilabel:`Field name` are entered on the same 
   line, the *Value* will be returned as a default if *Field* has a null result. 
   JSON expects a *Value* of **null** for blank field entries in arrays.
#. Text entry lines in the WARES database are delimited with @VM, @ASVM, or @TM. 
   JSON does not recognize these delimiters, and line ending characters are not 
   permitted in JSON data. JSON exports will change these delimiters to escaped
   newline symbols (\\n) wherever text may be multiline.

Character representations
=============================

The following characters will be escaped with preceding back-slashes when 
embedded in JSON data:

+------+------------------+---------+------+
| Char | Description      | Hex     | Dec  |
+======+==================+=========+======+
| \\   | reverse solidus  | \\5C\\  |  92  |
+------+------------------+---------+------+
| \/   | solidus (slash)  | \\2F\\  |  47  |
+------+------------------+---------+------+
| \"   | quotation mark   | \\22\\  |  34  |
+------+------------------+---------+------+
| \\b  | backspace        | \\7F\\  | 127  |
+------+------------------+---------+------+
| \\f  | form feed        | \\0B\\  |  11  |
+------+------------------+---------+------+
| \\n  | new line         | \\0A\\  |  10  |
+------+------------------+---------+------+
| \\r  | carriage return  | \\0D\\  |  13  |
+------+------------------+---------+------+
| \\t  | horizontal tab   | \\09\\  |   9  |
+------+------------------+---------+------+

JSON format description
=============================

JSON describes a data set with unordered lists of descriptor/value pairs 
enclosed in braces ({}), and ordered arrays of descriptor/value pairs enclosed 
in brackets ([]). For readability, nested groups of elements are indicated by
indentation using white space (spaces). Documentation of JSON standards is 
available at http://json.org/. An example portion of a shipment record is shown
following:

.. code-block:: JSON

   {
     "references": [
       {
         "referenceCode": "CO", 
         "reference": "5343463643"
       },
       {
         "referenceCode": "PO", 
         "reference": "INV450470452"
       },
     ],
   }


.. _bill-packs:

#############################
Mandatory Picking Charge
#############################

DOS WARES does not seem to have a way to calculate number of separate cases or 
packages picked when shipping both full pallets and picked cases. Similarly, 
there is not an obvious way to automate the calculation and billing of case 
picking fees.

BUT! WARES has very flexible programming which allows the calculation and 
billing of case picking to be added quite simply. Just follow this guide.

Adding Case Pick Quantity
=============================

Adding the case pick quantity for billing means adding a symbolic entry to the 
shipments dictionary. Here is how:

#. Go to menu selection :menuselection:`Tools --> Reports --> Dictionary Edit`.
#. Enter :guilabel:`Table name` = **SHIPMENTS** and :guilabel:`Column name` = 
   **BILL_PARTIAL**. A record will display as shown following:
   
   .. image:: _images/dict-bill_partial.png
   
#. :kbd:`up-arrow` to the :guilabel:`Column name`, and enter the new name 
   **BILL_PACKS**. The window will clear to create a new dictionary item.
#. Press :kbd:`Alt-C` to copy the previous information into the new entry 
   for **BILL_PACKS**.
#. Press :kbd:`Enter` until the cursor is in the :guilabel:`Formula` entry.
   Press function key :kbd:`F3` to expand the formula for editing. The 
   original formula will display:
   
   .. image:: _images/dict-code-bill_partial.png
   
#. Use the mouse or arrow keys to move around the edit window, and change the 
   last four lines to read as shown highlighted in the following image:
   
   .. image:: _images/dict-code-bill_packs.png
   
   .. tip::
      If you accidentally press :kbd:`Enter`, place the cursor on the 
      resulting blank line and press :kbd:`Ctrl-D` to remove the line.
   
#. Press keys :kbd:`F9` and :kbd:`Esc` to save the changed formula 
   and exit the edit subwindow.
#. Change the :guilabel:`Column heading` = **Packs** for the new dictionary, 
   then press :kbd:`F9` to save the entry.

Verify the Dictionary Entry
=============================

Enter the :guilabel:`Column name` **BILL_PACKS** again and press 
:kbd:`Enter` to redisplay the Dictionary entry. Enter to the 
:guilabel:`Formula`, press :kbd:`F3` to display the formula and read the 
changes to verify them. If everything is good, press :kbd:`Esc Esc` to 
exit the dictionary window.

Adding Case Pick Billing
=============================

#. Display the window at :menuselection:`Billing --> Tariffs Setup`. 
#. Enter a new tariff :guilabel:`Identifier` and :guilabel:`Code` to start a 
   new rate, :guilabel:`Applied` **Mandatory**.
#. On the new rate record, enter the :guilabel:`Table Name` and 
   :guilabel:`Per Code` exactly as shown in the following image:
   
   .. image:: _images/tariff-bill_packs.png
   
#. Complete the :guilabel:`Rate`, :guilabel:`Quantity`, and :guilabel:`Minimum` 
   Fields and press :kbd:`F9` to save the new rate.

Verifying Case Pick Billing
=============================

As with any mandatory charge, go to the :menuselection:`Entry --> Shipments` 
window, and enter or display a shipment record which will require this charge. 
The shipment must be saved with :guilabel:`Status` **2** or **3**.

#. Change the shipment record :guilabel:`Status` to **4**, press :kbd:`F9`.
#. Press :kbd:`Alt-O, Enter` to redisplay the record, and then press
   :kbd:`F3` to bring up the charges.
#. Check that the case picking charge is on the list of calculated charges.
#. Press :kbd:`Esc` to remove the charges subwindow, then change the 
   :guilabel:`Status` back to **2** or **3** and save the record again to 
   restore the state of the shipment.

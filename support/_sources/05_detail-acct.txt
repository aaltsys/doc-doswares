.. _detail-acct:

#############################
Lot Detail Account Mismatch
#############################

Adjustments are used to transfer product between accounts. If the account 
identifier on an adjustment is not the recipient for the transfer, then lots 
created by the adjustment will be assigned to the wrong account. Use these 
instructions to correct the account on lots.

Preliminary Requirements
=============================

Before this correction is run the first time, two entries must be added to 
WARES design to identify incorrect lot accounts.

Dictionary LOT_ACCOUNT
-----------------------------

At menu selection :menuselection:`Tools --> Reports --> Dictionary`, add an 
entry for the :file:`DETAILS` table, column :file:`PROD_ACCOUNT`, as shown in 
the following screenshot:

.. image:: _images/PROD_ACCOUNT.png

.. tip::
   The code expansion is shown by pressing :kbd:`<F3>`. Use :kbd:`<F9>` to save 
   and :kbd:`<Esc>` to exit the expanded view, then save the dictionary record 
   by pressing :kbd:`<F9>` again.

Report DETAIL.PROD-ACCT
-----------------------------

At menu selection :menuselection:`Tools --> Processes --> Report Setup`, add a 
new report :file:`DETAIL.PROD-ACCT` as shown in the following screenshot:

.. image:: _images/DETAIL.PROD-ACCT.png

Correcting Lot Accounts
=============================

There are two simple steps to correct account mismatches on lots.

Report Lot Account Mismatches
-----------------------------

Run report :menuselection:`Reports --> Miscellaneous --> DETAIL.PROD-ACCT`, 
viewing the output. If and only if lots are displayed on the report, escape from 
the report viewer and proceed directly to the next step.

Fix Lot Account Mismatches
-----------------------------

.. warning::
   The :program:`COPYCOL` utility can make irreversible changes to your data 
   system. Do not use this utility without technical support unless you are 
   absolutely certain about what you are doing.

From menu selection :menuselection:`Tools --> General --> Copy Columns`, enter 
the following command information:

+---------------------+------------------------------+
| File Name           | DETAILS                      |
+---------------------+------------------------------+
| Source Data         | PROD_ACCOUNT                 |
+---------------------+------------------------------+
| To Field            | ACCOUNT                      |
+---------------------+------------------------------+

Press :kbd:`<F9>` to continue to the :guilabel:`Browse Selections` list, and 
select (press :kbd:`<Enter>`) :menuselection:`Query Table`. If the top line of 
the :guilabel:`Stored Query Table` says *SELECT DETAILS WITHOUT ACCOUNT EQ 
PROD_ACCOUNT ...* and has the correct number of hits, then press :kbd:`<Enter>`, 
otherwise press :kbd:`<Esc>` and start over.

Finally, you should see the :guilabel:`Copy Columns` confirmation message. it
must read:

+---------------------+------------------------------+
| Using File:         | DETAILS                      |
+---------------------+------------------------------+
| From Field =        | PROD_ACCOUNT                 |
+---------------------+------------------------------+
| To column =         | ACCOUNT                      |
+---------------------+------------------------------+
| Match Value =       |                              |
+---------------------+------------------------------+

If everything is correct, enter :kbd:`Y <Enter>` to change the lot account.

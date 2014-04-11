.. _cu-mfs:

#############################
 Customer Access
#############################

.. note::
   Operating system considerations for local and remote access to WARES are not 
   discussed in this article. Remote access to WARES using a secure terminal 
   server is explained at http://servers.aaltsys.info/install/07_aadserver.html.

WARES includes an extensive user access security security system, which allows 
reliable customer connection to a WARES system while protecting confidentiality 
and security of data. These protections consist of four parts:

*  Operating System user login control from local and remote computers,
*  Database-level document access controlled by WARES user account,
*  Application menu selection access control by WARES user, and
*  Access level and posting process restrictions by WARES user.

The following guide describes the most-restrictive configuration of access 
security, intended for customer access to a single WARES account. Menu 
selections and data entry are restricted to a minimum to prevent confusion. The 
following information is important for using this guide:

*  A SYSPROG password is required. Call support for this information.
*  Data access is restricted by WARES account identifier. Throughout these
   instructions, replace text **{ACCTID}** with an actual WARES account id.
*  The **{ACCTID}** used below must start with a letter. If the actual WARES 
   account identifier is numeric, then insert a letter in front to make an 
   **{ACCTID}** meeting this requirement. Then in the User Logon Setup step 6, 
   fields 3, 4, and 5 would be just the WARES numeric account identifier.
   
WARES User System Setup
=============================

.. note::
   Step 6 uses Security Level :kbd:`5`, which is equivalent to WARES status 
   :kbd:`1 (reserved)`. Security levels are shown following:
   
   +-----------------+-----------------+
   | Security level  | WARES Status    |
   +=================+=================+
   | 5               | 1 (reserved)    |
   +-----------------+-----------------+
   | 4               | 2 (posted)      |
   +-----------------+-----------------+
   | 3               | 3 (verified)    |
   +-----------------+-----------------+
   | 2               | 4 (billed)      |
   +-----------------+-----------------+
   | 1               | 5 (closed)      |
   +-----------------+-----------------+

.. note::
   #. Step 7 of the System Setup below imposes a restricted menu on the user. 
      Replace :kbd:`CU_ENVIRONMENT` with :kbd:`WARES_ENVIRONMENT` in the command 
      at this step to use the full system menu. 
   #. The option :kbd:`(O)` in parentheses is capital letter :kbd:`O`, not 
      number :kbd:`0`.

#. At the WARES top menu, press :kbd:`<F2>` to see :guilabel:`Available Menus`.
   Select menu :menuselection:`STARTUPAPP`.
#. Choose :menuselection:`Open` to display the :guilabel:`Open Application`
   dialog, and enter Name :kbd:`SYSPROG`.
#. Enter the Sysprog password ____________________ when prompted for it, and
   Press :kbd:`<Enter>` to dismiss the message about missing menu ``MENU``.
#. Enter :kbd:`RUNMENU STARTUPCONFIG` and :kbd:`<Enter>` at the 
   :guilabel:`Command` window.
#. Select :menuselection:`User` from the Config menu, and fill in the options::
   
      Name         {ACCTID}
      Application  WARES
      Password     (leave blank)

#. Press :kbd:`<F10>`, then :kbd:`A` to select :menuselection:`Advanced` from
   the window. Fill in fields::
   
      Startup Command  (leave blank)
      Environment      {ACCTID}
      Security Level   5

#. Press :kbd:`<F9>, <F9>, <Esc>, <Esc>` to save the new user and return to the
   WARES command line.

#. Type the command::
   
      COPYROW SYSENV CU_ENVIRONMENT TO: {ACCTID}_ENVIRONMENT (O)

#. Type :kbd:`OFF` and :kbd:`<Enter>` to quit WARES.

WARES User Logon Setup
=============================

#. Start WARES from a user login, and logon at the supervisor access level. 
#. Choose :menuselection:`Tools --> Define --> Controls` from the menu. 
#. Press :kbd:`<F10>, F` and select filename :menuselection:`UTIL_CONTROLS`.
#. Enter the control record key fields::
   
      Type        LOGON
      Identifier  {ACCTID} 

#. Press :kbd:`<Esc>` to leave the Logon Setup Control window. 
#. Fill in fields 1 through 5 as follows::
   
      Field 1:  WARES 
      Field 2:  WARES.DATA (or other volume identifier)
      Field 3:  {ACCTID}
      Field 4:  {ACCTID} 
      Field 5:  {ACCTID}

#. Press :kbd:`<F9>` to save. Then logoff with :menuselection:`Access --> Quit`.

Testing the login
=============================

WARES must be started from a :file:`.pif` file. 

#. Using a WARES workstation, <Right-click> the existing :file:`WARES.pif` 
   desktop icon and choose :menuselection:`Copy`, then <Right-click> a blank 
   spot on the desktop and choose :menuselection:`Paste`.
#. <Right-click> the :file:`Copy of WARES.pif` you just created, and choose
   :menuselection:`Properties`, then select tab :menuselection:`Program`.
#. The Program tab :guilabel:`cmd:` line will contain text such as 
   :kbd:`WARES.BAT WARES` or :kbd:`ATLAS.BAT USER00`. Replace the word following 
   :kbd:`.BAT` with the :kbd:`{ACCTID}` for the new WARES user.
#. Click :guilabel:`Apply` and :guilabel:`OK` to close the Properties dialog.
#. <Double-click> the :file:`Copy of WARES.pif` to start the WARES program.
#. A restricted WARES menu for the user should display the following keywords: 
   
      Products  Receipts  Orders  Shipments  Lots  -Reports  Quit 

#. Display the :menuselection:`Products` window, then press :kbd:`<SF10>` to 
   list products. Only products for this one customer should display. 
#. When finished viewing, choose :menuselection:`Quit` from the menu to exit 
   WARES. 


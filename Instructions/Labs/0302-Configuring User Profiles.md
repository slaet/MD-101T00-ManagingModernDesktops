# Practice Lab - Configuring user profiles

## Summary

In this lab, you will practice configuring user profiles in AD DS and setting up folder direction. 

## Exercise 1: Configuring roaming user profiles and Folder Redirection

### Scenario

Ada Russel frequently uses both LON-CL1 and LON-CL2 and is struggling with accessing documents between machines.  She's requested that the files in the documents folder are the same regardless of which device she is using. You've been asked to use Folder Redirection.

#### Task 1: Prepare the environment for roaming profiles and Folder Redirection

1.  On **LON-DC1**, sign-in as **adatum\\administrator** using **Pa55w.rd** as
    the password.

2.  On **LON-DC1**, on the taskbar, select **File Explorer**. In the navigation
    pane, select **Allfiles (E:)**.

3.  In **File Explorer**, in the details pane, right-click an empty space, point
    to **New**, and then select **Folder**. Type **Profiles** as the folder
    name, and then press Enter.

4.  Right-click the **Profiles** folder, select **Share with**, and then select
    **Specific people**.

5.  In the **File Sharing** dialog box, in the text box, type **domain users**,
    select **Add**, select the arrow near **Read for Domain Users**, select
    **Read/Write**, select **Share** and then select **Done**.

6.  In **File Explorer**, in the details pane, right-click an empty space, point
    to **New**, and then select **Folder**. Type **Redirected** as the folder
    name, and then press Enter.

7.  Right-click the **Redirected** folder, select **Share with** and then select
    **Specific people**.

8.  In the **File Sharing** dialog box, in the text box, type **domain users**,
    select **Add**, select the arrow near **Read for Domain Users**, select
    **Read/Write**, select **Share**, select **Done**, and then close File
    Explorer.

#### Task 2: Configure roaming user profiles

1.  On **LON-DC1**, on the taskbar, select **Server Manager**.

2.  In **Server Manager**, select **Tools**, and then select **Active Directory
    Users and Computers**.

3.  In **Active Directory Users and Computers**, in the navigation pane, expand
    **Adatum.com**, and then select the **Marketing** OU.

4.  In the details pane, right-click **Ada Russell**, and then select
    **Properties**.

5.  In the **Ada Russell Properties** dialog box, on the **Profile** tab, in the
    **Profile path** text box, type **\\\\LON-DC1\\Profiles\\%username%**, and
    then select **OK**.

6.  Minimize the **Active Directory Users and Computers** window.

#### Task 3: Configure Folder Redirection

1.  On **LON-DC1**, in **Server Manager**, select **Tools**, and then select
    **Group Policy Management**.

2.  In the **Group Policy Management** console (GPMC), in the navigation pane,
    expand **Forest: Adatum.com**, expand **Domains**, and then expand
    **Adatum.com**.

3.  In the navigation pane, right-click the **Marketing** OU, and then select
    **Create a GPO in this domain, and Link it here**.

4.  In the **Name** text box, type **Folder Redirection**, and then select
    **OK**.

5.  In the GPMC, in the navigation pane, expand the **Marketing** OU,
    right-click **Folder Redirection**, and then select **Edit**. The **Group
    Policy Management Editor** window opens.

6.  In the **Group Policy Management Editor** window, under **User
    Configuration** in the navigation pane, expand **Policies**, expand
    **Windows Settings**, and then expand **Folder Redirection**.

7.  Right-click **Documents**, and then select **Properties**.

8.  In the **Documents Properties** dialog box, in the **Setting** drop-down
    box, select **Basic – Redirect everyone’s folder to the same location**.

9.  In the **Target folder location** section, in the **Root Path** text box,
    type **\\\\LON-DC1\\Redirected**, and then select **OK**.

10. In the **Warning** dialog box, select **Yes**.

11. Close the **Group Policy Management Editor** window, and then minimize the
    GPMC.

#### Task 4: Test roaming user profiles and Folder Redirection

1.  On **LON-DC1**, on the taskbar, select **File Explorer**.

2.  In **File Explorer**, in the navigation pane, select **Allfiles (E:)**, and
    then verify that the **Profiles** and **Redirected** folders are empty.

3.  Sign in to **LON-CL1** as **Adatum\\Ada** with the password **Pa55w.rd**.

4.  Right-click anywhere on the desktop, point to **New**, and then select
    **Folder**. Type **Presentations** as the folder name, and then press Enter.

5.  On the desktop, right-click anywhere, point to **New**, and then select
    **Shortcut**.

6.  Select **Browse**, expand **This PC**, select **Local Disk (C:)**, select
    **OK**, select **Next**, and then select **Finish**. A shortcut to local disk
    C: is added to the desktop.

7.  On the taskbar, select **Start**, type **notepad**, and then press Enter.

8.  In **Notepad**, type your name. On the **File** menu, select **Save As**,
    select the **Documents** folder in the navigation pane, enter your name in
    the **File Name** text box, select **Save**, and then close **Notepad**.

9.  On the taskbar, select **File Explorer**, and then in the navigation pane,
    select **Documents**. In the details pane, right-click the file with your
    name, and then select **Properties**. Verify that the location of that file
    points to the network, to **\\\\LON-DC1\\Redirected\\Ada\\Documents**, and
    that it’s not stored inside Ada Russell’s local profile. Also, verify that
    there is an **Offline Files** tab in the **File Properties** dialog box, and
    then select **OK**.

10. **Sign out** of LON-CL1.

11. On **LON-DC1**, in **File Explorer**, verify that the **E:\\Profiles** and
    **E:\\Redirected** folders are no longer empty. The **Profiles** folder
    contains the Ada Russell roaming user profile (**Ada.V6**), while the
    **Redirected** folder contains Ada Russell’s redirected **Documents**
    folder.

12. Sign in to **LON-CL2** as **Adatum\\Ada** with the password **Pa55w.rd**.

13. Verify that the **Presentations** folder and the **Local Disk (C)** shortcut
    are on the desktop.

14. On the taskbar, select **File Explorer**, and then in the navigation pane,
    select **Documents**. In the details pane, right-click the file with your
    name, and then select **Properties**. Verify that the location of that file
    points to the network, to **\\\\LON-DC1\\Redirected\\Ada\\Documents**, and
    that it’s not stored inside Ada Russell’s local profile.

15. **Sign out** on LON-CL2.

## Exercise 2: Configuring Enterprise State Roaming

### Scenario

Users are requesting that their Windows settings and application data be the same when using different computers. They also require to have their documents available.You have decided to implement Enterprise State Roaming and OneDrive Known Folder Move. You will need to enable ESR and Known Folder Move, and verify that it is working.  Diego Siciliani has offered to test, as he frequently switches between LON-CL3 and LON-CL4.


#### Task 1: Enable Enterprise State Roaming

1.  Sign in to **LON-CL1** as **Adatum\\Administrator** with the password **Pa55w.rd**.

2.  In Microsoft Edge, type **https://portal.azure.com** in the address bar, and
    then press **Enter**.

3.  Sign in as user **Admin\@yourtenant.onmicrosoft.com**, and use the tenant
    admin password.

4.  In the Azure Portal, in the navigation pane, select **Azure Active
    Directory**.

5.  On the **Azure Active Directory** blade, in the navigation pane, select
    **Devices**.

6.  On the **Devices** blade, make a note of devices that are listed in the
    details pane. In the navigation pane, select **Enterprise State Roaming**.

7.  On the **Devices – Enterprise State Roaming** blade, in the details pane, in
    the **Users may sync settings and app data across devices** section, select
    **Selected**.

8.  Select **Selected No member selected**, select **Add** and type **Diego
    Sicilian** in the text box.

9.  Select **Diego Siciliani** and then select **Select**.

10. Select **OK**, and then select **Save**. Close the **Devices | Enterprise State Roaming** blade.

    _Note: By performing this task, you enabled Enterprise State Roaming for Diego
    Siciliani._

11. In the **ADATUM | Overview** portal, select **Groups.**

12. On the **Groups – All groups** page, select **All groups**, and then select
    **New Group**.

13. In the **Group** window, select **Security** for **Group type**, type
    **AdatumGroup2** in the **Group Name** text box, select **Assigned** for
    **Membership type**, and then select **No members selected**.

14. In the **Add members** window, select **Diego Siciliani**, and then select
    **Select**.

15. Select **Create**. Close the **Group** page.

16. In the **Azure Active Directory admin center** page, select from the breadcrumb
    navigation **ADATUM**, scroll down and then select **Properties**. Note down the value for **Tenant ID**.
    
    _Note: The value is needed for the configuration of the Knwon Folder Move._

#### Task 2: Enable OneDrive Known Folder Move

1.  On **LON-CL1** in Microsoft Edge, type **https://endpoint.microsoft.com** in the 
    address bar and then press **Enter**.

2.  In the Microsoft Endpoint Manager admin center, select **Devices** from the 
    navigation bar. On the **Devices | Overview** page, select **Configuration Profiles**.

6.  On the **Devices | Configuration profiles** blade, in the details
    pane, select **Create profile**.

7.  In the **Create a profile** blade, select the following options, and then select **Create**:

    -   Platform: **Windows 10 and later**

    -   Profile: **Administrative Templates**

8.  In the **Basics** blade, enter the following information, and then select **Next**:

    -   Name: **A. Datum Known Folder Move**

    -   Description: **Configuration of OneDrive Known Folder Move**

9.  On the **Configurations settings** blade, select **All Settings**. In the
    **Search to filter items.** text box type **OneDrive**.

10. Under **Setting Name** select **Silenty move Windows known folders to OneDrive**.
    In the **Silenty move Windows known folders to OneDrive** dialog box select **Enabled**, then enter the value you noted down earlier for **Tenant ID**. Select **OK**.

11. Select **Silently sign in users to the OneDrive sync app with their Windows
    credentials**, and then select **Edit**. In the **Silently sign in users to the OneDrive sync app with their Windows credentials** dialog box select **Enabled**, then select **OK**.

12. Select **Continue syncing on metered networks**, and then select **Edit**. In the
    **Continue syncing on metered networks** dialog box select **Enabled**.

13. Then select **Next** two times until you reach the **Assignments** blade. 
    On the **Assignments** blade, select **Select groups to include**. Then on 
    the **Select groups to include** blade, in the **Search** box, type **A**. Select **ADatumGroup2** and then select **Select**.

14. Select **Next** and then select **Create**.


#### Task 3: Verify sync is enabled on LON-CL3

1.  Switch to **LON-CL3** and sign in as **DiegoS\@yourtenant.onmicrosoft.com** with the 
    default tenant password if you are not already signed in. 

2.  On the taskbar, select **Start** and then select the **Settings** icon. Select **Accounts** then select **Sync your settings**.

3.  On the **Sync your settings** page, verify that **Sync settings** is set to **On**. 

    _**Important**: If Sync settings is set to off and it is greyed out, the device must be rejoined.  This is due to an issue with ESR being enabled after devices have been enrolled._ 
    _If this occurs, continue with task 4, otherwise continue with Task 5._

#### Task 4: Re-enroll Devices (if needed)

1.  In Accounts, select the **Access work or school**.  Select the Azure AD connection and
    select **Disconnect**. Select **Yes** and then select **Disconnect** to confirm. In the **Windows Security** dialog enter **Admin** as **Email Address** and **Pa55w.rd** as **Password**.

2.  Restart the VM and sign in as **Admin**, with the password **Pa55w.rd**.

3.  Select **Start** and type **View advanced system settings** and press **Enter**.
    In the **System Properties** window under **User Profiles** select **Settings**.

4.  In the **User Profiles** window select **Account Unknown** and then select **Delete**.
    Confirm with **Yes**.

5.  Select **Start**, then **Settings**, then **Accounts**.  Select **Access work or school** and select **Connect**.

6.  In the **Microsoft account** window, select **Join this device to Azure Active Directory**.

7.  On the **Let's get you signed in** page, type **diegos\@yourtenant.onmicrosoft.com** 
    and then select **Next**.

8.  On the **Enter password** page, enter the tenant password and select **Sign in**.

9.  Wait a few seconds and then on the **Make sure this is your organization** dialog, select **Join**.

10. On the **You're all set!** page, select **Done**.

11. **Sign out** of LON-CL3.

#### Task 5: Test Enterprise State Roaming and Known Folder Move

1.  Sign in to **LON-CL3** as **DiegoS\@yourtenant.onmicrosoft.com** with the 
    default tenant password.

    _Note: It could take 5-10 minutes until the Intune configuration is finished._

    _**Important**: If the OneDrive auto configuration is not working sign out and sign in again. This is due to Windows issues._

2.  On **LON-CL3**, on the taskbar, select **Microsoft Edge** and in the address bar,
    type **www.microsoft.com/learn**, and then press **Enter**. When the page
    loads, select the star and the end of the address bar (or press CTRL+D). In
    the **Favorites** pop-up, select **Add**.

3.  On the taskbar, select **Start**, type **notepad**, and then press Enter.

4.  In **Notepad**, type your name. On the **File** menu, select **Save As**,
    select the **Documents** folder in the navigation pane, enter your name in
    the **File Name** text box, select **Save**, and then close **Notepad**.    

5.  Switch to **LON-CL4** and sign in as **Admin**, with the password **Pa55w.rd**.

    _**Important:** The device must be enrolled new with the credentials of **DiegoS\@yourtenant.onmicrosoft.com**. Follow the procedures outlined in Task 4._

6.  On **LON-CL4** sign in as **DiegoS\@yourtenant.onmicrosoft.com**. 

7.  On the taskbar, select **Start** and then select the **Settings** app, then 
    select **Sync your settings**.

8.  On the **Sync your settings** page, verify that **Sync settings** is set to **On**. 

9.  On the taskbar, select **Microsoft Edge**. In **Microsoft Edge**, press CTRL+I to view
    favorites. Verify if the Microsoft Learn favorites page is already synced from **LON-CL3**.  

    _Note: It can take several minutes for settings to sync. If the favorites option
    doesn't show, try rebooting and signing back in as DiegoS\@yourtenant.onmicrosoft.com._

10. On the taskbar, select **File Explorer**, and then in the navigation pane,
    select **Documents**. Verify that the document you created on **LON-CL3** is available.


**END OF LAB**

# Practice Lab - Connecting AD DS and Azure AD

## Summary

In this lab, you will practice configuring synchronization between Active Directory Domain Services and Azure Active Directory.

### Scenario

A. Datum Corporation is currently managing provisioning users in both AD DS and Azure AD as separate processes.  This is time consuming and has led to inconsistent information. You have been tasked with addressing this issue by synchronizing the two directories.

#### Task 1: Verifying licenses and creating a sync account

1.  On **LON-CL1**, sign in as **Adatum\\Administrator** with the password of **Pa55w.rd**, and then open the
    **Microsoft Edge** browser.

2.  In the **Microsoft Edge** window, go to **https://portal.azure.com** and select **Continue to Azure Portal website**. If
    prompted, sign in with your Mod administrator credentials available in hosted lab
    environment. If the **Stay signed in?** prompt appears, select **No**. If the **Welcome to Microsoft** Azure window appears, select     **Maybe later**.

3.  On the **Microsoft Azure** page, select **Azure Active Directory** in the
    left navigation pane. This will open the Adatum Azure Active Directory page.

4.  On the Azure portal, select **Users** in the navigation pane, select **All
    users**, and then select **New user**.

5.  In the **New User** dialog box, select **Create user** and enter the following:

    -  User Name: **sync\@yourtenant.onmicrosoft.com**

    -  Name: **Sync User**

6.  Select **Show Password**, note and write down the value for **Initial Password**.

7. Under Groups and roles, on the **Roles** row, select **User**. 
    Select **Global administrator**, and then select **Select** , and
    then select **Create**.

8.  At the upper right of the page, select your account name, and then select
    **Sign in with a different account**.

9. On the **Microsoft Azure** page, select **Use another account** if needed,
    type **sync\@yourtenant.onmicrosoft.com** for the user name, type the
    temporary password that you noted above, and then select **Sign in**.

10. On the **Update your password** page, in the **Current password** text box,
    type the temporary password, in the **New password** and **Confirm
    password** text boxes, type **Pa55w.rd12345** and then select **Sign in**.

11. If the **Welcome to Microsoft** Azure window appears, select **Maybe later**.
    Select your **Sync user** account in the upper right of the page, and then
    select **Sign in with a different account**.

#### Task 2: Customize Azure AD company branding

1.  Sign back in to the Azure portal as **admin\@yourtenant.onmicrosoft.com**. 

2.  In the Microsoft Azure portal, in the navigation pane, select **Azure Active
    Directory**.

3.  On the **Azure Active Directory** blade, select **Company branding**, and
    then select **Configure**.

4.  On the **Configure company branding** blade, configure the following
    settings:

    -  Sign-in page text: **Adatum.com sign-in page**

    -  Show option to remain signed in: Select **Yes**.

5.  Select **Save**, and then close the **Company branding** blade.

6.  On the **Azure Active Directory** blade, in the navigation pane, select
    **Properties**.

7.  In the **Name** text box, type **ADATUM**, and then select **Save**. Leave the browser
    window open.

#### Task 3: Configuring directory synchronization with Azure AD Connect

1.  On **LON-DC1**, sign in as **Adatum\\Administrator**, with
    the password **Pa55w.rd**.

2.  Open **Internet Explorer**, and then go to
    **http://www.microsoft.com/en-us/download/details.aspx?id=47594**.

3.  On the **Microsoft Azure Active Directory Connect** page, select
    **Download**, and then select **Run**. 
    
    _**Important**: If you experience any problems
    with launching the download, add the https://download.microsoft.com website
    to your Trusted sites._

4.  In the **Microsoft Azure Active Directory Connect Wizard**, on the **Welcome
    to Azure AD Connect** page, select the **I agree to the license terms and
    privacy notice** check box, and then select **Continue**.

5.  On the **Express Settings** page, select **Customize**.

6.  On the **Install required components** page, select **Install**.

7.  On the **User sign-in** page, ensure that **Password Hash Synchronization**
    is selected, and then select **Next**.

8.  On the **Connect to Azure AD** page, in the **USERNAME** and **PASSWORD**
    boxes, enter the Sync account user name (it will be in the following format:
    **sync\@yourtenant.onmicrosoft.com**) and **Pa55w.rd12345** for a password, and
    then select **Next**.

9.  On the **Connect your directories** page, ensure that **Adatum.com** is listed
    under **FOREST**, and then select **Add Directory**.

10. In the **AD forest account** window, select the **Create New AD Account**
    option, and in the **ENTERPRISE ADMIN USERNAME** field, type
    **Adatum\\Administrator**, and then type **Pa55w.rd** in the **PASSWORD**
    field. Select **OK**, and then select **Next**.

11. On the **Azure AD sign-in configuration** page, ensure that in the **USER
    PRINCIPAL NAME** drop-down list, the **userPrincipalName** value is
    selected. Select **Continue without matching all UPN suffixes to verified
    domains** and then select **Next**.

12. On the **Domain and OU filtering** page, select **Sync selected domains and
    OUs**.

13. Expand **Adatum.com**, clear the checkbox on Adatum.com and ensure that the
    only following check boxes are selected: **Computers**, **IT**,
    **Managers**, **Marketing**, **Research**, and **Sales**. Clear the other
    check boxes, and then select **Next**.

14. On the **Uniquely identifying your users** page, select **Next**.

15. On the **Filter users and devices** page, select **Next**.

16. On the **Optional features** page, review available options, but do not make
    any changes. Ensure that **Password hash synchronization** is selected, and
    then select **Next**.

17. On the **Ready to configure** page, ensure that **Start the synchronization
    process when configuration completes** is selected, and then select
    **Install**.

18. When configuration is complete, select **Exit**.  
    _Note: At this time, synchronization of objects from your local Active Directory
    Domain Services (AD DS) and Azure AD begins. You should wait approximately
    3-4 minutes for this process to complete._

19. In the Internet Explorer window on LON-DC1, browse to
    **http://www.microsoft.com/en-us/download/details.aspx?id=41950**.

20. On the **Microsoft Online Services Sign-In Assistant for IT Professionals
    RTW** page, select **Download**. On the **Choose the download you want** page,
    select **en\\msoidcli_64.msi** and select **Next**. Select **Run**. Allow pop-ups
    or Disable pop-up blocker if needed.

21. Select **I accept the terms in the License Agreement** and select **Install**.
    When installation is done select **Finish**.
    
22. Close the **Internet Explorer** window.

#### Task 4: Verify synchronization in Azure AD

1.  Switch to **LON-CL1**.

2.  In the **Azure Active Directory** portal from the navigation pane select **Users**. Select **Refresh**.

3.  Verify that you see users from your local AD DS. Ensure that these users
    have the value **Windows Server AD** in the **SOURCE** column. Close Users
    window.

4.  Select **Groups**. Verify that you see groups from your local AD DS.

5.  Select the **Managers** group.

6.  On the **Managers** group page, ensure that you see users when you select
    **Members**. Also, verify that you cannot make any changes to this group, as
    it is sourced from the local Active Directory. Close the Managers window and
    close the Groups window.

7.  Leave the Azure Active Directory portal open on LON-DC1 for the next lab.

**END OF LAB**

# Practice Lab - Create and deploy device profiles

## Summary

In this lab, you will practice creating and applying a device profile.

### Exercise 1: Create and deploy a device profile

### Scenario

A. Datum Corporation’s has decided to manage all developers in the company using Azure Active Directory (Azure AD) and Intune. You have been asked to evaluate the solutions that would enable the developers to work effectively and securely on Windows 10 devices managed by Intune and Azure AD. The head of the developer department, Brenda Mueller, has volunteered to help you test and evaluate the solution and provide feedback. She has also given you some initial requirements that must be included in the configuration of Intune:

•	It should not be possible to access Gaming or Privacy in the Settings app.
•	The C:\DevProjects folder should be excluded from Windows Defender.
•	The process devbuild.exe must be excluded from Windows Defender.
•	Most used apps and Recently added apps should not be displayed on the Start menu.


#### Task 1: Verify settings on device before enrollment

1.  Sign in to **LON-CL3** as **Admin** with the password **Pa55w.rd**.

2.  On **LON-CL3**, on the taskbar, click **Start** and then click the
    **Settings** app.

3.  In the **Settings** app, verify that you can see the **Gaming** tile.

4.  Click **Privacy** and verify that you can see a lot of customization
    options.

5.  Click the left arrow in the upper left corner.

6.  Click the **Personalization** tile and then click **Start**. Verify that
    **Show recently used apps** is set to **On**.

7.  Click the left arrow in the upper left corner.

8.  In the **Settings** app, click **Update and Security**.

9.  On the **Update & Security** page, click **Windows Security** and then
    **Open Windows Security**.

10. On the **Windows Security** page, click the menu and then click the **Virus
    & threat protection**.

11. On the **Virus & threat protection** page, click **Manage settings** under
    **Virus & threat protection settings**. Scroll down to **Exclusions** and
    click **Add or remove exclusions**.

12. On the **Exclusion** page, verify that no exclusions have been configured.

13. Close the **Exclusions page** and the **Windows Security** page by clicking
    the **X** in the right upper corner twice.

### Task 2: Enroll Windows 10 device to Azure AD and Intune using the Settings app

1.  On **LON-CL3**, on the taskbar, click **Start** and then click the
    **Settings** app.

2.  In the **Settings** app, click the **Accounts** tile and then click **Access
    work or school**.

3.  In the **Access work or school** section, click **+Connect**.

4.  In the **Microsoft account** window, on the **Set up a work or school
    account** page, click **Join this device to Azure Active Directory**.

5.  On the **Let’s get you signed in** page, in the **Work or school account**
    text box, type **DiegoS\@yourtenant.onmicrosoft.com**

6.  On Enter password page, type **Pa55w.rd** in the text box and then click
    **Sign in**.

7.  Wait a few seconds and then on the **Make sure this is your organization**
    dialog, click **Join**.

8.  On the **You’re all set!** page, click **Done**.

9.  In the **Settings** app, in the **Access work or school** section, verify
    that the device is connected to Azure AD and then close the **Settings**
    app.

10. Right-click the **Start** button and select **Windows PowerShell (Admin)**,
    when prompted click **Yes.**

11. In the PowerShell console, type the following and then press Enter: **REG
    ADD HKLM\\SOFTWARE\\Policies\\Microsoft\\PassportForWork /v Enabled /t
    REG_DWORD /d 0 /f**  
    This will disable Windows Hello on the device and will disable the forced
    creation of a PIN when logging on to the device the first time using an
    Azure AD account. This will also disable the need for access to a mobile
    phone as this requires validation of the Azure AD account being used. You
    can also disable the use of Windows Hallo by creating a policy in Intune.

### Task 3: Logon to a different Windows 10 device using Azure AD user

1.  On **LON-CL4**, right-click Start, click **Shutdown or sign out** and then
    click **Sign out**.

2.  Click **other user**, and in the **Email address** field type
    DiegoS**\@yourtenant.onmicrosoft.com**, and then click **Next**. In the
    Password field, type **Pa55w.rd** and then press Enter.

3.  Wait for the profile to be created. It will take around 30-60 seconds.  
    **Note:** When you are logged on using your Azure AD credentials you will
    benefit from Single-Sign-On (SSO) to Azure AD, Intune and Office 365.


### Task 4: Create device profile based on scenario

1.  On **LON-CL3**, on the taskbar, click **Microsoft Edge**.

2.  In Microsoft Edge, type **https://portal.azure.com** in the address bar, and
    then press Enter.

3.  Sign in as user **Admin\@yourtenant.onmicrosoft.com**, and use the tenant
    Admin password.

4.  In the Azure portal, click **Intune** in the navigation pane, and then on
    the **Microsoft Intune** blade, click **Device configuration**.

5.  On the **Device configuration** blade, click **Profiles**. In the details
    pane, click **+ Create profile**.

6.  In the **Create profile** blade, enter/select the following information:

-   Name: **A. Datum developers - standard**

-   Description: **Basic restrictions and configuration for developers in A.
    Datum.**

-   Platform: **Windows 10 and later**

-   Profile type: **Device restrictions**

1.  On the **Device restrictions** blade, click **Control Panel and Settings**.
    Select **Block** next to **Gaming** and **Privacy**. Then click **OK**.

2.  Back on the **Device restrictions** blade, click **Start**. Scroll down and
    select **Block** next to **Most used apps** and **Recently added apps**.
    Then click **OK**.

3.  Back on the **Device restrictions** blade, scroll down and click **Windows
    Defender Antivirus**. On the **Windows Defender Antivirus,** scroll down and
    click **Windows Defender Antivirus Exclusions**.

4.  On the **Windows Defender Antivirus Exclusions** blade, in the **Files and
    folders** box, type the following and then click **Add**:
    **C:\\DevProjects**.

5.  In the **Processes** box, type the following and then click **Add**:
    **DevBuild.exe**. Then click **OK** twice.

6.  Back on the **Device restrictions** blade, click **OK** and then click
    **Create**.

### Task 5: Create the Adatum developer device group

1.  In the Azure portal, click **Azure Active Directory** in the navigation
    pane, and then **Groups**.

2.  On the **Groups** blade, click **+ New group**.

3.  On the **Group** blade, enter/select the following information:

-   Group type: **Security**

-   Group name: **A. Datum developer devices**

-   Group description: **All Windows 10 devices in A. Datum developer
    department**

-   Membership type: **Assigned**

4.  Click **Members** and on the **Select members** blade, in the **Search by
    name or mail address**, type **lon**. Click **LON-CL3** and then click
    **Select**.

5.  Back on the **Group** blade, click **Create**. Close the **Group** blade by
    clicking the **X** in the upper right corner.

6.  On the **Groups – All groups** blade, verify that the **A. Datum developer
    devices group** is displayed.

### Task 6: Create a dynamic Azure AD device group

1.  In **LON-CL1**, in the Azure portal, scroll the page to the left and then in
    the **Azure Active Directory** blade click **Groups**.

2.  On the **Group** blade, on the details pane, click **+New group**.

3.  On the **Group** blade, provide the following values:

    1.  Group type: **Security**

    2.  Group name: **Enrolled Devices**

    3.  Membership type: **Dynamic Device**

4.  On the **Group** blade, click **Dynamic device members**.

5.  Click **Add dynamic query**. On the **Dynamic membership rules** blade
    provide the following Simple membership rule to add devices where:

```
    deviceOSType Contains Windows

```
6.  On the **Dynamic membership rules** blade, click **Add query** and then
    click **Create**.

### Task 7: Deploy device profile to Windows 10 device

1.  In the Azure portal, click **Intune** in the navigation pane, and then on
    the **Microsoft Intune** blade, click **Device configuration**.

2.  On the **Device configuration** blade, click **Profiles**. In the details
    pane, click the **A. Datum developers – standard** profile.

3.  On the **A. Datum developers – standard** blade, click **Assignments**. On
    the **A. Datum developers – standard – Assignments** blade, click **Select
    groups to include**.

4.  On the **Select members** blade, in the **Search by name or mail address**,
    type **A**. Click **A. Datum developer devices** and then click **Select**.

5.  Back on the **A. Datum developers – standard** blade, click **Save**.

### Task 8: Verify on the device that device profile is applied

1.  On **LON-CL3**, on the taskbar, click **Start** and then click the
    **Settings** app.

2.  In the **Settings** app, click the **Accounts** tile and then click **Access
    work or school**.

3.  In the **Access work or school** section, click the **Connected to Contoso’s
    Azure AD** link and then click **Info**.

4.  In the **Managed by Contoso** dialog box, click **Sync**. Wait for the
    synchronization to complete.  
    It may take up to 15 minutes before the profile is applied to Windows 10
    device.

5.  Close the **Settings** app, and open it again. Verify that the **Gaming**
    and **Privacy** tile has been removed.

6.  Click the **Personalization** tile and then click **Start**. Verify that
    **Show recently used apps** and **Show most used apps** are set to **Off**.
    Click the left arrow in the upper left corner.

7.  In the **Settings** app, click **Update and Security**.

8.  On the **Update & Security** page, click **Windows Security** and then
    **Open Windows Security**.

9.  On the **Windows Security** page, click the menu and then click the **Virus
    & threat protection**.

10. On the **Virus & threat protection** page, click **Manage settings** under
    **Virus & threat protection settings**. Scroll down to **Exclusions** and
    click **Add or remove exclusions**.

11. On the **Exclusion** page, verify that **C:\\DevProjects** and
    **DevBuild.exe** are displayed.

12. Close the **Exclusions page** and the **Windows Security** page by clicking
    the **X** in the right upper corner twice.



### Exercise 2: Change deployed device policy  

### Scenario

There was an exception to A. Datum's policies initiated where developers should not have the Privacy option blocked in Settings on thier devices. This change should be implemented and tested.

### Task 1: Change setting in assigned profile

1.  On **LON-CL3**, in the Azure portal, click **Intune** in the navigation
    pane, and then on the **Microsoft Intune** blade, click **Device
    configuration**.

2.  On the **Device configuration** blade, click **Profiles**. In the details
    pane, click **A. Datum developers - standard**.

3.  On the **A. Datum developers - standard** blade, click **Properties**. On
    the **A. Datum developers - standard** – **Properties** blade, click
    **Settings 6 configured**.

4.  On the **Device restrictions** blade, click **Control Panel and Settings**.
    Select **Not configured** next to **Privacy**. Then click **OK** twice.

5.  Back on the **A. Datum developers - standard** – **Properties** blade, click
    **Save**.

### Task 2: Force synchronization of policy from Intune console

1.  On **LON-CL3**, in the Azure portal, click **Intune** in the navigation
    pane, and then on the **Microsoft Intune** blade, click **Devices** and then
    click **All devices**.

2.  In the details pane, click **LON-CL3**. On the **LON-CL3** blade, click
    **Sync** and when prompted click **Yes**.  
    Intune will contact the device and tell it to synchronize all policies. This
    may take up to 5 minutes.

### Task 3: Verify profile change on device

1.  Switch toon **LON-CL34** and on the taskbar, click **Start** and then click
    the **Settings** app.

2.  In the **Settings** app, click **Privacy** and verify that all of the
    customization options are back.

3.  Close the **Settings** app.

**END OF LAB**
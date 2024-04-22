#  Entra ID Multi-Factor Authentication Implementation

## Introduction
This comprehensive project documentation offers an in-depth exploration of the meticulous process involved in fortifying the authentication framework of Entra ID in Azure through the implementation of Multi-Factor Authentication (MFA). Recognized as a cornerstone of contemporary security protocols, MFA enhances the verification process by requiring users to authenticate their identity using multiple factors. This documentation elucidates the sequential steps encompassing the disabling of Security Default, creation of dynamic groups, assignment of licenses, implementation of an MFA policy tailored explicitly for the Sales team, and comprehensive testing protocols.

## Disabling Security Default
![Accessing_Security_Default_Page](media/001_Accessing_Security_Default_Page.png)
At the project's inception, the journey towards implementing MFA necessitates the disabling of Security Default. 
![Diasble Security Defaults](media/002_DisablingMFA.png)

This pivotal step, executed within the Azure portal, entails navigating to the Entra ID properties and meticulously managing the Security Default setting to deactivate it. 
![Defaults Are Gone](media/003_organisationNotManagedBySecurityDefaults.png)
By nullifying Security Default, the groundwork is laid for the formulation of a customized security policy aligned with the organization's unique requirements and security posture.

## Testing User Access With MFA Disbaled

In order to verify that MFA is currently not enabled for the Tenant, I will make use of one of the members of the Tenant by Name Chris Green
![Members of The Tenant](media/006_ChrisGreen.png)
Members of the Tenant.

![ChrisGreet](media/006_ChrisGreen.png)
Details of User Chris Green

Chris Green will attemp login into the Azure Portal with his UPN and will not be required for MFA set as displayed below
![Chris Green Login](media/007_logginInToAzurePOrtalAsChrissGreen.png)

![PasswordEnteredForchrissgreen](media/008_PasswordEnteredForchrissgreen.png)

![SuccessIWhtouMFArequirement](media/009_SuccessIWhtouMFArequirement.png)

Chris has been able to access the Azure Portal without MFA Requirement as it has been disabled as a Security Default.



## Creation of Dynamic Group
The creation of dynamic groups constitutes a pivotal aspect of establishing a resilient MFA infrastructure within Entra ID. Within the Azure portal's Entra ID blade, a new Microsoft 365 Dynamic Group christened "Sales" is meticulously fashioned. This dynamic group is meticulously configured with a dynamic query, stipulating that users with the departmental designation of "Sales" are automatically assimilated into the group, streamlining the user management process and ensuring alignment with organizational roles and responsibilities.

### The Process

In doing this project, I want newly created users to be dynamically assinged to Groupes based on thier attributes. As stated above, I will be working to create Sales Group which will be having Memebers Dynamically Assigned. 

Below is the listing of the current groups in the Tenant.
![Current Groups In Tenant](media/010_CurrentGroupsInTenant.png)

I proceeded to Create the Sales group of Group Type Microsoft 365 and indicated the membership type as "Dynamic User"
![GroupDetailssalesGroup](media/011_GroupDetailssalesGroup.png)

Since it is a Dynamic group, it must have a Dynamic Query Attached and the logic of my Dianmy Query is to have Members who have the The Department Attribute as Sales should be automatically added to the group
![CreatingDynamicQuery](media/012_CreatingDynamicQuery.png)

As can eb verified from the above image, the Dynamic Query is 
```
(user.department -eq "Sales") or (user.department -eq "sales")

```
This query helps to capture Users who have Department starting With either small or capial "s"

![SaleGroupCreated](media/013_SaleGroupCreated.png)

From the above, we can confirm the creation of the Sales Group with the Membership Type of Dynamic which is Different from the other Groups in Tenant.

### Adding Members to the Group
In order to add members to the group, we either create new members with the Department Attribute as Sales or better still we edit existing users and change their Departmnet attributes to Sales. I will do the two starting with changing the Atrinute of Chris Green.

Below we can see the attributes of Chris and realise he does not belong to any group
![NotInANyGroup](media/016_NotInANyGroup.png)

On the Overview page of Chris Green, I clicked on Edit Properties to make the necessary adjustments.
![OverviewpageEditProperties](media/017_OverviewpageEditProperties.png)

The Department attribute has been changed to Sales as depicted below
![SetDepartmenttoSales](media/018_SetDepartmenttoSales.png)

Going back to Groups Under Chris's name, you will realised now he belongs to the Sales Group just after making the Change is His Attribute
![019_ChrisPageGroup](media/019_ChrisPageGroup.png)

To double check, I went to the Groups Blade in Entra ID and Open the sales group to verify its members. The members as shown below is only Chris Green due to the change made earlier
![GroupchrisAddedAutomatic](media/020_GroupchrisAddedAutomatic.png).

I then proceeded to add more members to the group this time by creating new users from scratch as seen below
![025_NewMembersAddedDynamicallyToTheGroup](media/025_NewMembersAddedDynamicallyToTheGroup.png)

## Assigning Licenses to the Sales Group
License assignment emerges as a critical facet of the MFA implementation endeavor, embodying the principles of least privilege and role-based access control. Rather than individually provisioning licenses to users, a judicious approach is adopted wherein licenses are methodically allocated to groups. Within the intuitive Entra ID interface, licenses are meticulously assigned to the Sales Group, thereby ensuring that all members are endowed with the requisite privileges and access rights imperative for executing their tasks seamlessly and effectively contributing to organizational objectives.\

### The Process
In the first place, I will like to verify that no individual in the Sales Group has any Lincense assinged and that confirmation can be done Using our Chris Green. 
Under the Manage Section when Chris Page is Opened, there is an option of Linceses which will list all the licnceses Assinged to him.
![NolincenceAssinged](media/015_NolincenceAssinged.png)

From the image above, we can confirm Chris currently has no Lincense assinged to the fact that we have not assigned him any Lincense either on an individual level or on a Group Level. This arise from the fact that the Sales Group also does not have any assinged License as can be confirmed from Below
![NoLincenseassingedtosalesTeam](media/021_NoLincenseassingedtosalesTeam.png)

Since we want to avoid assigning Lincense on an individual basis, in the Sales Group Page, I navigated to the Linceses Section on the left and Assigned an Micosoft 365 Lincense to the sales Group
![AssigningOffice365Lincence](media/022_AssigningOffice365Lincence.png)

![confimedLincestoSalesteam](media/023_confimedLincestoSalesteam.png)
The License has been assigned accordingly.

Going back to Chris Page, it can be confirmed he now has the Lincense of Microsoft 365 which he inherited from Sales Group just because he is a member of the group.
![LincenceInherited](media/024_LincenceInherited.png)

To view the apps contained in the License, We will log into my apps Portal but this time around making use of Emily Johnson.

![EmilyJohnsonLoggingInProcess](media/036_EmilyJohnsonLoggingInProcess.png)

![alt text](media/027_PromtToChangePassword.png)

Emily Johnson has access all Microsoft 365 apps as she has the Lincense by virtue of been part of the Sales group in Entra confirmed from the Image below.
![ListingofAppsAssignedtoEMily](media/028_ListingofAppsAssignedtoEMily.png)

## Implementing MFA Policy for Sales Team
The crux of the MFA implementation endeavor resides in the formulation and enforcement of a comprehensive policy tailored explicitly for the Sales team. Multi-Factor Authentication serves as the linchpin of contemporary cloud security, bolstering resilience against an array of potential threats and vulnerabilities. Policies encapsulated within Azure Identity Protection afford administrators the latitude to enforce stringent security measures tailored to organizational exigencies. Leveraging the robust functionalities of Entra ID within the Azure portal, an intricately crafted MFA policy is conceived, delineating specific conditions, access controls, and authentication protocols. Rigorous testing protocols are subsequently instituted to validate the efficacy and robustness of the implemented policy, thereby ensuring a seamless authentication experience for Sales team members while fortifying the organization's security posture.

### The Process
From the beginning, the securiy default was disabled for the Tenant which ensure login happens using only singel factor authentiation which does not meet best security practices.
In creating a new Policy, I will enforce MFA requirement for only the Sale Group Members in the Tenant. 
To implement that, I moved to the Identity Protection  Blade in Entra ID and click on Conditional Access which give me the option to create a binding policy
![Identity_Protection_Portal](media/039_Identity_Protection_Portal.png)

![AboutToCreatePolicy](media/040_AboutToCreatePolicy.png)

The Policy was named *MFA_Policy_For_SalesGP*. For the Assignment, I selcted Users and Group and then Specify the Sales Group.
![Selecting_Sales_Group](media/041_Selecting_Sales_Group.png)

For the Target resource, I select Office 365 Apps and then My Apps  as shown below
![043_Selecting_Office365_For_SalesMFA](media/043_Selecting_Office365_For_SalesMFA.png)

For the conditions sections, I selected two conditions of which are 
1. Device Platform : Any Device
2. Location: Any Locations
This implies no matter your locaion or the types of device you use, you will still need to use MFA to access my apps portal and Office 365 Apps.
![Specifying Conditions](<media/044_Specifying Conditions.png>)

Then I set the Enable Policy to on
![Policy_Created_Successfully](media/046_Policy_Created_Successfully.png)

In the Grant section, I picked Require MFA
![045_Require_Multi_Factor_Authentication](media/045_Require_Multi_Factor_Authentication.png)

## Comprehensive Testing Protocols
Following the formulation and enforcement of the MFA policy, comprehensive testing protocols are instituted to validate the efficacy and robustness of the implemented security measures. Through meticulous testing procedures, administrators verify the seamless authentication experience for Sales team members and ascertain adherence to security policies and access controls. Rigorous scrutiny of authentication logs and verification of authentication methods corroborate the successful enforcement of MFA, thereby bolstering confidence in the organization's security infrastructure and fortifying resilience against potential threats.

### The Process

In order to test the efficacy of the newly created Policy, I will make use of Emily Johnson again
![MFA Policy Requirement For Emily](media/047_MFA_PolicyRequirementForEmily.png)

From above, you will realised Emily is Greeted with settting up his MFA Device before she can access the Portal after she tried accessing her My Apps Portal again .

![Verification Sent](media/048_VerificationSent.png)

A verification code has been sent to Emily after she supplied her Phone number in this case I am standing in for EMily hence handlin all the requirements.

![Verification Complete](media/049_Verification_Complete.png)

The verification has been completed after successsfully entering the OTP sent
![Emily Login Success](media/050_EmilyLoginSuccess.png)

To verify further that Emily is now Using MFA, I opened her Sign in Logs to check the Authentication methods which changed from Single Factor Authentication to Multi-Factor Authentication shown below
![Verify in MFA Set Emily By Checking Her Sign In Logs](media/051_VerifyinMFASetEmilyByCheckingHerSignInLogs.png)

It can also be seen from below image that Emily and all the other Sales Group Members will now have  the Policy Applied to them
![Drill Down Into Emily MFA Login To See Her Policy](media/052_DrillDownINtoEmilyMFALoginToSeeHerPolicy.png)

## Conclusion
In summation, the successful implementation of Multi-Factor Authentication for the Sales team within Entra ID signifies a seminal advancement towards fortifying organizational security and safeguarding critical assets against an array of potential threats. By adhering to the meticulously delineated steps and harnessing the potent capabilities afforded by Azure Identity Protection, administrators can navigate the complex terrain of cloud security with confidence and efficacy. Through the amalgamation of dynamic group creation, license assignment, policy enforcement, and comprehensive testing protocols, organizations can cultivate a culture of security awareness while facilitating a seamless and frictionless user experience. The implementation of MFA within Entra ID epitomizes a proactive stance towards fortifying organizational resilience in the face of evolving cybersecurity challenges.

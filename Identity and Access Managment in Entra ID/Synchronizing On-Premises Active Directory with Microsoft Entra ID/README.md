# Entra ID Connect Sync Process - biira.store

In this project, I successfully synchronized a group of users from an on-premises Active Directory (AD) in the **IT** Organizational Unit (OU) of the **biira.com** domain to the **Entra ID** domain of **biira.store**. The aim of this sync was to ensure that user identities were consistently available across both environments, making it easier to manage access to cloud resources and ensure a smooth user experience.

This write-up covers the steps I followed to set up and complete the synchronization, along with the tools I used, such as the **IDFix tool** to resolve identity issues in my on-prem AD before starting the sync process.

## Prerequisites

Before starting the sync, I ensured I had:

- An **on-prem Active Directory** (biira.com) where the users I wanted to sync were located.
- A **biira.store** domain in **Entra ID** (Azure AD) that I intended to sync users to.
- The necessary **admin permissions** to perform synchronization tasks on both the on-prem AD and the Entra ID.
- **Entra ID Connect** installed and configured on a server that had access to both environments (on-prem AD and Entra ID).

## Steps I Followed

### 1. Identity Fix Using IDFix Tool

The first task I tackled was ensuring that there were no identity issues in the on-prem AD that could cause problems during the sync process. For this, I used the **IDFix tool**, which is a Microsoft utility designed to help identify and fix identity issues that could block successful synchronization with Entra ID.

Here’s what I did with IDFix:

- **Checked for Invalid Characters**: Entra ID has strict rules about which characters can appear in certain attributes like email addresses and usernames. I ran the IDFix tool to identify any invalid characters in my user attributes and fixed them.
- **Resolved Duplicate Attributes**: Some of my users had duplicate or conflicting attributes, especially in the `proxyAddresses` field. The tool flagged these issues, and I resolved them by updating the attributes.
- **Fixed Invalid Formats**: Some attributes (like email addresses) had invalid formats, which IDFix helped me correct before I could proceed with the sync.
- **Ensured Required Attributes Were Present**: Entra ID requires certain fields to be filled, such as `UPN` (User Principal Name) and `mail`. The IDFix tool made sure these fields were correctly populated, reducing the chances of sync failure.

By resolving these issues early, I ensured that the synchronization process would proceed smoothly and without unnecessary errors.

[![IDFix Implementation Video Demonstration](<Images/001 ID FIx.png>)](https://youtu.be/mAwQ-iYKQXg?si=FfROEZP7APr8lJTi)


### 2. Installing and Configuring Entra ID Connect

Once the identity issues were sorted out, I moved on to setting up **Entra ID Connect**, which would be responsible for syncing my on-prem AD with Entra ID.

#### Installation

- I downloaded and installed **Entra ID Connect** from the Microsoft website. I chose to install it on a server that had access to the on-prem AD.
- During the installation process, I opted for the **custom installation** option, which allowed me to fine-tune the setup, such as enabling **password synchronization**, **write-back**, and other necessary features.

#### Configuration

- **Connecting to Entra ID**: I entered the **biira.store** domain credentials to authenticate and connect Entra ID Connect to my Entra ID instance.
- **Connecting to On-Prem AD**: I also connected Entra ID Connect to my **biira.com** on-prem AD by providing the necessary admin credentials.

#### Defining Sync Scope

- The next step was to define which users I wanted to sync. I focused on syncing users within the **IT Organizational Unit (OU)**, which ensured that only users from this OU were included in the sync. This helped me avoid syncing unnecessary users or groups.
  
  You can specify other sync scopes, such as syncing entire domains or particular groups. This flexibility allowed me to narrow down the sync to just the relevant users.

#### Verifying Synchronization Settings

- I carefully reviewed the **user attribute mappings** to ensure that the fields in on-prem AD (like `userPrincipalName` and `mail`) correctly mapped to their corresponding attributes in Entra ID.
- I also double-checked the **sync options**, ensuring that features like **password hash synchronization** were properly configured, so users could seamlessly sign in to both on-prem and cloud resources with the same credentials.

Once I was satisfied with the configuration, I ran a **test sync** to ensure everything was set up correctly.

### 3. Monitoring the Sync Process

With the configuration in place, I initiated the synchronization process. During this phase, I kept a close eye on the **Sync Status** page provided by Entra ID Connect. This page provided real-time information about the sync process, allowing me to:

- Monitor how many users were synced.
- Identify any **sync errors** or issues that needed attention.
- Verify that the users were correctly synced to the **biira.store** domain in Entra ID.

I regularly checked the status to ensure there were no issues and to verify that the sync was happening as expected.

### 4. Post-Sync Verification

Once the sync process was completed without errors, I verified the results by checking:

- **User presence in Entra ID**: I confirmed that the users from the **IT OU** in **biira.com** were now present in the **biira.store** Entra ID domain.
- **Testing Single Sign-On (SSO)**: I tested the SSO functionality to ensure that users could access cloud applications using the same credentials they use for on-prem AD.
- **Group memberships**: I also verified that group memberships were synced correctly, allowing users to access resources based on their group memberships.

## Watch the Full Process

For a detailed, step-by-step guide on how I completed this synchronization process, watch the YouTube series I created below:

[Step 1: ID Fix ](https://youtu.be/mAwQ-iYKQXg?si=JWeNy5isvPZasNx4)

[Step 2](https://youtu.be/VYaXZ6JGHu0?si=AgWdl46SSc2SECa5)

[Step 3](https://youtu.be/m2mRK-hmJpU?si=hcbNkdHc5KNRU0VP)

[Step 4](https://youtu.be/XXqk_VIf3fQ?si=wcisIPnAAMdf41KF)

[Step 5](https://youtu.be/GxAFqMWmkv0)

[Step 6](https://youtu.be/m3yc9_6dSh8?si=5EXlBEoo64rDAqdb)

This video series covers:

- How I used the **IDFix tool** to resolve identity issues.
- Setting up and configuring **Entra ID Connect**
- Verifying successful synchronization and post-sync functionality.

## Conclusion

This project was a great learning experience. By synchronizing users from **biira.com** to **biira.store**, I was able to streamline user management and ensure that users had consistent identities across both environments. The combination of **IDFix**, **Entra ID Connect**, and careful troubleshooting helped me achieve a successful integration between on-prem AD and Entra ID.

If you have any questions or want to know more about the process, feel free to reach out. I’d be happy to share more insights!

# Project: Implementing Self-Service Password Reset (SSPR) in a Hybrid Environment

**Overview**:  
This project details the implementation of Microsoft Entra ID’s Self-Service Password Reset (SSPR) in a hybrid setup integrated with an on-premises Active Directory using Password Hash Synchronization. The solution enhances user autonomy in password management while maintaining synchronization across environments.

---

### **Key Licensing Information**

1. **Cloud-Only Accounts**:
   - For cloud-only users in Microsoft Entra ID, SSPR is available **without additional licenses**, as it is included in the **free tier** of Microsoft Entra ID.

2. **Hybrid Environment (On-Premises Integration)**:
   - To enable SSPR with **password writeback** (required for hybrid users to sync password changes back to the on-premises Active Directory), you need either:  
     - **Microsoft Entra ID P1 License**, or  
     - **Microsoft Entra ID P2 License**.

3. **Microsoft 365 or Office 365 Subscriptions**:
   - If you’re using **Microsoft 365** or **Office 365** subscription plans (such as Enterprise E1, E3, or E5), these plans come with **Azure AD Premium P1** or **P2 licenses**, which include support for **SSPR** and additional security features.

4. **Advanced Features with P2**:
   - A P2 license includes all P1 features, with added security capabilities like Identity Protection. While not necessary for basic SSPR, these advanced features may enhance your deployment, particularly with risk-based conditional access.

---

### **Additional Key Requirements**

- **Azure AD Connect**:
  - Password Hash Synchronization and Password Writeback must be enabled for hybrid environments.
- **Authentication Methods**:
  - Users must verify their identity using configured methods (e.g., email, mobile app, security questions).
- **Security Group**:
  - Use a Security Group to scope the users who will use SSPR.

---

**Full Implementation**:  
For a step-by-step guide and practical demonstration of this project, check out my YouTube channel:  
👉 [Watch the Full Implementation on YouTube](https://www.youtube.com/playlist?list=PLfeBBu8bvwXmzHpNOnqLci5VEiWn248iC)

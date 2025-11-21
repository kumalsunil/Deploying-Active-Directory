<p align="center">
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/88de56f6-0e01-4acc-89c1-55ebfc5c6720" />
</p>

## 💾 Active Directory Deployment and Client Join Guide

This guide documents the steps taken to install Active Directory Domain Services (AD DS) and join a client machine to the new domain, `mydomain.com`.

---

## 1. Deploy Active Directory Domain Services (AD DS)

This step covers installing the AD DS role and promoting the server **DC-1** to be the first Domain Controller (DC) in a new forest.

### 1.1 Install the AD DS Role

1.  Log in to **DC-1** with an administrative account.
2.  Open **Server Manager** and click **Manage** > **Add Roles and Features**.
3.  Follow the wizard to install **Active Directory Domain Services**. (The role is installed before the promotion step).
    * _Note: This image shows the Server Manager Dashboard where the "Add roles and features" option is accessible, as well as the initial Run prompt._

| Description | Screenshot |
| :--- | :--- |
| **Server Manager Dashboard** | <img width="1043" height="453" alt="Screenshot (1)" src="https://github.com/user-attachments/assets/6fba7e36-49d6-4434-8dc0-f73a4edfd8ef" /> |

### 1.2 Promote the Server to a Domain Controller

1.  After the role installation, click the notification flag in Server Manager and select **Promote this server to a domain controller**.
2.  In the **Deployment Configuration** step, select **Add a new forest**.
3.  Set the **Root domain name** to `mydomain.com`.
4.  Follow the remaining prompts (set DSRM password, etc.) and click **Install**. The server will restart.

| Description | Screenshot |
| :--- | :--- |
| **Deployment Configuration** |<img width="949" height="726" alt="Screenshot (3)" src="https://github.com/user-attachments/assets/52e3135b-686c-481a-8ee3-3c5e42ad652c" /> |

---

## 2. Create Organizational Units and Domain Admin User

After the domain is functional, new Organizational Units (OUs) and a dedicated administrative user were created for security and organizational purposes.

### 2.1 Create Organizational Units (OUs)

1.  On **DC-1**, open the **Active Directory Users and Computers (ADUC)** console.
2.  Right-click the domain name (`mydomain.com`) and select **New** > **Organizational Unit**.
3.  Create the following OUs:
    * `EMPLOYEES`
    * `ADMINS` (nested under `EMPLOYEES` or created separately, as shown in the screenshot structure).

| Description | Screenshot |
| :--- | :--- |
| **Creating the 'EMPLOYEES' OU** |<img width="570" height="515" alt="Screenshot (4)" src="https://github.com/user-attachments/assets/fe633a89-01fa-4893-b867-df7959c42366" />|

### 2.2 Create and Elevate the `Jane Doe` Admin Account

1.  Create a new user named **Jane Doe** with the username `jane_admin` within the `ADMINS` OU.
2.  Open the user's **Properties**, go to the **Member Of** tab, and add the **Domain Admins** security group. This elevates the user's permissions.

| Description | Screenshot |
| :--- | :--- |
| **Adding User to Domain Admins** |<img width="1100" height="768" alt="Screenshot (6)" src="https://github.com/user-attachments/assets/7388863a-4fc2-4114-9a92-dd7c692bfb8e" /> |

---

## 3. Join Client-1 to the Domain

The final step is to make the client machine a member of the newly created `mydomain.com` domain.

### Join Client-1 to `mydomain.com`

1.  Log in to **Client-1** using the local administrative account.
2.  Navigate to **System Properties** > **Computer Name** tab and click **Change...**.
3.  Select the **Domain** radio button and enter your full domain name: **`mydomain.
4.  When prompted, enter the credentials of a domain administrator (e.g., `mydomain.com\jane_admin`).
5.  Restart **Client-1** to complete the domain join.

| Description | Screenshot |
| :--- | :--- |
| **Domain Join Configuration** |<img width="775" height="666" alt="Screenshot (7)" src="https://github.com/user-attachments/assets/36af00dc-8fba-43ca-860b-edff9d2cde9f" /> |

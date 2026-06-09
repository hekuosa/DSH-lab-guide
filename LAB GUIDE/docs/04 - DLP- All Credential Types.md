# Data Loss Prevention - All Credential Types

Reference: [Create and deploy a data loss prevention policy](https://learn.microsoft.com/en-us/purview/dlp-create-deploy-policy)

This section uses Microsoft Purview Data Loss Prevention (DLP) to prevent unauthorized sharing of credential-related information. The custom DLP policy you create detects credential data and blocks its external sharing through Exchange Online and Microsoft Teams. The configuration combines sensitive-information detection, sharing conditions, access restrictions, and user notifications to reduce the risk of accidental or intentional data leakage.

## Block external credential sharing

1. Go to **Solutions** > **Data loss prevention** > **Policies**, then select **Create policy**.
2. Select **Enterprise applications & devices**.
3. Select **Category:** Custom and **Regulations:** Custom policy, then select **Next**.
4. On **Name your DLP policy**, set:
   - **Policy name:** `Block external sharing of credentials`
   - **Description:** Prevents sharing of login credentials and secrets with external users using Microsoft Purview DLP.

5. Skip **Assign Admin units**.
6. On **Locations**, select **Microsoft Teams** and **Exchange Online**, then **Next**.

   ![DLP policy locations: Microsoft Teams and Exchange Online selected](../images/lab-guide-developer-subscription-032-503bf4c1.png)

7. On **Policy settings**, select **Create or customize advanced DLP rules**, then **Next**.
8. Select **Create a rule** and configure:
   - **Name:** `Block external sharing of credentials`
   - **Description:** `Block external sharing of credentials`
   - **Conditions:**
     - Content contains: Sensitive info types > **All Credential Types** (default settings: Medium confidence, instance count 1 to any)
     - Add condition: **Content is shared from Microsoft 365** > **with people outside my organization**

   ![Adding the All Credential Types sensitive info type as the DLP condition](../images/lab-guide-developer-subscription-033-9bd46f7d.png)

   ![Adding the external-sharing condition to the DLP rule](../images/lab-guide-developer-subscription-034-403637a3.png)

   - **Actions:**
     - Add action: **Restrict access or encrypt the content in Microsoft 365 locations** > **Block access for everyone**

   ![Restrict access action set to block everyone](../images/lab-guide-developer-subscription-035-38c40ba4.png)

   - **User notifications:** On
     - Notify users in the Microsoft 365 service with a policy tip or email notification
     - Notify: The person who sent, shared, or modified the content
     - Policy tip text: _For security reasons, sharing login credentials or secrets with external users is not allowed._

   ![DLP policy tip text and notification recipients configured](../images/lab-guide-developer-subscription-036-5829fe07.png)

9. On **Policy mode**, select **Turn the policy on immediately**, then complete the wizard to finish.

> **Verify:** the **Block external sharing of credentials** policy is listed under **DLP policies** with status **On**. You'll exercise it in [Phase 4](04-after-the-lab.md).

## Notify users who store credentials in OneDrive or SharePoint

1. Go to **Data loss prevention** > **Policies** > **Create policy**.
2. Select **Custom policy**.
3. Give the policy a name and description.
4. **Locations:** OneDrive and SharePoint.
5. Create a rule with the condition: **Content contains** > **Sensitive info types** > **All Credential Types**, instance count **2 to any**.
6. **Actions:** Block access for everyone.
7. **User notifications:** On — notify the users who sent, shared, or last modified the content.
8. **Email notifications:** turn on, then **Preview and edit notification email** to customize the sender display name, email subject, and email body.

For a customised email body, you can use the following example or create your own.

[Example body HTML](../materials/UserNotification.html)

9. Turn the policy on.

> **Verify:** the policy is listed under **DLP policies** with status **On**.
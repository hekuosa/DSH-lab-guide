# HR

## Client-side recommended labeling in action

Upload an HR document from [`test-files/HR test files/`](../test-files/HR%20test%20files/) to your admin user's OneDrive or any SharePoint site. Open the document in a web browser to trigger a policy tip recommending a sensitivity label. Alternatively, copy and paste content from any HR document in that folder into a blank document in your demo user's OneDrive.

You will then be prompted to apply a label to the document.

![Office policy tip recommending the HR sensitivity label on a document](../images/after-the-lab-developer-subscription-039-1536bbee.png)

Apply the label.

![HR sensitivity label applied to the document with the Classified as Highly Confidential footer](../images/after-the-lab-developer-subscription-040-d904f6d2.png)

#### Provide a justification to lower the label

If you try to change the label to a lower-priority label, you will be prompted to provide a business justification.

![Justification prompt shown when downgrading a sensitivity label](../images/after-the-lab-developer-subscription-041-561003b7.png)

> **Verify:** the justification dialog appears and the label change is logged in **Microsoft Purview** > **Audit**.

# Project DogOps

## Automatic client-side labeling

Paste content from any DogOps document in [`test-files/DogOps Test Files/`](../test-files/DogOps%20Test%20Files/) into a blank document in your admin user's OneDrive.

A policy tip confirms that the Highly Confidential/DogOps label has been applied automatically.

![Policy tip showing that the DogOps label was applied automatically based on detected content](../images/after-the-lab-developer-subscription-042-ffb97246.png)

## Automatic service-side labeling in action

Upload the files in [`test-files/DogOps Test Files/`](../test-files/DogOps%20Test%20Files/) to a public SharePoint site. They are automatically labeled as Project DogOps within a few hours. You can confirm this in **Microsoft Purview** > **Activity explorer**.

![Activity explorer showing files auto-labeled as Highly Confidential/DogOps](../images/after-the-lab-developer-subscription-043-e4c54831.png)

> **Verify:** in **Auto-labeling policies**, the simulation completes and the **Items to review** count matches the files you uploaded.

## Encryption

### User in the same organization

Sign in as a user that is **not** a member of the U.S. Sales group (for example `nestorw@<tenantname>.onmicrosoft.com`) and try to open any DogOps document. Access should be denied.

![Access-denied message in Word for a non–U.S. Sales user opening a DogOps document](../images/after-the-lab-developer-subscription-044-36ce1c46.png)

![Access-denied screen in SharePoint for a non–U.S. Sales user opening a DogOps document](../images/after-the-lab-developer-subscription-045-2cc6b2e6.png)

### External user

Attach a DogOps file as a copy and send it to someone outside the demo organization. The document remains encrypted at the recipient's end.

> **Verify:** the external recipient sees a sign-in / access-request screen instead of the document content.

# DLP 

## Block external credential sharing

Send the contents of [`data/fake-credentials.txt`](../data/fake-credentials.txt) to an external email address (for example a personal Gmail you control). The DLP policy blocks the message and you receive a notification.

> **Note:** if `data/fake-credentials.txt` is not present in your clone, paste a few realistic-looking-but-fake credential lines (e.g. `username: alice@contoso.com`, `password: P@ssw0rd!`, `aws_secret_access_key=...`) into the body of the email instead. Never use real credentials.

> **Verify:** in **Microsoft Purview** > **Data loss prevention** > **Activity explorer**, the email appears with action **Blocked** for the **Block external sharing of credentials** policy.

## Notify users who store credentials in OneDrive or SharePoint

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
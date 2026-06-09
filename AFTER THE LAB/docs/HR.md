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


# DLP 

## Block external credential sharing

Send the contents of [`test-files/sample_fake_credentials.docx`](../test-files/sample_fake_credentials.docx) to an external email address (for example a personal Gmail you control or <meganb293157@gmail.com>). The DLP policy blocks the message and you receive a notification.

> **Note:**  Never use real credentials.

> **Verify:** in **Microsoft Purview** > **Data loss prevention** > **Activity explorer**, the email appears with action **Blocked** for the **Block external sharing of credentials** policy.

## Notify users who store credentials in OneDrive or SharePoint

1. As the test end user (e.g. Nestor Wilke), save two or more fake credentials into a Word document and upload it to OneDrive (or save directly into a OneDrive-synced folder)
2. Wait for the DLP scan to evaluate the file at rest.
3. The user receives an email with subject Action required: Sensitive data blocked. 

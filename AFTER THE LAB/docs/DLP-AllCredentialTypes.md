# DLP 

## Block external credential sharing

Send the contents of [`data/fake-credentials.txt`](../data/fake-credentials.txt) to an external email address (for example a personal Gmail you control). The DLP policy blocks the message and you receive a notification.

> **Note:** if `data/fake-credentials.txt` is not present in your clone, paste a few realistic-looking-but-fake credential lines (e.g. `username: alice@contoso.com`, `password: P@ssw0rd!`, `aws_secret_access_key=...`) into the body of the email instead. Never use real credentials.

> **Verify:** in **Microsoft Purview** > **Data loss prevention** > **Activity explorer**, the email appears with action **Blocked** for the **Block external sharing of credentials** policy.

## Notify users who store credentials in OneDrive or SharePoint

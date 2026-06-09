# Insider Risk Management — Departing Agent Data Theft

This scenario simulates a departing employee exfiltrating data, using an HR data connector to feed resignation events into Insider Risk Management.

## Create the resignation CSV file

1. Open the **Employee Resignations Simulation Template** Excel file.
2. Populate column A with the email addresses of the participating users. You can use the demo user Isaiah Langer (`IsaiahL@<tenantname>.onmicrosoft.com`) or any other user in your tenant.
3. The template includes pre-configured values for `<ResignationDate>` (midnight on the current day) and `<LastWorkingDate>` (10 days later).

   > _To use different dates, update the formulas in columns B and C using ISO 8601 format (YYYY-MM-DD). See [ISO 8601 date and time format](https://www.iso.org/iso-8601-date-and-time-format.html)._

4. In Excel, select **File** > **Export** > **Change File Type** and choose **CSV (Comma delimited) (\*.csv)**.
5. Select **Save a copy** and save the CSV to the local disk as `HR-Export`.

## Register an application in Microsoft Entra ID

1. Sign in to [Microsoft Entra](https://entra.microsoft.com) and go to **App registrations**.
2. Select **New registration**.
3. Enter `DSH-HRconnector` as the application name.
4. Under **Supported account types**, select **Single tenant only — _tenantname_**.
5. Leave **Redirect URI** at the default setting.
6. Select **Register**.
7. On the **Overview** page, note the **Application (client) ID** and **Directory (tenant) ID**.
8. In the left navigation, select **Certificates & secrets**.
9. Under **Client secrets**, select **+ New client secret**.
10. Add a description (for example `DSH-HRconnector secret`) and set the expiry to 6 months.
11. Select **Add** and note the **value** of the client secret — you won't be able to see it again after leaving the page.

## Create the HR connector in Microsoft Purview

1. Sign in to [Microsoft Purview](https://purview.microsoft.com/).
2. In the left navigation, select **Settings**.
3. On the **Settings** card, expand **Data connectors**.
4. Select **All connectors**.
5. Search for **HR**, then select the **HR** connector.
6. On the HR page, select **Add connector**.
7. On the **Terms of Service** page, select **Accept**.
8. On **Add credentials for connecting to your data source**, paste the **Application (client) ID** from the app you registered.
9. Enter `DSH-HRconnector` as the connector name, then select **Next**.
10. On **Choose the HR scenario you want to include**, select **Employee Resignation**, then **Next**.
11. On **Decide whether to map data manually or from a sample file**, set **What's the format of the file you would like to import?** to **.csv file – Comma delimited**.
12. Under **File mapping method**, select **Upload a sample file (recommended)**, then **Upload sample file**.
13. Open the `HR-Export.csv` file you saved earlier, then select **Next**.
14. On **File mapping details**, select **Employee resignation** to show the individual field mapping (see the image below).

   ![Map the HR scenarios to the columns in your file](../images/map-the-hr-scenarios-to-the-columns-in-your-file.png)

15. Select **Next**.
16. On the **Review and finish** page, select **Finish**.
17. On the **Your connector was created** page, note the **Connector Job ID** for later use.

   ![Your connector was created, showing the Connector Job ID](../images/your-connector-was-created.png)

18. Select **Done**.

## Run the sample script to upload your HR data

> _Add the `webhook.ingestion.office.com` domain to your organization's firewall allowlist. If you block this domain, the script won't run._

The final step is to run a sample script that uploads the HR data from the CSV file to the connector.

1. On the **Data connectors** overview page, on the **My Connectors** tab, select your `DSH-HRconnector`.
2. On the connector details page, select **Get sample script**.

   ![DSH-HRconnector details page with the Get sample script button](../images/dsh-hrconnector-get-sample-script.png)

3. On the **microsoft/m365-compliance-connector-sample-scripts** GitHub page, download the script and save it as `DSH-HRConnectorUpload.ps1`.
4. On the local workstation, open a Windows PowerShell session **as administrator**.
5. Change to the directory where you saved the script.
6. Run the script with the following parameters:

   ```powershell
   .\DSH-HRConnectorUpload.ps1 -tenantId <tenantId> -appId <Application (client) ID> -appSecret <Client secret value> -jobId <jobId / connectorId> -FilePath '<csvFilePath>'
   ```

   When the script runs successfully, you should see output similar to the image below, indicating the data upload succeeded.

   ![PowerShell output showing a successful HR connector upload](../images/hrconnectorupload-successful.png)

> **Verify:** in **Microsoft Purview** > **Data connectors**, the connector shows a recent successful upload.


# Create MI5 custom SIT

## Create a keyword dictionary from a file using PS

1. To begin, you need to connect to Security & Compliance PowerShell.
2. Save keywords text file locally (Has to be saved with Unicode encoding. To if needed to check > In Notepad, navigate to > Save As > Encoding > Unicode.)
3. Read the file into a variable by running this cmdlet:

 ```powershell
  $fileData = [System.IO.File]::ReadAllBytes('<filename>')
   ```

4. Read the file into a variable by running this cmdlet:

```powershell
  New-DlpKeywordDictionary -Name <mark><name><mark>-Description <mark> <description> <mark> -FileData $fileData
   ```


## Create an Insider Risk Management policy

1. Go to **Insider Risk Management** > **Policies** > **Create policy** > **Quick policy** > **Data theft from Microsoft 365 apps by users leaving your org**.
2. Select **Customize**.
3. **Policy template** — select **Next**.
4. **Name and description:**
   - **Name:** `Departing agent data theft`
   - **Description:** Detect potential data theft from Microsoft 365 apps by users leaving your org.
   - Select **Next**.
5. **Users and groups** — select **All users, groups, and adaptive scopes**, then **Next**.
6. **Exclusions** — no exclusions, then **Next**.
7. **Content to prioritize** — select **SharePoint sites** and **Sensitive info types**, then **Next**:
   - **SharePoint sites** — add the **Universal Exports** site, then **Next**.
   - **Sensitive info types** — add the **Spectre_007** sensitive info type, then **Next**.
   - **Scoring** — select **Get alerts only for activity that includes priority content**, then **Next**.
8. **Triggering events** — select **(Recommended) HR data connector events**, then **Next**.
9. **Indicators:**
   - **Office indicators:**
     - Downloading content from SharePoint
     - Sending email with attachments to recipients outside the organization
     - Sending email with attachments to free public domains
     - Sending email with attachments to self
   - **Detection options:**
     - **Sequence detection** — select **Download from M365 location then exfiltrate** and **Download from M365 location then exfiltrate, then delete**.
     - **Cumulative exfiltration detection** — leave unselected.
     - **Risk score boosters** — select **Activity is above the user's usual activity for that day**, then **Next**.

   ![Selected Insider Risk Management detection options](../images/irm-selected-detectionoptions.png)

   - **Indicator thresholds** — select **Choose your own thresholds**:
     - **Office indicators:**
       - Downloading content from SharePoint — 3, 6, 9
       - Sending email with attachments to recipients outside the organization — 1, 2, 3
       - Sending email with attachments to free public domains — 1, 2, 3
       - Sending email with attachments to self — 2, 4, 6
     - **Sequence detection:**
       - Download from M365 location then exfiltrate — 1, 2, 3
       - Download from M365 location then exfiltrate, then delete — 1, 2, 3
     - **Risk score boosters** — Activity is above the user's usual activity for that day (default).
     - Select **Next**.
10. **Review settings and finish** — select **Submit**.
11. On the confirmation page, select **Done**.

> **Verify:** the **Departing agent data theft** policy appears under **Insider Risk Management** > **Policies** with status **On**.

## Generate sample activity (days 1–3)

Over the first three days, perform the following actions as the departing user to generate alerts:

- Download 2 files from SharePoint to OneDrive.
- Send 1 email to a recipient outside the organization.
- Send 1 email to a public (free) domain.

### Universal Exports document library

1. On the **Universal Exports** SharePoint site, create a new document library named `MI5`, labeled **Internal Exception**.
2. Upload the **James Bond — Daily briefing** and **Project documents** folders.

   > _These are automatically given the **Internal Exception** label._

### Follow-up DLP automation

- Configure a DLP policy on **Credentials** with a Power Automate action that emails the user a "do not store credentials" reminder.
- **Locations:** SharePoint Online and OneDrive.

> **Verify:** in **Insider Risk Management** > **Alerts**, alerts are generated for the departing user after the simulated activity and HR connector events are processed.

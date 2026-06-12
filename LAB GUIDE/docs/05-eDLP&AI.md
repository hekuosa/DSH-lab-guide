# Data Loss Prevention

## DSPM — extend insights for data discovery 

> **Note:** Requires eDLP. If you have an Azure subscription, you can set up an Azure Virtual Desktop environment and onboard it to Microsoft Defender for Endpoint to try out eDLP features.


1. Go to **DSPM** > **Tasks and actions** > **Setup tasks**.
2. Select **Extend your insights for data discovery** and create the following policies:
   - Detect when users visit AI sites
   - Detect sensitive info pasted or uploaded to AI sites


# Restrict copy paste of sensitive data to AI sites

1. Create a DLP policy with the following conditions:
   - Locations > Devices
   **Rule**
   - Content contains: Sensitive info types > Select any relevant SITs e.g. ProjectDogOps & MI5
   - Actions: Service domain and browser activities, see images below for example configuration.
  
     ![Audit or restict activities on devices](../images/edlp_ai_rule_img1.png)


     ![Sensitive service domain group restriction(s) configured](../images/edlp_ai_sensitive_service_domain_restrictions.png)

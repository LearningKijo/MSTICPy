# msticpy - tips Getting Started
First of all, I am going to cover leveraging msticpy in **"Local Machine"** environment, NOT in Notebooks, Microsoft Sentinel.
Also, I would like to share some tips for each part.
1. Creating [a Client App for M365D](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/exposed-apis-create-app-webapp?view=o365-worldwide)
2. install [Anaconda](https://www.anaconda.com/)
3. install [msticpy](https://github.com/microsoft/msticpy)
4. Configure [msticpyconfig.yaml](https://learn.microsoft.com/en-us/azure/sentinel/notebooks-msticpy-advanced?tabs=windows#set-an-environment-variable-for-your-msticpyconfigyaml-file)

## 1. Creating a Client App for M365D
When looking for API permissions, you could be confused whether you should choose an old name or not. To request API permissions appropriately, please type an old name - Microsoft Threat Protection and WindowsDefenderATP.
> Microsoft 365 Defender : Microsoft Threat Protection <br>
Microsoft Defender for Endpoint : WindowsDefenderATP

![image](https://user-images.githubusercontent.com/120234772/219311297-c5d520d0-0d77-40be-bf7a-28d5c47e0ab5.png)

**Please save the secret once you created !!** 
> Client secret values cannot be viewed, except for immediately after creation. <br>
Be sure to save the secret when created before leaving the page.

![image](https://user-images.githubusercontent.com/120234772/219384551-7a21c12c-b2c1-4826-8753-76888f8eabed.png)

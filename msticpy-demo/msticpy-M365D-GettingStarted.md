# msticpy - Microsoft 365 Defender part1
Getting Started : I am going to cover the fundamental use of msticpy for Microsoft 365 Defender.<br>

1. Connect to the provider, Microsoft 365 Defender
2. Confirm the available lists in msticpy, Microsoft 365 Defender
3. Try a query in msticpy, Microsoft 365 Defender
4. Understand the detail of query in msticpy, Microsoft 365 Defender

## 0. Prerequisite
Before connecting to the provider, Microsoft 365 Defender, a few preparations are necessary - [MSTICPy | Microsoft 365 Defender Provider](https://msticpy.readthedocs.io/en/latest/data_acquisition/DataProv-MSDefender.html). In this page, I am covering the use for msticpy, Microsoft 365 Defender, on the local device, NOT Notebooks, Microsoft Sentinel.

## 1. Connect to the provider, Microsoft 365 Defender
![image](https://user-images.githubusercontent.com/120234772/218461249-e3fc945d-4d49-471b-8b04-ea0bc6332d37.png)

## 2. Confirm the available lists in msticpy, Microsoft 365 Defender 
![image](https://user-images.githubusercontent.com/120234772/218461392-97fa287a-94ec-40a0-a229-5d200a963ef4.png)

  When you typed **"md_prov.list_queries()"**, you can see there are a number of queries for Microsoft 365 Defender.
> Output :
['M365D.application_alerts',
 'M365D.host_alerts',
 'M365D.ip_alerts',
 'M365D.list_alerts',
 'M365D.list_alerts_with_evidence',
 'M365D.mail_message_alerts',
 'M365D.mailbox_alerts',
 'M365D.process_alerts',
 'M365D.registry_key_alerts',
 'M365D.sha1_alerts',
 'M365D.sha256_alerts',
 'M365D.url_alerts',
 'M365D.user_alerts',
 'MDATP.file_path',
 'MDATP.host_connections',
 'MDATP.ip_connections',
 'MDATP.list_connections',
 'MDATP.list_filehash',
 'MDATP.list_files',
 'MDATP.list_host_processes',
 'MDATP.process_cmd_line',
 'MDATP.process_creations',
 'MDATP.process_paths',
 'MDATP.protocol_connections',
 'MDATP.url_connections',
 'MDATP.user_files',
 'MDATP.user_logons',
 'MDATP.user_network',
 'MDATP.user_processes',
 'MDATPHunting.accessibility_persistence',
 'MDATPHunting.av_sites',
 'MDATPHunting.b64_pe',
 'MDATPHunting.brute_force',
 'MDATPHunting.cve_2018_1000006l',
 'MDATPHunting.cve_2018_1111',
 'MDATPHunting.cve_2018_4878',
 'MDATPHunting.doc_with_link',
 'MDATPHunting.dropbox_link',
 'MDATPHunting.email_link',
 'MDATPHunting.email_smartscreen',
 'MDATPHunting.malware_recycle',
 'MDATPHunting.network_scans',
 'MDATPHunting.powershell_downloads',
 'MDATPHunting.service_account_powershell',
 'MDATPHunting.smartscreen_ignored',
 'MDATPHunting.smb_discovery',
 'MDATPHunting.tor',
 'MDATPHunting.uncommon_powershell',
 'MDATPHunting.user_enumeration',
 'MDE.accessibility_persistence',
 'MDE.av_sites',
 'MDE.b64_pe',
 'MDE.brute_force',
 'MDE.cve_2018_1000006l',
 'MDE.cve_2018_1111',
 'MDE.cve_2018_4878',
 'MDE.doc_with_link',
 'MDE.dropbox_link',
 'MDE.email_link',
 'MDE.email_smartscreen',
 'MDE.file_path',
 'MDE.host_connections',
 'MDE.ip_connections',
 'MDE.list_connections',
 'MDE.list_filehash',
 'MDE.list_files',
 'MDE.list_host_processes',
 'MDE.malware_recycle',
 'MDE.network_scans',
 'MDE.powershell_downloads',
 'MDE.process_cmd_line',
 'MDE.process_creations',
 'MDE.process_paths',
 'MDE.protocol_connections',
 'MDE.service_account_powershell',
 'MDE.smartscreen_ignored',
 'MDE.smb_discovery',
 'MDE.tor',
 'MDE.uncommon_powershell',
 'MDE.url_connections',
 'MDE.user_enumeration',
 'MDE.user_files',
 'MDE.user_logons',
 'MDE.user_network',
 'MDE.user_processes']

## 3. Try a query in msticpy, Microsoft 365 Defender
Under [msticpy | Data Queries Reference](https://msticpy.readthedocs.io/en/latest/data_acquisition/DataQueries.html#queries-for-microsoft-365-defender), it covers the use of Microsoft 365 Defender. Below is an example that shows the alert lists in Microsoft 365 Defender.

Example) 
| QueryGroup | Query | Description | Req-Params | Table | 
| :-- | :-- | :-- | :-- | :-- |
| M365D | list_alerts | Retrieves list of alerts | end (datetime), start (datetime) | AlertInfo |
> Ex : md_prov.M365D.list_alerts(start=-7)

![image](https://user-images.githubusercontent.com/120234772/218467980-43b40976-1d28-4149-824b-4e24bb17a172.png)


> Ex : md_prov.M365D.list_alerts(start=-30, add_query_items="| summarize count() by Severity")

![image](https://user-images.githubusercontent.com/120234772/219263196-a71de44e-862a-49d6-86e9-4d9c59f3432f.png)

By adding **add_query_items="xxxxxx"** to the date, you can get the enriched data as well. As you can see the next section - 4. Understand the detail of query in msticpy, {add_query_items} | [code: 34] was available for each query. 

## 4. Understand the detail of query in msticpy, Microsoft 365 Defender
For instance, when you use **"M365D.list_alerts"**, this query is working in backend in kql_mdatp_alerts.yaml.

```
25 sources:
26   list_alerts:
27    description: Retrieves list of alerts
28    metadata:
29    args:
30      query: "
31        {table}
32        | where Timestamp >= datetime({start})
33        | where Timestamp <= datetime({end})
34        {add_query_items}"
35      uri: None
36    parameters:
 ```
> GitHub : msticpy/msticpy/data/queries/m365d/[kql_mdatp_alerts.yaml](https://github.com/microsoft/msticpy/blob/main/msticpy/data/queries/m365d/kql_mdatp_alerts.yaml)

#### Disclaimer 
The views and opinions expressed herein are those of the author and do not necessarily reflect the views of company.

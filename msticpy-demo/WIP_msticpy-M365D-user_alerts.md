# msticpy - M365D user_alerts
```
user_alerts:
    description: Lists alerts associated with a specified user
    metadata:
    args:
      query: '
        {table}
        | where Timestamp >= datetime({start})
        | where Timestamp <= datetime({end})
        | join kind=inner (AlertEvidence
        | where Timestamp >= datetime({start})
        | where Timestamp <= datetime({end})) on AlertId
        | where EntityType =~ "User"
        | where AccountName =~ "{account_name}"
        {add_query_items}'
    parameters:
      account_name:
        description: The user name
        type: str
```
> **GitHub** : msticpy/msticpy/data/queries/m365d/[kql_mdatp_alerts.yaml](https://github.com/microsoft/msticpy/blob/main/msticpy/data/queries/m365d/kql_mdatp_alerts.yaml)
> 
## M365D | user_alerts | Lists alerts associated with a specified user
```
from msticpy.data.data_providers import QueryProvider

md_prov = QueryProvider("M365D")

md_prov.connect()

md_prov.M365D.user_alerts(start=-30, account_name="SteveM365D", add_query_items="| where ServiceSource == 'Microsoft Defender for Endpoint'| summarize Informational = countif(Severity == 'Informational'), Low = countif(Severity == 'Low'), Medium = countif(Severity == 'Medium'), High = countif(Severity == 'High') by bin(Timestamp, 1d)")
```
![image](https://user-images.githubusercontent.com/120234772/221608537-fbff7d45-14c3-4ac2-8d79-da8c5e931825.png)

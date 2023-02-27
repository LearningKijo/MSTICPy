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

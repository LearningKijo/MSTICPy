# msticpy - M365D process_alerts

M365D - process_alerts - Lists alerts associated with a specified process
```
  process_alerts:
    description: Lists alerts associated with a specified process
    metadata:
    args:
      query: '
        {table}
        | where Timestamp >= datetime({start})
        | where Timestamp <= datetime({end})
        | join kind=inner (AlertEvidence
        | where Timestamp >= datetime({start})
        | where Timestamp <= datetime({end})) on AlertId
        | where EntityType =~ "Process"
        | where FileName =~ "{file_name}"
        {add_query_items}'
    parameters:
      file_name:
        description: The process name
        type: str
        aliases:
          - process
```
GitHub : msticpy/msticpy/data/queries/m365d/[kql_mdatp_alerts.yaml](https://github.com/microsoft/msticpy/blob/main/msticpy/data/queries/m365d/kql_mdatp_alerts.yaml)


## M365D | process_alerts | Lists alerts associated with a specified process

Case1 : tracking alerts, which are associated with "reg.exe"
```
md_prov.M365D.process_alerts(start=-30, file_name="reg.exe")
```
![image](https://user-images.githubusercontent.com/120234772/220569738-3b9a3552-7605-479b-97ad-b2b864655d0a.png)


Case2 : tracking alerts, which are associated with "net.exe" + added an additional query to list commands for each alert.
```
alerts_df = md_prov.M365D.process_alerts(start=-30, file_name="net.exe", add_query_items="| summarize make_set(ProcessCommandLine) by AlertId, Title")
alerts_df.to_csv('alerts.csv', index=False)
```
![image](https://user-images.githubusercontent.com/120234772/219591170-6b256fd0-f304-46ff-87ad-de5516873459.png)

![image](https://user-images.githubusercontent.com/120234772/221079025-ae0c25e5-22c3-47ef-95e5-2e51e795301c.png)

![image](https://user-images.githubusercontent.com/120234772/221079291-e1c3190c-2612-4887-a9ea-c05d77342093.png)


#### Disclaimer
The views and opinions expressed herein are those of the author and do not necessarily reflect the views of company.





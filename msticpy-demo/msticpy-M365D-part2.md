# msticpy - Microsoft 365 Defender part2

// WIP <br>

M365D | process_alerts | Lists alerts associated with a specified process
```
md_prov.M365D.process_alerts(start=-30, file_name="net.exe", add_query_items="| summarize make_set(ProcessCommandLine) by AlertId, Title")
```
![image](https://user-images.githubusercontent.com/120234772/219591170-6b256fd0-f304-46ff-87ad-de5516873459.png)

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
msticpy/msticpy/data/queries/m365d/kql_mdatp_alerts.yaml


```
registry_key_alerts:
    description: Lists alerts associated with a specified registry key
    metadata:
    args:
      query: '
        {table}
        | where Timestamp >= datetime({start})
        | where Timestamp <= datetime({end})
        | join kind=inner (AlertEvidence
        | where Timestamp >= datetime({start})
        | where Timestamp <= datetime({end})) on AlertId
        | where EntityType =~ "RegistryValue"
        | where RegistryKey =~ "{key_name}"
        {add_query_items}'
    parameters:
      key_name:
        description: The Registry key 
```

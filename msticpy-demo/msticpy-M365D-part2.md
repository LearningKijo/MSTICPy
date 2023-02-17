# msticpy - Microsoft 365 Defender part2
In progress
> md_prov.M365D.process_alerts(start=-30, file_name="net.exe", add_query_items="| summarize make_set(ProcessCommandLine) by AlertId, Title")
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

# msticpy - Microsoft 365 Defender part2
In progress
> md_prov.MDE.process_cmd_line(start=-10, cmd_line="net.exe", add_query_items="| summarize make_set(ProcessCommandLine) by DeviceId, DeviceName")
```
  process_cmd_line:
    description: Lists all processes with a command line containing a string
    metadata:
    args:
      query: '
        {table}
        | where {time_column} >= datetime({start})
        | where {time_column} <= datetime({end})
        | where ProcessCommandLine contains "{cmd_line}"
        {add_query_items}'
    parameters:
      cmd_line:
        description: Command line artifact to search for
        type: str
```
msticpy/msticpy/data/queries/m365d/kql_mdatp_process.yaml

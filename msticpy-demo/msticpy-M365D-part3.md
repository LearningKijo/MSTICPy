##  MDE | process_cmd_line | Lists all processes with a command line containing a string
The attacker might execute the command to turn off Microsoft Defender Antivirus. To list all activities in relation to disabling antivirus tool by registry key, execute this command.
```
md_prov.MDE.process_cmd_line(start=-30, cmd_line="DisableAntiSpyware")
```

![image](https://user-images.githubusercontent.com/120234772/220122881-85dbd545-920d-4e0c-abf5-742fe7d9fc69.png)



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
GitHub : msticpy/msticpy/data/queries/m365d/[kql_mdatp_process.yaml](https://github.com/microsoft/msticpy/blob/main/msticpy/data/queries/m365d/kql_mdatp_process.yaml)


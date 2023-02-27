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
> **GitHub** : msticpy/msticpy/data/queries/m365d/[kql_mdatp_alerts.yaml](https://github.com/microsoft/msticpy/blob/main/msticpy/data/queries/m365d/kql_mdatp_alerts.yaml)


## M365D | process_alerts | Lists alerts associated with a specified process

Case1 : Tracking alerts associated with the use of 'reg.exe'.
```
from msticpy.data.data_providers import QueryProvider

md_prov = QueryProvider("M365D")

md_prov.connect()

md_prov.M365D.process_alerts(start=-30, file_name="reg.exe")
```
![image](https://user-images.githubusercontent.com/120234772/220569738-3b9a3552-7605-479b-97ad-b2b864655d0a.png)


Case2 : Tracking alerts associated with "net.exe" and adding an additional query to list commands for each alert. Then, exporting the results to a CSV file.
```
from msticpy.data.data_providers import QueryProvider

md_prov = QueryProvider("M365D")

md_prov.connect()

alerts_df = md_prov.M365D.process_alerts(start=-30, file_name="net.exe", add_query_items="| summarize make_set(ProcessCommandLine) by AlertId, Title")

alerts_df.to_csv('alerts.csv', index=False)
```
![image](https://user-images.githubusercontent.com/120234772/219591170-6b256fd0-f304-46ff-87ad-de5516873459.png)


![image](https://user-images.githubusercontent.com/120234772/221111523-bafad4f8-4b95-4f55-90e2-817f1dba853f.png)
> Figure 1. CSV file in jupyter notebook

![image](https://user-images.githubusercontent.com/120234772/221079291-e1c3190c-2612-4887-a9ea-c05d77342093.png)
> Figure 2. CSV file in Excel

#### Disclaimer
The views and opinions expressed herein are those of the author and do not necessarily reflect the views of company.





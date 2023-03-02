# msticpy - M365D registry_key_alerts
M365D - registry_key_alerts - Lists alerts associated with a specified registry key
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
        description: The Registry key name
        type: str     
```
> **GitHub** : msticpy/msticpy/data/queries/m365d/[kql_mdatp_alerts.yaml](https://github.com/microsoft/msticpy/blob/main/msticpy/data/queries/m365d/kql_mdatp_alerts.yaml)

## M365D - registry_key_alerts - Lists alerts associated with a specified registry key
Tracking activity related to a specified registry key is useful for detecting attempts by attackers to disable antivirus.

```
from msticpy.data.data_providers import QueryProvider

md_prov = QueryProvider("M365D")

md_prov.connect()

md_prov.M365D.registry_key_alerts(start=-30, key_name=r"software\\policies\\microsoft\\windows defender")
```
#### **Tip**
As I don't have a background in programming, I wasn't previously familiar with this particular aspect.
> **Mistake :**
> ![image](https://user-images.githubusercontent.com/120234772/222354687-83c0c92b-c639-45c5-afe1-2bf9d5c1bbe5.png)
>
>![image](https://user-images.githubusercontent.com/120234772/222354609-2de8d06a-434f-4e01-a79c-02603edb160d.png)
> **Correct :** <br>
> md_prov.M365D.registry_key_alerts(start=-30, key_name=r"software\\policies\\microsoft\\windows defender")
> ![image](https://user-images.githubusercontent.com/120234772/222354876-f6a41f79-7dc4-48ef-bc42-0575fe9d3ed6.png)
>
> md_prov.M365D.registry_key_alerts(start=-30, key_name="software\\\\\\\\policies\\\\\\\\microsoft\\\\\\\\windows defender")
> ![image](https://user-images.githubusercontent.com/120234772/222355015-a246a65c-7523-4451-8923-dfcb3ffaa2eb.png)


#### demo
![image](https://user-images.githubusercontent.com/120234772/221597336-44698318-9cdb-4f23-92c4-93371c6c2abe.png)

#### Disclaimer
The views and opinions expressed herein are those of the author and do not necessarily reflect the views of company.


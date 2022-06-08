The version of those guide and photo is 8.5.4
# Create a new dashboard
Click `Add(icon) > Create > Dashboard`  
![image](https://user-images.githubusercontent.com/71573064/172528427-88dbaee8-bb58-48b3-b94e-8f22dda91127.png)  
## Create a new panel
Click "Add a new panel"
![image](https://user-images.githubusercontent.com/71573064/172528450-ca6c97a0-5cd0-4712-9481-c836061c097c.png)  
You can set up a new panel in here.  
Right part is the setting of this panel.   
![image](https://user-images.githubusercontent.com/71573064/172528557-5242884a-1ec9-409d-be35-73045a93bd31.png)  
### Select data by query
Input query in the field  
![image](https://user-images.githubusercontent.com/71573064/172529589-d41bd191-f3e9-40bf-b3a5-908ff320cb12.png)  
If the query is vaild, the result graph should be displayed.  

### Change visualization
Change the visualization though clicking the option on the top right![image](https://user-images.githubusercontent.com/71573064/172529383-8e6511ef-15df-41aa-8484-d08e61b0f885.png)

![image](https://user-images.githubusercontent.com/71573064/172529230-9efd2248-c2f3-436e-bb39-5f1f8ab699d2.png)

### field name
In default, fields will be shown completely:  
![image](https://user-images.githubusercontent.com/71573064/172529823-9285fa7c-2240-4029-ba44-b940d7cbca7b.png)  
We can modify the field name in `Standard options > Display name`.  
![image](https://user-images.githubusercontent.com/71573064/172530163-50b1966e-04fd-406e-9596-62edd4cab97e.png)  
And we can extract the name by using variables  
  
Example: Temp {Loc="PBI", Sensor="3"}  
|Expression syntax|Renders to|
|---|---|
|${__field.displayName}|`Temp {Loc="PBI", Sensor="3"}`|
|${__field.name}|`Temp`|
|${__field.labels.Loc}|`PBI`|

More details in https://grafana.com/docs/grafana/next/panels/standard-field-definitions/#display-name
We can use variables to display the field more clearly.  
![image](https://user-images.githubusercontent.com/71573064/172530191-6664eddf-4a28-4630-83fe-9ff17a6c465e.png)

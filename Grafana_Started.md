# Getting started
last guide is `Grafana_Installation.md`
## View the page
After starting server, the default domain is `localhost` HTTP port is 3000.  
You can go to Grafana page though `http://localhost:3000/`  
  
(To view the port number, view the `/etc/grafana/grafana.ini`)  
If you have changed the domain name and port, please go to `http://<domain name>:<changed port>/` 
![image](https://user-images.githubusercontent.com/71573064/172525162-8138a626-f420-4690-a514-34209ba1599a.png)
  
The first page is supposed to be login page  
When you first come in, the default username and password is `admin`.  
![image](https://user-images.githubusercontent.com/71573064/172522030-13b8b032-e56b-4e36-84a2-a9aed36ea598.png)
  
If you log in sucessfully, the page will redirect to main page.  
![image](https://user-images.githubusercontent.com/71573064/172522249-3498c042-1460-4fce-a648-5dbf2d0056ef.png)

## Add the datasource
To connect the data source (such as Prometheus), click `Setting (icon) > Configuration > Data sources`
![image](https://user-images.githubusercontent.com/71573064/172522210-970d92c7-8ed5-460b-b83b-a86a04182718.png)  
click the button "Add Datasource"
![image](https://user-images.githubusercontent.com/71573064/172522444-a62b4781-54e2-4732-a000-fad307cc7854.png)  
Choose the datasource you need  
![image](https://user-images.githubusercontent.com/71573064/172522597-2c95dde1-90fd-4743-b355-f99048fb696a.png)  
Set the datasource config  
Input the url of datasource(mandatory)  
![image](https://user-images.githubusercontent.com/71573064/172522705-6256f1b4-41df-4c7e-896e-6fe55a5717f5.png)  
then click "Save & test"  
  
To test the connect, you can go to `Explore(icon) > Explore`  
and input any query to view the result.  
![image](https://user-images.githubusercontent.com/71573064/172523661-395d6222-6c38-4783-a228-a57fcdb150b8.png)
![image](https://user-images.githubusercontent.com/71573064/172523707-66e3d882-b3ed-4f1a-9cde-93a4c976fc40.png)

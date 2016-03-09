##API Management
---
layout: post

Download PPT [here](https://www.github.com/string-args/MyAlchemyApps/raw/master/AlchemyAPI.pptx).
Visit APIManagement Repository [here](https://github.com/string-args/myAlchemyApps).

### Application Development Tutorial

API Management is the process of publishing, promoting and overseeing APIs in a secure, scalable environment. It also ensures that your API program reaches its fullest potential. 

In this tutorial, you will how to deploy a sample API Management application to Bluemix. In addition, you will learn how to use the services offered by API Management

#### Copy Sample Application

You will download a copy of a sample application that you will deploy in your Bluemix Account.

1. Create the directory `apimanagement` in the root directory. 
2. Download [apimanagement.war](https://github.com/string-args/MyAlchemyApps/raw/master/build/libs/myalchemyapp.war) and save it in the `apimanagement` directory.

#### Deploy Sample Application in Bluemix using the cf tool

1. Open a terminal window and go to the `apimanagement` directory.
2. Login to your Bluemix account using the cf tool. 

		 cf login -a https://api.ng.bluemix.net -s dev  

3. Upload the sample application to your Bluemix account.

		cf push apimanagement-< your_name > -m 256M -p apimanagement.war

4. Go back to the browser tab containing your Bluemix account. In the menu, click `DASHBOARD`.
5. Click the widget of your application to see its overview.

#### Add a API Management Service and Bind it to the Sample Application

1. Click the `ADD A SERVICE OR API` link. You will be redirected to the Catalog page.
2. Look for `API Management` service and click it.
3. In the `Service name` text box, type `apimanage-myservice`.
4. Click the `CREATE` button.
5. When asked to restage your application, click the `RESTAGE` button. Wait for your application to restage.
6. Open another browser tab, and type in the url `apimanagement-< your_name>.mybluemix.net` to see if your application works.



#### Delete the Sample Application and the API Management Service

1. Go back to the browser tab containing your Bluemix account. In the menu, click `DASHBOARD`. 
2. Click the `gear` icon in the widget of the sample application.
3. Click the `Delete App` entry. In the `Services` tab, make sure that the PostgreSQL service is selected. In the `Routes` tab, make sure that the route (i.e., URL) is selected.
4. Click the `DELETE` button.

#### END OF TUTORIAL

	 
	
 

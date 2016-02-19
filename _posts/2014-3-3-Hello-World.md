---
layout: post
title: AlchemyAPI - Feature Extraction and Image Analysis
---
Download PPT [here](https://www.github.com/string-args/MyAlchemyApps).

### Application Development Tutorial

[Alchemy API](http://www.alchemyapi.com/) helps developers and businesses build cognitive applications through text analysis and deep learning.

In this tutorial, you will how to deploy a sample Alchemy API application to Bluemix. In addition, you will learn how to use the services offered by AlchemyAPI i.e. Alchemy Language and Alchemy Vision.

#### Copy Sample Application

You will download a copy of a sample application that you will deploy in your Bluemix Account.

1. Create the directory `myalchemyapp` in the root directory. 
2. Download [MyAlchemyApp.war](https://github.com/string-args/MyAlchemyApps) and save it in the `myalchemyapp` directory.

#### Deploy Sample Application in Bluemix using the cf tool

1. Open a terminal window and go to the `myalchemyapp` directory.
2. Login to your Bluemix account using the cf tool. 

	 > cf login -a https://api.ng.bluemix.net -s dev

3. Upload the sample application to your Bluemix account.

	> cf push myalchemyapp-< your_name > -m 256M -p MyAlchemyApp.war

4. Go back to the browser tab containing your Bluemix account. In the menu, click `DASHBOARD`.
5. Click the widget of your application to see its overview.

#### Add a AlchemyAPI Service and Bind it to the Sample Application

1. Click the `ADD A SERVICE OR API` link. You will be redirected to the Catalog page.
2. Look for `AlchemyAPI` service and click it.
3. In the `Service name` text box, type `alchemyapi-myservice`.
4. Click the `CREATE` button.
	 
	
 

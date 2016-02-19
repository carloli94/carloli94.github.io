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
5. When asked to restage your application, click the `RESTAGE` button. Wait for your application to restage.
6. Open another browser tab, and type in the url `myalchemyapp-< your_name>.mybluemix.net` to see if your application works.

#### Analyze How the AlchemyAPI Service Works

This tutorial will only cover the following functions of Alchemy Language - `Title, Author, Language, Taxonomy, Sentiment` and of Alchemy Vision - `Face Recognition`.

In order for the service to work, `Gradle` is required to solve the dependency management problem of the API. The following line of code is needed in the `build.gradle` file.

	> compile 'com.ibm.watson.developer_cloud:java-wrapper:1.1.0'

If you extract `MyAlchemyApp.war` you will see the subdirectory `src/main/java/Servlet`. This contains several java files including `FServlet.java` and `IServlet.java`.

#### Examine the Java classes

1. `FServlet.java` is the servlet class for Feature Extraction. The following imports are needed for the Alchemy Language function to work:

	> import com.ibm.watson.developer_cloud.alchemy.v1.AlchemyLanguage; 
	>
	> import com.ibm.watson.developer_cloud.alchemy.v1.model.DocumentTitle; 
	>
	> import com.ibm.watson.developer_cloud.alchemy.v1.model.DocumentAuthors; 
	>
	> import com.ibm.watson.developer_cloud.alchemy.v1.model.Language; 
	>
	> import com.ibm.watson.developer_cloud.alchemy.v1.model.Taxonomies; 
	>
	> import com.ibm.watson.developer_cloud.alchemy.v1.model.DocumentSentiment; 


2. `IServlet.java` is the servlet class for Image Analysis. The following imports are needed for the Alchemy Vision function to work:

	> import com.ibm.watson.developer_cloud.alchemy.v1AlchemyVision;
	> 
	> import com.ibm.watson.developer_cloud.alchemy.v1.model.ImageFaces;
	
3. An API key is needed in order for the services of AlchemyAPI to work. This API key is already provided to you when you BIND the service in the sample application. And in this sample application, the api key is already extracted by a method in the `VCAP_SERVICES` as discussed in the previous lab. The following code demonstrates how the API key was used:

	> AlchemyLanguage service = new AlchemyLanguage();
	
	> service.setApiKey(" {api_key} ");
		
	> AlchemyVision service = new AlchemyVision();
	
	> service.setApikey(" {api_key} ");

#### Run the Sample Application

The web application is composed of two tabs: 1 for Feature Extraction and 1 for Image Analysis. It accepts URL input.

1. In the Feature Extraction tab, copy and paste the url provided below and click `Extract`:

 > http://blog.programmableweb.com/2011/09/16/new-api-billionaire-text-extractor-alchemy/

2. The output will be shown in the screen for few second. The output will be in JSON format:



	 
	
 

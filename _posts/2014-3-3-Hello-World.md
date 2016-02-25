---
layout: post
title: AlchemyAPI - Feature Extraction and Image Analysis
---
Download PPT [here](https://www.github.com/string-args/MyAlchemyApps/raw/master/AlchemyAPI.pptx).

Visit AlchemyApp Repository [here](https://github.com/string-args/myAlchemyApps).

### Application Development Tutorial

[Alchemy API](http://www.alchemyapi.com/) helps developers and businesses build cognitive applications through text analysis and deep learning.

In this tutorial, you will how to deploy a sample Alchemy API application to Bluemix. In addition, you will learn how to use the services offered by AlchemyAPI i.e. Alchemy Language and Alchemy Vision.

#### Copy Sample Application

You will download a copy of a sample application that you will deploy in your Bluemix Account.

1. Create the directory `myalchemyapp` in the root directory. 
2. Download [MyAlchemyApp.war](https://github.com/string-args/MyAlchemyApps/raw/master/build/libs/myalchemyapp.war) and save it in the `myalchemyapp` directory.

#### Deploy Sample Application in Bluemix using the cf tool

1. Open a terminal window and go to the `myalchemyapp` directory.
2. Login to your Bluemix account using the cf tool. 

		 cf login -a https://api.ng.bluemix.net -s dev  

3. Upload the sample application to your Bluemix account.

 			
		cf push myalchemyapp-< your_name > -m 256M -p MyAlchemyApp.war

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

If you extract `MyAlchemyApp.war` you will see the subdirectory `src/main/java/Servlet`. This contains several java files including `FServlet.java` and `IServlet.java`.

#### Examine the Java classes

1. `FServlet.java` is the servlet class for Feature Extraction. Take note of the following ENDPOINT URLs, these ENDPOINTS URLs are used along with the input_url and the apikey to be able to get the output of the function.

         
         Taxonomy: "http://gateway-a.watsonplatform.net/calls/url/URLGetRankedTaxonomy"
         Language: "http://access.alchemyapi.com/calls/url/URLGetLanguage"
         Authors: "http://gateway-a.watsonplatform.net/calls/url/URLGetAuthors"
         Sentiment: "http://gateway-a.watsonplatform.net/calls/url/URLGetTextSentiment"
         Title: "http://gateway-a.watsonplatform.net/calls/url/URLGetTitle"
         

2. `IServlet.java` is the servlet class for Image Analysis. Take note of the following ENDPOINT URLs, these ENDPOINTS URLs are used along with the input_url and the apikey to be able to get the output of the function.

		
		Face Recognition: "http://gateway-a.watsonplatform.net/calls/url/URLGetRankedImageFaceTags"		
		 
	
	   
3. An API key is needed in order for the services of AlchemyAPI to work. This API key is already provided to you when you BIND the service in the sample application and is extracted from the `VCAP_SERVICES`. 

          
           AlchemyConnector connector = new AlchemyConnector();
           connector.getAPIKey();
           

#### Run the Sample Application

The web application is composed of two tabs: 1 for Feature Extraction and 1 for Image Analysis. It accepts URL input.

1. In the Feature Extraction tab, copy and paste the url provided below and click `Extract`:

		 http://thelasallian.com/2016/02/13/uaap-lady-spikers-rout-adamson-in-straight-sets/

2. The output will be shown in the screen for few second. The output will be in JSON format:
	
		Title:
			 {"url": "http://thelasallian.com/2016/02/13/uaap-lady-spikers-rout-adamson-in-straight-sets/", "title": 
			 "UAAP: Lady Spikers rout Adamson in straight sets"}
		Author:
			 {"url": "http://thelasallian.com/2016/02/13/uaap-lady-spikers-rout-adamson-in-straight-sets/", "author":
			 "Tinsel Joaquin"}
		Language:
			{"language": "english", "iso-639-1": "en", "iso-639-2": "eng", "iso-639-3": "eng", "ethnologue":
			"http://www.ethnologue.com/show_language.asp?code=eng", "native-speakers": "309-400 million", "wikipedia": 
			"http://en.wikipedia.org/wiki/English_language"}
		Taxonomy:
			{"taxonomy": [ { "label": "/religion and spirituality/christianity", "score": "0.502526" }, { "confident":
			"no", "label": "/sports/bobsled", "score": "0.393774" }, { "confident": "no", "label": "/health and
			fitness/disorders/mental disorder/panic and anxiety", "score": "0.388495" } ]}
		Sentiment:
			{"docSentiment": { "mixed": "1", "score": "-0.329049", "type": "negative" }}
		
3. The output is only possible because of the functions in `FServlet.java`. Remember the ENDPOINT URLs of the functions above. They are used to generate the output of each function in JSON Format: 

		Title:
		URL title_url = new URL(TITLE_ENDPOINT_URL+"?url="+input_url+"&apikey="+connector.getAPIKey()+"&outputMode=json");
		reader = new BufferedReader(new InputStreamReader(title_url.openStream()));
		while ((line = reader.readLine()) != null){
			sb.append(line);
		}
		
		*The above code takes the ENDPOINT URL of the Title function added with the url inputted by the user, 
		the api key provided and the specifying that the output mode is in JSON Format. The output of the function 
		is then read through line by line in the BufferedReader and appended to String Builder sb to produce the output.
		
		Author:
		URL author_url = new URL(AUTHOR_ENDPOINT_URL+"?url="+input_url+"&apikey="+connector.getAPIKey()+"&outputMode=json");
		reader = new BufferedReader(new InputStreamReader(author_url.openStream()));
		while ((line = reader.readLine()) != null){
			sb.append(line);
		}
		
		Language:
		URL language_url = new			
		URL(LANGUAGE_ENDPOINT_URL+"?url="+input_url+"&apikey="+connector.getAPIKey()+"&outputMode=json");
		reader = new BufferedReader(new InputStreamReader(language_url.openStream()));
		while ((line = reader.readLine()) != null){
			sb.append(line);
		}
		
		Taxonomy:
		URL taxonomy_url = new
		URL(TAXONOMY_ENDPOINT_URL+"?url="+input_url+"&apikey="+connector.getAPIKey()+"&outputMode=json");
		BufferedReader reader = new BufferedReader(new InputStreamReader(taxonomy_url.openStream()));
		while ((line = reader.readLine()) != null){
			sb.append(line);
		}
		
		Sentiment:
		URL sentiment_url = new
		URL(SENTIMENT_ENDPOINT_URL+"?url="+input_url+"&apikey="+connector.getAPIKey()+"&outputMode=json");
		reader = new BufferedReader(new InputStreamReader(sentiment_url.openStream()));
		while ((line = reader.readLine()) != null){
			sb.append(line);
		}
	
	
4. In the Image Analysis Tab, Copy and Paste the url below and click Extract:

			http://s2.stabroeknews.com/images/2014/08/brad.jpg

5. The output will be shown in the screen for few second. The output will be in JSON format:

			Face Recognition:
				{"imageFaces": [ { "age": { "ageRange": "35-44", "score": "0.492583" }, "gender": { "gender":
				"FEMALE", "score": "0.995504" }, "height": "428", "positionX": "518", "positionY": "274", "width":
				"428" }, { "age": { "ageRange": "35-44", "score": "0.52164" }, "gender": { "gender": "MALE", "score":
				"0.990048" }, "height": "386", "identity": { "disambiguated": { "dbpedia":
				"http://dbpedia.org/resource/Brad_Pitt", "freebase": 
				"http://rdf.freebase.com/ns/m.0c6qh", "musicBrainz":
				"http://zitgist.com/music/artist/eaeceae0-98f7-4630-b8a0-df5083db4c9a", "name": "Brad Pitt",
				"opencyc": "http://sw.opencyc.org/concept/Mx4rvchm5pwpEbGdrcN5Y29ycA", "subType": [ "Person", "Actor",
				"MusicalArtist", "AwardNominee", "AwardWinner", "Celebrity", "FilmActor", "FilmProducer", "TVActor" ],
				"yago": "http://yago-knowledge.org/resource/Brad_Pitt" }, "name": "Brad Pitt", "score": "0.956893" },
				"positionX": "257", "positionY": "164", "width": "386" } ]}

6. The output is only possible because of the functions in `IServlet.java`. Remember the ENDPOINT URLs of the functions above. They are used to generate the output of each function in JSON Format: 

			Face Recognition:
					URL face_url = new
					URL(FACE_ENDPOINT_URL+"?url="+input_url+"&apikey="+connector.getAPIKey()+"&outputMode=json");
					BufferedReader reader = new BufferedReader(new InputStreamReader(face_url.openStream()));
					while ((line = reader.readLine()) != null){
						sb.append(line);
					}
					

8. The Face Recognition function generates the gender, the approximate age, and the name (if celebrity is detected) of the person detected in the image.

9. You are now free to enter an image link or a document link. 

#### Delete the Sample Application and the Alchemy API Service

1. Go back to the browser tab containing your Bluemix account. In the menu, click `DASHBOARD`. 
2. Click the `gear` icon in the widget of the sample application.
3. Click the `Delete App` entry. In the `Services` tab, make sure that the PostgreSQL service is selected. In the `Routes` tab, make sure that the route (i.e., URL) is selected.
4. Click the `DELETE` button.

#### END OF TUTORIAL

	 
	
 

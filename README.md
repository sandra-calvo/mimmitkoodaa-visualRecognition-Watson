

# IBM Cloud :cloud: & Watson 
# Visual Recognition: Mimmitkoodaa workshop

<!--- GIF & images
![Alt Text](https://media.giphy.com/media/vFKqnCdLPNOKc/giphy.gif)
--->
 
## Introduction 
In this guide, we will create our own custom classifier and a Node-RED application using Watson visual recognition on IBM Cloud. 

#### Prerequisites
- Register on IBM Cloud at https://bluemix.net

# PART 1: Create a custom classifier

## Step 0. Explore: Visual Recognition Service
The IBM Watson™ Visual Recognition service uses deep learning algorithms to analyze images (.jpg, or .png) for scenes, objects, faces, and other content, and return keywords that provide information about that content. You can also create custom collections of your own images, and then upload an image to search the collection for similar images. 

![](/screenshots/Picture0.png?raw=true)

#### Use Cases 

| Industry | Use case example|
| ------------- |-------------|
| Manufacturing | Use images from a manufacturing setting to make sure products are being positioned correctly on an assembly line.|
| Visual Auditing| Look for visual compliance or deterioration, train custom classifiers to understand what defects look like.|
|Insurance | Rapidly process claims by using images to classify claims into categories.|
| Social Listening | Use images from your product line or your logo to track buzz about your company on social media. |
| Social Commerce | Use an image of a plated dish to find out which restaurant serves it and find reviews.| 
| Retail | Take a photo of your favorite outfit to find stores with those clothes in stock. |
| Education| Create image-based applications to educate about taxonomies, use pictures to find educational material or similar subjects.|

#### Demo
To see the Visual Recognition service in action, see the Visual Recognition demo app. With the demo, you can analyze images for subject matter, and faces, as well as train a temporal custom classifier.

https://visual-recognition-demo.ng.bluemix.net/ 

#### Explore the API (First go through the lab at least once) 
Interact with the Watson API to understand how it works. Use the explorer to test your calls to the API, and to view live responses from the server.   
http://www.ibm.com/watson/developercloud/visual-recognition/api/v3/#apiexplorer 
OR
https://watson-api-explorer.mybluemix.net/apis/visual-recognition-v3#/ 

You can authenticate to the Visual Recognition API by providing the API key that is provided in the service credentials for the service instance that you want to use. After you create an instance of the Visual Recognition service, you can view the API key by selecting Service Credentials from the left pane of the service dashboard. 
You can do the training through the API explorer or using CURL if you prefer. 

#### Documentation 
Find the complete documentation on the Visual Recognition service here: http://www.ibm.com/watson/developercloud/doc/visual-recognition/ 

#### Other Watson services
Check other Watson services: http://www.ibm.com/watson/developercloud/doc/ 

Explore the APIs: https://watson-api-explorer.mybluemix.net/ 
 
 
## Step 1. Create your Visual Recognition service
1.	Click "Catalog" in the upper right corner and then find the Visual Recognition service at the bottom of the catalog under Watson category - (scroll down might be needed). 
Click on it to add it to your dashboard. 

![](/screenshots/Picture1.png?raw=true)
 
2.	Select the region and space where you want to deploy the service and click on 'Create'. The IBM Cloud Lite account only allows to create one visual recognition service per account, so if you already have a service in use go to Step 2.

![](/screenshots/Picture2.png?raw=true)
 
3.	After few seconds you will have your service ready to be used. 

## Step 2. Create and train your classifier
Once you have created the Visual recognition service it's time to start creating a new classifier. By default, the Visual recognition service will be able to detect all kind of objects, forms, colors and things in the images. The same way the demo application in Step 0 was able to detect. However, in this lab we will create our own classifier. 

A classifier can be premade or self-created and uses algorithms to classify a picture as an input. Before we enter the Visual Recognition tool we will need to generate an API key. Click on "Service credentials" on the left side menu. 

![](/screenshots/Picture3.png?raw=true)

Click on the "New Credential" button to generate an API key. 

![](/screenshots/Picture4.png?raw=true)
 
A window will be prompted, simply click on "Add". 

![](/screenshots/Picture5.png?raw=true)
 
Now that you have your credentials ready, copy the API key and save it in a notebook in your computer if you want, or keep the tab open. We will need that later in the lab. 

![](/screenshots/Picture6.png?raw=true)
 
Now let's access the Visual Recognition Tool by entering the following URL in a new tab:
 
 https://watson-visual-recognition.ng.bluemix.net/

Click on API Key and enter the credentials you copied in the previous stage.

![](/screenshots/Picture7.png?raw=true)
 
You will see 3 classifiers ready. This is the default Visual recognition set up, so in addition to the general classifier it is able to recognize food and faces. 

Let's create our own classifier by clicking in "Create Classifier".
 
 ![](/screenshots/Picture8.png?raw=true)
 
Once that's done download the training data located in the "training material" folder. Download the .zip files. As you can see we are going to train Watson to recognize Angry Birds characters. 

Name your classifier for example "AngryBirds" and create three classes named "Red", "Blue" and "Yellow". For the negative class you can use the Pigs.zip file.

Drag and drop the .zip files into their correct classes. Once that's done press "Create" as shown in the next picture. 

 ![](/screenshots/Picture9.png?raw=true)
 
The training process can take few minutes.

 ![](/screenshots/Picture10.png?raw=true)

 
#### Congrats! You've now created your own customized classifier in the Watson Visual Recognition service. 

Now drag and drop images to test how the classifier works. 

 ![](/screenshots/Picture10b.png?raw=true) 

# PART 2: Create a Node-RED app using Visual Recognition

## Step 3. Create Your Node-RED Application

#### About Node-RED
Node-RED is a visual tool for wiring the internet of things - connecting hardware devices, APIs and online services in a new and interesting way. Node-RED provides a browser-based flow editor that makes it easy to wire together flows using the wide range nodes in the palette. Flows can be then deployed to the runtime in a single-click.
- JavaScript functions can be created within the editor using a rich text editor.
- A built-in library allows you to save useful functions, templates or flows for re-use.
- See https://nodered.org for more information. 


If you already have a Node-RED application and a Visual Recognition service in use in Bluemix, you can use those - In that case jump to Step 4.

4.	In a browser navigate to https://bluemix.net
5.	Select 'LOG IN' then enter your log in information and press 'SIGN IN'.  
6.	Select the 'CATALOG' view.
7.	Locate the NODE-RED Starter in the boilerplate section of the catalog and click on it.  
 
 ![](/screenshots/Picture11.png?raw=true)

8.	Enter a name for your application, as shown below (host will automatically be completed).  The host name must be unique on IBM Cloud, so please choose a name for example using your initials. Press 'CREATE'. 

 ![](/screenshots/Picture12.png?raw=true)
 
9.	Your application is now staging and will be up and running/awake in a short while. Press 'OVERVIEW' to see information about your application. 

10.	When fully staged, click on the View app link, next to the green circle, this launches the Node-RED main page in a new tab.

 ![](/screenshots/Picture13.png?raw=true)
 
11.	Configure your Node-RED editor. In this section, you will set up a username and password to protect your flow. 

 ![](/screenshots/Picture14.png?raw=true)

12.	Write an username and a password of your choice and click 'Next'. Remember that it does not have to be related to your IBM Cloud access. 

 ![](/screenshots/Picture15.png?raw=true)
 
Node-RED is an open source project so you can add new nodes to the palette by modifying the package.json file. 

  ![](/screenshots/Picture16.png?raw=true)
  
  ![](/screenshots/Picture17.png?raw=true)
 
*Your Node-RED flow is all set!

Now click Go to your Node-RED flow editor to open the flow editor and enter your credentials to access the editor.

  ![](/screenshots/Picture18.png?raw=true)
  
  ![](/screenshots/Picture19.png?raw=true)

13.	When using Node-RED we build our apps using this graphical editor interface to wire together the blocks we need. We can simply drag and drop the blocks from the left menu into the workspace in the center of the screen and connect them to create a new flow. 

Note: If you get an "Authorization denied" message when deploying your applications make your sure you are logged in. Click on the icon on the top right side of the Node-RED canvas and login with the credentials you created in the previous steps. 

 ![](/screenshots/Picture20.png?raw=true)

## Step 4. Build your Node-RED flow to classify images
This is the flow we are going to build in this step to test the visual recognition capabilities:

![](/screenshots/Picture21b.png?raw=true)
 
Locate the inject node under the input section in the palette window.  
The inject node is simply a node to send a message (string, timestamp etc) through your flow.

1.	Drag the node onto the workspace in the middle of the screen. Double click on the inject node to configure the node. Change the payload to be a string, and add a direct link to an image you would like to analyze. 
For example: https://www.thesun.co.uk/wp-content/uploads/2017/06/nintchdbpict0002407806071.jpg?strip=all&w=960 

![](/screenshots/Picture22.png?raw=true)
 
2.	Next, we add the Visual recognition node, under the Watson section in the palette.   

3.	Drag the node onto the workspace. Connect the Visual recognition node with the inject node by dragging the output and input dots together and double click in the visual recognition node to configure the setting.
This node will analyze the image sent by the inject node.  

![](/screenshots/Picture23.png?raw=true)
 
Configure the node like the above image with your own API key.

4.	Add a function node for parse the output of the visual recognition.   
Double click on the function node and add the following code: (Be aware, that sometimes there can be format problems when copying the code.)

``` javascript
msg.payload="Watson says that is a/an: \n ";
    for (var i=0; i < msg.result.images[0].classifiers[0].classes.length; i++) {
    msg.payload += msg.result.images[0].classifiers[0].classes[i].class + " with a score of " + msg.result.images[0].classifiers[0].classes[i].score + "\n";
    }
    return msg;
```

5.	To see the results of the image analysis in the debug tab add a debug node. This node doesn't need any configuring. 

6.	The flow is now complete. Make sure that all nodes are connected then click 'Deploy' in the top right corner on the screen.  
 
Click the button to the right of the inject node. To see the results of the analysis, take a look at the debug tab. 

![](/screenshots/Picture25.png?raw=true)
 
In order to make the lab easier we are going to import the rest of the code. 

You can get the complete Node-RED flow from the **mimmitkoodaa_visualRecognition_flow.txt**.

Import the flow by simply clickcing on the 3 white lines on the top right corner of the Node-RED window.  Import - Clipboard - and paste the text you copied from above. 

![](/screenshots/Picture26.png?raw=true)

![](/screenshots/Picture27.png?raw=true)
 
This will create the missing part shown in the first picture of this section. You will need to do some editing on few nodes, because credentials are not transferred with the rest of the code. 

Edit the Visual Recognition nodes with your own credentials (API Key). 

Now feel free to find you own images and add them to the different inject nodes to classify images.
 
## Step 5. Test your customized classifier
Same way you imported the code in the previous step, copy the following text and import it in Node-RED. In this case use **mimmitkoodaa_customClassifier_flow.txt**

We should have the next flow:
 
 ![](/screenshots/Picture28.png?raw=true)
 
This flow takes a picture and runs it through the custom classifier created in Step 2. If it finds a match it will tell us what Watson sees in the picture, if it can't find a match it will print a message saying that. 

Remember you will need to edit the credentials in the Visual Recognition node and write your own ID in the function "Define the classifier ID".

Your classifier ID can be found in the Visual Recognition Tool: (Do not use the ID shown in the picture)

![](/screenshots/Picture29.png?raw=true)
 
Edit the blue timestamp/inject node with the image URL you want to run through the classifier. 


## Step 6. Create your webapp (UI)
First we will add some new nodes to our palette. 

In the Node-RED window click on the three lines on the top right corner and in the menu, click on the "Manage palette". This will open the node menu where you can add new nodes to your application. You will see the nodes that are installed by default and if you go to the 'install' tab you can search for any node package and add it directly to your app.
                  

Search for the dashboard nodes by writing 'dashboard'. This will return multiple node packages, you need to install the package 'node-red-dashboard'. Find it in the search results and click on install. 

This will prompt a window to confirm the installation. Click on install and wait few minutes, the application may require a restart. Click "Done" to close the left side menu. 

After few minutes you will see the new nodes in your Node-RED palette. 

Same way you imported the code in the previous steps, copy the following text and import it in Node-RED. In this case use **mimmitkoodaa_UI.txt**

We added the UI flow:

 ![](/screenshots/Picture30.png?raw=true)
 
 You will need to add to the visual recognition nodes your own API Key. 
 
 And also your own classifier ID to the node named custom. 
 
 ## Step 7. Check your webapp! 
The dashboard nodes added an UI to our Node-RED application. To access the UI go to:

http://yourAppName.mybluemix.net/ui - US South

Remember that if you are in UK, Germany Sydney the addredd will look slightly different:
http://yourAppName.eu-gb.mybluemix.net/ui - UK

http://yourAppName.eu-de.mybluemix.net/ui - Germany

http://yourAppName.au-syd.mybluemix.net/ui - Sydney

Awesome, you web app is ready! :+1:

Play with the visual recognition classifier using the UI.
Enter the image URL and choose default classifier or custom and check the results!

 ![](/screenshots/Picture31.png?raw=true)
 
 # Summary
 In this lab you created a custom classifier using Watson Visual Recognition API and exposed your custom classifier through a web app using Node-RED. 


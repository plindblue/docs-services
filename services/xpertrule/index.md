{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Getting started with Xpertrule for Bluemix
{: #gettingstarted} 
*Last updated: 21 Sep 2016*

XpertRule Decision Author for Node-RED is a tool for developers to rapidly add complex decision and analytics automation to node-RED flows. XpertRule Decision Author is ideal in manufacturing, utilities, aerospace, and automotive sectors, and anywhere that requires automation of complex decisions, calculations, diagnosis, or root-cause analysis. It's simple to deploy as a Node-RED node and execute wherever node-RED red can be run: edge or cloud.
{:shortdesc}

## Publishing knowledge in Decision Author
1. Log in to XpertRule Decision Author by using your email and password: [http://ibmxrkb.xpertrule.com/](http://ibmxrkb.xpertrule.com)
{:new_window}

	The launch page contains a default knowledge base called ‘Bluemix Sample’. For details about how to author this knowledge base, see the following web site:  [http://ibmxrkb.xpertrule.com/editor/help/transactional_getting_started_1.html](http://ibmxrkb.xpertrule.com/editor/help/transactional_getting_started_1.html)
{:new_window}

	For now we will concentrate on publishing the sample knowledge base for use in a Node-RED app.

2. Open the ‘Bluemix Sample’ by double clicking.

	1. Locate the menu and click Publish.

	2. Select Publish the current Knowledge Base.  

A URL appears. Copy the URL for later use in Node-RED.

## Publishing a knowledge base into a Bluemix Node-RED app
1. Log in to the new Bluemix site using your relevant email and password. (If you log in to the current Bluemix site, select ‘Try the new Bluemix’ from the header.)

	1. Select Catalog from the menu bar.
	
	2. Under the category ‘Boiler Plates’, select ‘Node-RED Starter’.
	
	3. Provide an App name (avoid using spaces) and Host, and select your relevant plan.
	
	4. Click Create.

2.  Scroll down and click Download Starter Code.  

	After the starter code is downloaded, unpackage and copy the folder to a location of your choice.

3. Open a new command prompt.

	Change the directory to where you placed the Node-RED starter code. 
  ```
	cd directory_name
  ```
  {: codeblock}

4. Next, install the xrcall Node-RED node, which will be used for running the knowledge base published earlier.

	- This step requires you to have npm installed. If you don’t already have it installed, we recommend downloading Node.js from nodejs.org, which includes npm.

	- Return to your command prompt and run the following command:
  ```
	npm install node-red-contrib-xrcall
  ```
  {: codeblock}

	If you have installed the xrcall node correctly, you will find it in the ‘node modules folder’.

5. Push the ‘Starter Code’ along with the new xrcall node back to Bluemix.

	1. Start by downloading and installing the cf Command Line Interface.
	```	
	https://github.com/cloudfoundry/cli/releases
	```
  {: codeblock}
  
	2. Return to your command prompt and connect to IBM Bluemix by entering the following command:
	```
	cf api https://api.ng.bluemix.net
	```
  {: codeblock}
  
	3. From your command prompt, log in to Bluemix by entering the following command:
	```
	cf login
	```
  {: codeblock}
  
	4. Enter your relevant Bluemix email address and password.

	5. Upload the app to Bluemix by using the following command:
	```
	cf push (insert the name of your newly created Bluemix app)
	```
  {: codeblock}
  
	This might take a few minutes.

6. Access your updated Node-RED by returning to the Bluemix site and selecting Cloud Foundry Applications.

	1. Locate the relevant app and click the associated URL.  A new window called Node-RED opens in Bluemix.
	
	2. Locate and click ‘Go to your Node-RED flow editor’.

	3. Within the newly opened editor, locate the menu and select Import > Clipboard.

	4. Paste the following flow into the newly opened window:
	```
	[{"id":"db2e43f6.4c3d1","type":"xrcall","z":"66f711b2.8ba8b","name":"XpertRule Knowledge","host":"ibmxrkb.xpertrule.com","port":"8125","path":"Super_Admin_All_Users_Bluemix_App","x":440,"y":90,"wires":[["39b3c085.676da"]]},{"id":"90f107ec.c83858","type":"inject","z":"66f711b2.8ba8b","name":"Manual Trigger","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"x":118,"y":90,"wires":[["b86b43cf.cce65"]]},{"id":"39b3c085.676da","type":"debug","z":"66f711b2.8ba8b","name":"","active":true,"console":"false","complete":"true","x":615,"y":91,"wires":[]},{"id":"b86b43cf.cce65","type":"function","z":"66f711b2.8ba8b","name":"Inputs","func":"msg.Cost = 0;\nmsg.Department = \"Sales\";\nmsg.Grade = \"Director\";\nmsg.In_London = false;\n\nreturn msg;","outputs":1,"noerr":0,"x":268,"y":90,"wires":[["db2e43f6.4c3d1"]]}]
	```
  {: codeblock}
  
	5. Click Import and place your newly created flow onto the open editor.

7. Double-click the xrcall node.

	1. Access the published URL you created earlier in XpertRule Webauthor. Use it to complete the relevant fields as per the following example:
	```
	Host: ibxrkb.xpertrule.com
	Port: 8125
	Path: User_Bluemix_App
	```
  {: codeblock}
  
	2. Click Done.

8. Test the knowledge base by clicking Deploy and performing a manual trigger. The output is displayed in the debug window.

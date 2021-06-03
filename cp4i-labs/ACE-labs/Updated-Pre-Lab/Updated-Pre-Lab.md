# Generating credentials for Designer connectors on CP4i


## Salesforce Connector

To get started you will require admin level access to your Salesforce account. If you want to create a free Salesforce account to test, make sure that you create a Developer account rather than a Trial account. If you connect to App Connect with a Trial account, the Salesforce events do not work.

![alt text][pic0]

To get your login URL, click on your user profile. The URL text below your Account Name is your login URL.

![alt text][pic1]

Once logged into your Salesforce account, on the left-hand Finder panel go to: PLATFORM TOOLS > Apps > App Manager

![alt text][pic2]

You then want to create a New Connected App or use an existing one. Steps for creating a new app are as follows:
![alt text][pic3]

Provide Connect App Name and API Name is automatically generated for you. Provide Contact Email usually admin email address.
Please make sure you Enable OAuth Settings and follow steps below to configure OAuth setting.


![alt text][pic4]

Click on Enable OAuth Settings to get the configuration panel.
Either click on Enable for Device Flow and that will auto-generate Callback URL or alternately you can provide your own fully qualified Callback URL.

Next step is to configure scope of access for our connectors which will be the Connected App in this case. Connectors technically only require data api, you can optionally choose to enable all the scopes for this connected app.

And then Click on Save.

![alt text][pic5]

It may take several minutes for newly created Connected App to be registered. Once registered go back to App Manager, select and view the created App
![alt text][pic6]

Use Consumer Key and Secret as Client ID and Client Secret as needed in the connector template. Next we will need to retrieve Security Token. For this click on your user profile and select Settings option in the profile panel.

![alt text][pic7]

Under Settings find and click Reset Security Token option
![alt text][pic8]

Click on Reset Security Token Button and it will send the newly generated security token to your admin email address. Use the token for your credentials.

---
## Service Now Connector


Pre-requisite: Download and Install [Postman](https://www.postman.com/) app

To get started you will require admin level access to your ServiceNow account. If you want to create a free ServiceNow account to test out App Connect, you’ll have to register for a ServiceNow Account for the Developer Site. Once your account is activated, you can request a ServiceNow personal developer instance.

![alt text][pic9]

Search for Registry in Filter navigator search bar and then select Application Registry

![alt text][pic10]

Click "New" and create an OAuth API endpoint for external clients
![alt text][pic11]

![alt text][pic12]

In the config panel give it a unique name and hit submit
![alt text][pic13]

This will create a new OAuth endpoint with Client ID and Client Secret generated. You can view these details by clicking and viewing the new endpoint.

Save Client ID and Secret for future use.

Inside your Oauth endpoint we now need to make few updates to make it work with Postman so that we can generate access tokens.

Insert Postman url: https://www.getpostman.com/oauth2/callback in Redirect URL field.

Also, increase Access Token Lifespan to same as Refresh Token Lifespan.

![alt text][pic14]

Click on Update button to save the changes. Now, open Postman app on your machine.
![alt text][pic15]

Create a new Collection with a new API request. Go to the collections tab and click **Create Collection**

![alt text][pic16]

Click on the drop-down arrow next to new collection. 

![alt text][pic17]

Then click **Add a Request**

![alt text][pic18]

Select HTTP request method as GET and use HTTP URL as below: https://&lt;your URL&gt;/api/now/table/incident. YourURL can be found when you are signed into your ServiceNow developer account. Typically this URL will be in the following format: https://devXXXXX/service-now.com

![alt text][pic19]

![alt text][pic20]


Now click on Authorization to config auth parameters. Set Auth type to OAuth 2.0

![alt text][pic21]

Configure GET NEW ACCESS TOKEN panel with following details:
* **Token Name** – any unique name
* **Grant Type** – Authorization Code
* **Callabck URL** – https://www.getpostman.com/oauth2/callback (same as the one you inserted in OAuth endpoint in ServiceNow)
* **Auth URL** - https://<your ServiceNow URL>/oauth_auth.do
* **Access Token URL** - https://<your ServiceNow URL>/ oauth_token.do 
* **Client ID** – As generated in above steps
* **Client Secret** – As generated in above steps
* **Scope** – useraccount
* **State** – 1
* **Client Authentication** – Send as Basic Auth header

![alt text][pic22]

Click on **Get New Access Token** and it will kick start OAuth web dance. You will require your admin username/password to authenticate yourself with web dance. Note: this log in is different from your developer user and password

![alt text][pic23]


![alt text][pic24]


Once through click on Allow and it will give you Access Token and Refresh Tokens generated for you. Store them for future use.


![alt text][pic25]



[pic0]: images/0.png
[pic1]: images/1.png
[pic2]: images/2.png
[pic3]: images/3.png
[pic4]: images/4.png
[pic5]: images/5.png
[pic6]: images/6.png
[pic7]: images/7.png
[pic8]: images/8.png
[pic9]: images/9.png
[pic10]: images/10.png
[pic11]: images/11.png
[pic12]: images/12.png
[pic13]: images/13.png
[pic14]: images/14.png
[pic15]: images/15.png
[pic16]: images/16.png
[pic17]: images/17.png
[pic18]: images/18.png
[pic19]: images/19.png
[pic20]: images/20.png
[pic21]: images/21.png
[pic22]: images/22.png
[pic23]: images/23.png
[pic24]: images/24.png
[pic25]: images/25.png

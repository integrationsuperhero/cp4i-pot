# IBM App Connect Enterprise

## App Connect Designer ServiceNow

[Return to main lab page](../index.md)

---

# Table of Contents 
- [1. Introduction](#introduction)
  * [Pre-Lab: Gathering your ServiceNow Credentials](#pre_lab)
- [2. Create a Designer Flow in CP4I to Call ServiceNow](#create_a_designer_flow_in_cp4i_to_call_servicenow)
  * [2a Testing the API flow](#testing_the_API_flow)
  * [2b Add an Additional Operation for our ServiceNow API](#add_an_additional_operation_for_our_servicenow_API)
  * [2c Testing the New API Operation](#testing_the_new_API)
- [3. Deploying Your Designer Flow to App Connect Dashboard](#deploying_your_designer_flow_to_app_connect_dashboard)
    
---

# 1. Introduction <a name="introduction"></a>
The purpose of this LAB is to show how to retrieve ServiceNow Records using IBM App Connect Designer on IBM Cloud Pak for Integration.
When prompted to log in to CP4I  use the username and password provided to you for this lab.   

**Pre-Lab: Gathering your ServiceNow Credentials**
For this lab, you will need to collect your Salesforce account details: Username, Password, Client Secret, and Client ID. You can learn how to obtain these values from this link: https://developer.ibm.com/integration/docs/app-connect/how-to-guides-for-apps/use-ibm-app-connect-salesforce/ 

# 2. Create a Designer Flow in CP4I to Call ServiceNow  <a name="create_a_designer_flow_in_cp4i_to_call_servicenow"></a>

In this section we use App Connect Designer to create a flow that will be exposed as an API to connect and call Salesforce records.

1\. Select the Enterprise LDAP:

![alt text][pic0]

2\. When prompted use the username and password provided to you for this lab. In this example we are using wedge10.

![alt text][pic1]

3\. Click on the App Connect Designer link to take you to the designer dashboard.

![alt text][pic2]

4\. Select the tab on the left to open the Catalog screen.

![alt text][pic3]

5\. Now scroll down to the ServiceNow connector and click on the Connect button


6\. Fill in the ServiceNow connection info that you have from the pre-lab section at the beginning of this lab

![alt text][pic4]

7\. You will see the events and actions availble with this connector. Also you can change the Account Name to something more meaningful to you by clicking on the 3 dots next to the Account name.

![alt text][pic5]

8\. Click on the App Connect Designer dashboard icon:
![alt text][pic6]

9\. Select from the New drop down to create a new API flow:  

![alt text][pic7]

10\. First thing we will do is create the model for this.  We will call the model **ServiceNowRetrieve.**  Also in the upper left we will change the Name from Untitled to **ServiceNowRetrieve.**  Click **Create model**

![alt text][pic8]

11\. We will map the following properties which are all data type String. You can also set the data type to Number for properties containing numerical integer values. 

1.	SystemUserID
2.	FirstName
3.	LastName
4.	Email

![alt text][pic9]

Now that we have defined the properties in our API model definition, we can implement a flow by clicking on the Operations tab.

12\. From the Operations drop-down menu, select Add a Custom Operation. Here we will customize the operation that we want our API to perform.

![alt text][pic10]

13\. Customize the details of your API operation. 
**Note:** *You can optionally set a description for your individual API operation.*

Display Name: **Retrieve Accounts**

HTTP Verb: **GET** 

Operation Name: **user**

**Note:** *The operation name will be a part of your API Endpoint URL and is therefore consumer-facing.*

Response body: **ServiceNowRetrieve**

![alt text][pic11]

14\. After customizing your API operation, the details should match the image below.

![alt text][pic12]

Now we can click the Implement Flow button next to our API operation definition. This will take us to the App Connect Designer flow.

15\. This is where we can insert Smart Connectors to communicate with a variety of external applications as well as implement conditional logic and callable flows. 

![alt text][pic13]

16\. After clicking the blue plus icon on our flow designer interface, we will be able to see the variety of Smart Connectors offered by IBM App Connect Designer. 
Scroll down to the ServiceNow connector 
For our lab, we will be using the ServiceNow smart connector, so let us scroll down to the ServiceNow connector and select it.


17\. You will see a vast catalog of different ServiceNow objects you can interact with from App Connect Designer.  For this lab we will be retrieveing the system users so select System users and you will see varies actions.  Select the **Retrieve system users**

![alt text][pic14]

18\. The next interface that populates under our Designer flow allows us to add conditionals to our integration flow. For example, if we want to retrieve all account records for a particular account, we can specify this condition by setting the AccountName key to the respective account.

In our example, we will retrieve the first 4 ServiceNow system users records. In order to do this, we can set the Maximum number of items to retrieve field to 4.  And then select, Process 4 item from the collection in the radio button options. As you can see there is also some error handling options provided by App Connect Designer below.

A helpful feature offered by the Smart Connectors is the **“Try this action”** button on the right of the screen. Clicking this button will allow you to test your ServiceNow connection. If your credentials and operations are configured correctly you should be able to pull records from ServiceNow. 

![alt text][pic15]

19\. After clicking the “Try this action” button you will see the test results.

![alt text][pic16]

20\. By clicking on the **View Details**, you will be able to see all the details for the ServiceNow system user records you have retrieved. Click on any one of your system users and you should be able to see the details associated with it. 
Once done reviewing click on the “x” in upper right corner to close the test window.

![alt text][pic17]

21\. Now we can configurate our API Response body to populate a successful response message with the data fields we are interested in returning to our consumer. Go ahead and click the Response button on the integration flow

![alt text][pic18]

22\. This we where we can utilize the in-built *Smart Mapping* feature provided by IBM App Connect Designer. *Smart Mapping* grabs all the fields available from an external object which is a ServiceNow account in our example.

It allows you to choose any of the available data fields and allows you to perform custom functions on your data. For example, if we want to format an Account Name to be in lowercase characters, we can click on the function button next to our **Request Body** keys to insert a variety of helpful data transformation functions. 

Now we will map our API Response keys to the respective values we want our consumer to obtain from ServiceNow. Let us start with the SystemUserID field. 

Click on the hamburger icon next to SystemUserID field.   
Now you will see the list of Available mappings. 

Click on the ServiceNow / Retrieve system users mapping and select Sys id. Repeat the process for the other data fields. 
You can also start typing for example in the FirstName field and that will take you directly to the mapping. 
After populating all the fields your mapping should match the image attached below then click **Done**


![alt text][pic19]

23\. This will take you back to the main page for this API.  Click on the 3-dot menu next to stop and select Start API.  It will change from Stop to Starting and once it shows Started Click on the Test on the menu and continue to next section.  

![alt text][pic20]

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


# 2a Testing the API flow <a name="testing_the_API_flow"></a>
Make sure your API is running by checking the upper pane of your Designer instance. Since App Connect Designer has an built-in REST API testing utility. 

1\. Now select the GET operation on the left menu and review the information on this API we just created.  Now you should be able to see the Details pane describing the properties and parameters of your REST API operation. The full URL endpoint for your Designer flow is also displayed.

![alt text][pic21]

2\. Now click on the Try it button.  

![alt text][pic22]

3\. Scroll down and click on the **Send** button. This will trigger an API call to your Designer flow and in turn populate a Request and Response pane below the Send button.
You will see the first 4 entries returned for each of the fields we mapped into the response.

![alt text][pic23]

[pic21]: images/21.png
[pic22]: images/22.png
[pic23]: images/23.png


# 2b Add an Additional Operation for our ServiceNow API <a name="add_an_additional_operation_for_our_servicenow_API"></a>
In this section we will add an additional operation to get Account by ID.

1\. Before we start this we will need to stop the API.  In the upper right corner select the 3 dots and click on Stop API

![alt text][pic24]

2\. Now we will go back to the Define tab of our API to add another operation.   
First select to add another operation and select the Retrieve SalesforceRetrieve by ID. 

![alt text][pic25]

![alt text][pic26]

3\. Select “Implement flow” for the new operation and that will get us to the flow editor where we will select the “+” sign and scroll down to ServiceNow connector and select Retrieve accounts.

![alt text][pic27]

4\. We will now add a condition to retrieve the System Users ID for the ID that is passed to the API.  
Click on the Add condition and you will see the Where clause for the equals condition click in the blank box and you will see the mapping option there where you can select the Sys id that is passed to the API.   

![alt text][pic28]

When done should look like the following:
![alt text][pic29]

5\. Now we can configurate our API Response body to populate a successful response message with the data fields we are interested in returning to our consumer. Go ahead and click the Response button on the integration flow.

![alt text][pic30]

6\. Now we will map our API Response keys to the respective values we want our consumer to obtain from ServiceNow. Let us start with the SystemUserID field. 

Click on the hamburger icon next to SystemUserID field.   
Now you will see the list of Available mappings. 

Click on the ServiceNow / Retrieve system users mapping and select Sys id. Repeat the process for the other data fields. 
You can also start typing for example in the FirstName field and that will take you directly to the mapping. 
After populating all the fields your mapping should match the image attached below then click **Done**


7\. Now we will map our API Response keys to the respective values we want our consumer to obtain from ServiceNow. Let us start with the SystemUserID field. 

Click on the hamburger icon next to SystemUserID field.   
Now you will see the list of Available mappings. 

Click on the ServiceNow / Retrieve system users mapping and select Sys id. Repeat the process for the other data fields. 
You can also start typing for example in the FirstName field and that will take you directly to the mapping. 
After populating all the fields your mapping should match the image attached below then click **Done**

![alt text][pic31]


[pic24]: images/24.png
[pic25]: images/25.png
[pic26]: images/26.png
[pic27]: images/27.png
[pic28]: images/28.png
[pic29]: images/29.png
[pic30]: images/30.png
[pic31]: images/31.png


# 2c Testing the New API Operation <a name="testing_the_new_API"></a>
Make sure your API is running by checking the upper pane of your Designer instance. Since App Connect Designer has an built-in REST API testing utility. 

1\. Click in the upper right cornor hamburger tab and select Start API.
![alt text][pic32]

2\. Click on the Test menu on top
As you can see we have two operations now one that will get us the first four accounts and the other will get account by id.   
So let’s first run the user GET first to get a list of user IDs.

![alt text][pic33]

3\. Now click on the **Try it** button.  
Scroll down and click on the Send button. This will trigger an API call to your Designer flow and in turn populate a Request and Response pane below the Send button.

![alt text][pic34]

4\. After clicking  the Send button you will see the Response with list of SystemUserID.

![alt text][pic35]

Pick one of the SystemUserID from the Response to use in the other Operation.

5\. Now select the GET operation on the left menu and review the information on this new operation we just created.  You will see a required field for this API called id*  enter one of the SystemUserID from the last step.  Then click **Send**

![alt text][pic36]

6\.You will see the response for the SystemUserID that you entered for the API call. 
![alt text][pic37]

[pic32]: images/32.png
[pic33]: images/33.png
[pic34]: images/34.png
[pic35]: images/35.png
[pic36]: images/36.png
[pic37]: images/37.png
# 3. Deploying Your Designer Flow to App Connect Dashboard <a name="deploying_your_designer_flow_to_app_connect_dashboard"></a>

Now we can export our Designer flow App Connect Dashboard on Cloud Pak for Integration. Navigate to your App Connect Designer Dashboard so we can export our flow as a BAR file. The Dashboard for App Connect Designer is on the left-hand pane. After navigating to the Dashboard, click on the triple-dot icon on your Designer flow. 

Now click on **Export** and then select **Runtime Flow Asset (BAR).** This will allow you to download the BAR file to your local directory. 

![alt text][pic38]

1\. Click on Dashboard to get back to the main designer page where you will see your API running.

![alt text][pic39]

2\.You will see that your API is running and you then will click on the triple-dot icon on your Designer flow.  Select Export.
![alt text][pic40]

3\. We will export this API as a runtime flow asset.
![alt text][pic41]

4\. This will save the ServiceNowRetrieve.bar file locally on your machine and will use that to deploy to the AppConnect runtime. 

5\. Now we will go back to the Integrtion home page. Click on the IBM Cloud Pak for Integration on the top menu
![alt text][pic42]

6\. From the Platform Navigator, select your App Connect Dashboard instance.
This should be prefix with your user id that you used to sign in with.  In this example it is showing sign in as cody9.

![alt text][pic43]

7\.Now select the Create a server option from your App Connect Dashboard capability.
![alt text][pic44]


8\. We will now select the Designer Integration that we will deploy then click next.

![alt text][pic45]

9\. Now we will either drag and drop the BAR file we just exported or we can click to upload it.  Then click next.

![alt text][pic46]

10\. The next section is for configuration you can look at all the options that are available.   We will just be using the Designer Accounts which will include your ServiceNow credentials.

![alt text][pic47]

11\. The final section is the server details.   We will give it a name, set the flow type, and change the Replicas to 1.  Go ahead and click Create.

![alt text][pic48]

12\. This will take you back to the Servers Dashboard where you will see your new server.   To start with it will be showing Unavailable while it is starting up the pods for it. 

![alt text][pic49]

13\.You can click the refresh in the upper right corner.  
Once it is up and running it will show the following:

![alt text][pic50]

14\. We can also quickly test the API call running in the Integration server.   Select the Get accounts and then select the GET url and paste in a browser window.

![alt text][pic51]

15\. You will see the following results.
![alt text][pic52]

[Return to main lab page](../index.md)

[pic38]: images/38.png
[pic39]: images/39.png
[pic40]: images/40.png
[pic41]: images/41.png
[pic42]: images/42.png
[pic43]: images/43.png
[pic44]: images/44.png
[pic45]: images/45.png
[pic46]: images/46.png
[pic47]: images/47.png
[pic48]: images/48.png
[pic49]: images/49.png
[pic50]: images/50.png
[pic51]: images/51.png
[pic52]: images/52.png

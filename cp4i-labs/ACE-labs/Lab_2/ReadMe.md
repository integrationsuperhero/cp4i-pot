# IBM App Connect Enterprise

[Return to main lab page](../index.md)

## Distributing workload using ACE v11 Callable Flows
### Featuring:
- Callable Flows
- IBM App Connect on Cloud Pak for Integration (CP4I)
- IBM App Connect Enterprise v11
---
# Table of Contents
- [1. Introduction](#introduction)
- [2. Create MyLoggerCF](#create_myloggercf)
  * [2.1 Putting integration servers to work!](#putting_integration_servers_to_work)
    + [2.1.1 Import MyCallableFlows](#import_mycallableflows)
    + [2.1.2 Review MyCallableFlows](#review_mycallableflows)
    + [2.1.3 Deploy MyCallableFlows](#deploy_mycallableflows)
  * [2.2 Configure the Callable Flows in Cloud Pak for Integration (CP4I)](#configure_the_callable_flows_in_cp4i)
  * [2.3 Create a Designer Flow in CP4I to call On-Prem Flow](#create_a_designer_flow_in_cp4i_to_call_onprem_flow)
  * [2.4 Test from the Designer Test Tab](#test_using_designer_test_tab)
  
---
# 1\. Introduction <a name="introduction"></a>
The purpose of this LAB is to show the configuration needed to distribute workload using IBM App Connect Enterprise Callable Flows.  

This lab was built using IBM App Connect Enterprise FP3 in a Windows 2010 environment.

# 2\. Create MyLoggerCF <a name="create_myloggercf"></a>

1\. Open the IBM App Connect Enterprise Toolkit

If you already have the toolkit open continue to step 3.   We will use workspace from lab 1  for the work in this lab guide. This is showing PoTWorkSpace on your local windows box.   If you have Linux then will use /home/PoTWorkSpace

![alt text][pic0]

2\. In the “Welcome to IBM App Connect Enterprise Toolkit” window click the arrow on the top right of the screen to go to the Integration Toolkit: 

![alt text][pic1]

[pic0]: images/0.png
[pic1]: images/1.png

## 2.1 Putting integration servers to work! <a name="putting_integration_servers_to_work"></a>
You now have a integration servers running: TEST_SERVER running with defaults settings;  You will now review a very simple application called PING_Basic and deploy it to integration servers you have running in your environment.  

## 2.1.1 Import MyCallableFlows <a name="import_mycallableflows"></a>
In this section we use the App Connect Enterprise Toolkit (Enterprise Toolkit) to develop and deploy a simple callable flow into an on-premises ACE integration server so that the flow is visible in Cloud Pak for Integration.

Now download the **MyCallableFlows-PI.zip** 
    Click here and save the zip file - [MyCallableFlows-PI.zip](MyCallableFlows-PI.zip)

The sample we will be using a Trace node to write a copy of the incoming payload to a file and a Compute node to modify the incoming message to add a status element.
In this next section you will import the application into your workspace so that you can review what it will do. 

1\. With your mouse right click on the background of the Application Development window and select “Import”

![alt text][pic2]

2.\ Select **IBM Integration** > **Project Interchange** then click the Next button:  

![alt text][pic3]

3\. Use the browse button to import the file <span style="font-weight:100">MyCallableFlows-PI.zip</span> from where you had downloaded it. 

Click Finish:

![alt text][pic4]

4\. The **MyCallableFlows** Application will be imported into your workspace, expand the application to see the message flow: 

![alt text][pic5]

[pic2]: images/2.png
[pic3]: images/3.png
[pic4]: images/4.png
[pic5]: images/5.png

## 2.1.2 Review MyCallableFlows <a name="review_mycallableflows"></a>

1\. Double click on LoggerCF.msgflow, this will open the message flow in window **<span style="color:red">(B)</span>**.

This flow has two paths.   For this lab the input node is a CallableInput node that will allow this flow to be invoked from the cloud. 

![alt text][pic6]

2\. Here if you click on the CallableInput you will see the Endpoint Name that will invoke this flow.  Next click on the Node Trace this will write the in coming payload to the file name **logger.out**. 

**Note:** ***This is showing a Unix directory but the artifacts have a windows directory.  Change this to match the enviroment you are running the Toolkit in.***

Click on the ModifyMessage Compute node and it shows we add a status of ‘done’ 

![alt text][pic7]

4\. Double click on the node called “Compute” to see the data that will be returned from the http request when the message flow us started: 

The flow will return the following: 

<span style="color:#E1C4D8">Set</span> <span style="color:#3F3FBF">OutputRoot.JSON.Data.pingbasic.Server = ExecutionGroupLabel</span>;

<span style="color:#E1C4D8">Set</span> <span style="color:#3F3FBF"> OutputRoot.JSON.Data.pingbasic.WorkPath = WorkPath</span>;

<span style="color:#E1C4D8">Set</span> <span style="color:#3F3FBF"> OutputRoot.JSON.Data.pingbasic.MsgFlow = MessageFlowLabel</span>;

<span style="color:#E1C4D8">Set</span> <span style="color:#3F3FBF"> OutputRoot.JSON.Data.pingbasic.DateTime</span> = <span style="color:#E1C4D8">CURRENT_TIMESTAMP</span>;

i.e. The **server name** that the flow is running on; the **WorkPath** of the server; the **message flow name**; the **current timestamp**; 

5\. Close the esql editor and the message flow without making any changes: 

![alt text][pic8]

[pic6]: images/6.png
[pic7]: images/7.png
[pic8]: images/8.png

## 2.1.3 Deploy MyCallableFlows <a name="deploy_mycallableflows"></a>

1\. Right click on the MyCallableFlow and select Deploy

![alt text][pic10]

2\. Select the Integration Servers TEST_SERVER to deploy our flow

![alt text][pic11]

3\. 

![alt text][pic12]

4\. We now have our Callable flow deployed and running on the local Integration Server

![alt text][pic13]

[pic10]: images/10.png
[pic11]: images/11.png
[pic12]: images/12.png
[pic13]: images/13.png

## 2.2 Configure the Callable Flows in Cloud Pak for Integration (CP4I) <a name="configure_the_callable_flows_in_cp4i"></a>

In this section we use App Connect Designer to configure callable flows, to enable secure connectivity between flows running in IBM App Connect on IBM Cloud and in an integration server in your on-premises App Connect Enterprise.

1\. Open a Firefox browser window and go to the following URL: 

[https://integration-navigator-pn-cp4i.apps.wedge.coc-ibm.com/](https://integration-navigator-pn-cp4i.apps.wedge.coc-ibm.com/)

**Note:** ***if you already have the CP4I Platform Navigator page open go to step 4***

2\. Select the Enterprise LDAP:

![alt text][pic14]


3\. When prompted use the username and password provided to you for this lab. In this example we are using wedge10. 

![alt text][pic15]

4\. Click on the App Connect Designer link to take you to the designer dashboard.”

![alt text][pic16]

5\. Click on the Callable flows icon:

![alt text][pic17]

6\. This is the configure callable flow page.   Click on the Connect callable flows to get to the download page. 

![alt text][pic18]

7\. Now we will need to download the agent configuration json file that we will add to the on prem server to create the secure connection between the onprem and CP4I.

**Note:** ***don’t close this window we will use it to test the connection***

![alt text][pic19]

8\. Take the agentx.json file we just downloaded and copy to the TEST_SERVER config location. This is showing the PoTWorkSpace location on windows server. Copy the json file to the location in the server directioy in the agentx directory.    

The logging file will then be created:

![alt text][pic20]

9\. Stop and start the **Test_Server**

10\. Now return to the window that you opened in CP4I designer to download the json file.   Click on the Test your agent and you will see agents connected.   

You will see at least 1 agent. 

**Note:** ***If you closed the window go back to step 2 and that will open the window again just disregard the download button.***

![alt text][pic21]

[pic14]: images/14.png
[pic15]: images/15.png
[pic16]: images/16.png
[pic17]: images/17.png
[pic18]: images/18.png
[pic19]: images/19.png
[pic20]: images/20.png
[pic21]: images/21.png

## 2.3 Create a Designer flow in CP4I to call on-prem flow <a name="create_a_designer_flow_in_cp4i_to_call_onprem_flow"></a>

In this section we use App Connect Designer to configure callable flows, to enable secure connectivity between flows running in IBM App Connect on IBM Cloud and in an integration server in your on-premises App Connect Enterprise.

1\. Click on the **App Connect Designer** dashboard icon:

![alt text][pic22]

2\. Select from the New drop down to create a new API flow:  

![alt text][pic23]

3\. First thing we will do is create the model for this.  We will call the model **CallableFlow**

![alt text][pic24]

4\. We will add 3 properties to this model: Name, Message, and Status

![alt text][pic25]

5\. Now that we have the model we will select the Operations tab and select the Create CallableFlow.

![alt text][pic26]

6\. Now select the Implement flow button and that will open the flow editor.

![alt text][pic27]

7\. ![alt text][pic28]

8\. Here we will select the MyCallableFlows for the application.  This is the integration running on-prem.  The endpoint is the name of the CallableInput node in the flow. 

We will add the data objects aName and aMessage that will pass data to the on-prem flow.

![alt text][pic29]

9\. Now we will select the Response and update the Reponse body. 

We will leave the Reponse header as 201.

For the Response body will add the Name that we input to the API call.

![alt text][pic30]

10\. For the status we will take the update that was made in the compute node on the on-prem flow.   Cut and paste this into the Status field: **{{$CallableflowInvoke.message.status}}**

![alt text][pic31]

11\. Before starting the API make sure we have the name set to CallableFlow_Test.   This is used as part of the base URL of the API we will be testing.  

Click on the 3 dots and select Start API on the right side.

![alt text][pic32]

[pic22]: images/22.png
[pic23]: images/23.png
[pic24]: images/24.png
[pic25]: images/25.png
[pic26]: images/26.png
[pic27]: images/27.png
[pic28]: images/28.png
[pic29]: images/29.png
[pic30]: images/30.png
[pic31]: images/31.png
[pic32]: images/32.png

## 2.4 Test from the Designer Test tab <a name="test_using_designer_test_tab"></a>

1\. Now click on the Test tab to get the info needed to test this API.  Once on the following the select the POST/CallableFlow to be able to test your API.

![alt text][pic33]

2\. Next Select the Try it tab and you will see that for the Authorization Username and Password are populated. 

![alt text][pic34]

3\. Scroll down and for in the body you will put a Name and Message in the format below:

<code>
    
    {
        "Name": "Joe Jodl",
        "Message": "Test my on-prem callable flow from CP4I"
    } 

</code>

![alt text][pic35]

4\. Click the Send button and you will see the results of the call. 

![alt text][pic36]

5\. Go back to your on-prem server where you set the trace node to log info.  Open the logger file and you will see the results of the on-prem flow running.

![alt text][pic37]
![alt text][pic38]

[pic33]: images/33.png
[pic34]: images/34.png
[pic35]: images/35.png
[pic36]: images/36.png
[pic37]: images/37.png
[pic38]: images/38.png

[Return to main lab page](../index.md)

# <span style="color:teal">END OF LAB GUIDE</span>

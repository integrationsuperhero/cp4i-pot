# IBM API Connect


## API lifecycle include creating, running, managing, and securing APIs


---

# Table of Contents 
- [1. IBM API Connect](#ibm_api_connect)
- [2. The Steps of the API Lifecycle Include Creating, Running, Managing, and Securing APIs](#the_steps_of_the_api_lifecycle_include_creating_running_managing_and_securing_api)
  * [2.1 Let's Start](#lets_start)
  * [2.2 Create](#create)
  * [2.3 Security Definition](#security_definition)
  * [2.4 Security](#security)
  * [2.5 Paths](#paths)
  * [2.6 Definitions (Optional)](#definitions)
  * [2.7 Properties](#properties)
  * [2.8 Target Services](#target_services)
  * [2.9 Categories](#categories)
- [3. Assemble View](#assemble_view)
- [4. Publishing](#publishing)
- [5. Developer Portal](#developer_portal)
- [6. Summary](#summary)

---

# 1. IBM API Connect <a name="ibm_api_connect"></a>

IBM API connect is an integrated API management offering, where all of the steps in the API lifecycle, and the actions that surround it, are performed within the offering.

# 2. The Steps of the API Lifecycle Include Creating, Running, Managing, and Securing APIs <a name="the_steps_of_the_api_lifecycle_include_creating_running_managing_and_securing_api"></a>

* Create Develop and write the API definition and implementation, and test the API.
* Run Package and deploy the API. Ensure that the API is hosted securely on a stable platform.
* Manage Create and manage self-service portals that expose the API to API consumers. Monitor the set of rules and conditions that govern the API to ensure it is fulfilling its intended purpose, and make adjustments if necessary. Retire and archive the API when appropriate.
* Secure Incorporate access control, monitoring, and logging to properly secure the API.

# 2.1 Let's Start <a name="lets_start"></a>
First make sure you are logged into the CP4I Platform Navigator using the wedgeX account that was provided to you. If you are already logged in you can skip these steps. 

1\. Open a Firefox browser window and use the URL provided from the instructor to access the Platform Navigator.

**Note: if you already have the CP4I Plateform Navigator page open go to step 4**

2\. Select the Enterprise LDAP:

![alt text][pic0]

3\. When prompted use the username and password provided to you for this lab. 
In this example we are using wedge10. 

![alt text][pic1]

4\. Click on the API Connect link to take you to the API Manager Home page.”

![alt text][pic2]

5\. You will now be on the APIC log in page. Select the CoC LDAP User Registry 

![alt text][pic3]

6\. Enter your username and password that you used to sign in to the platform navigator. 

![alt text][pic4]

7\. When logged in and connected to the APIC Home Dashboard you will see a few tiles and a tab on the left-hand side of the page.

![alt text][pic5]

[pic0]: images/0.png
[pic1]: images/1.png
[pic2]: images/2.png
[pic3]: images/3.png
[pic4]: images/4.png
[pic5]: images/5.png


# 2.2 Create <a name="create"></a>

There are a few ways to pull existing API’s flows or manually expose an API on this page. Whether it’s starting from scratch or pulling from an asset from a connected asset repo they all achieve the same thing.

For this Lab we will use the Open API Document (salesforce-0.0.1.yaml) we downloaded from our ace integration server earlier in order to import the API.

1\. For now, we will click add and then api from the dropdown.
On the create page you will be greeted with a few choices of how you would like to add an API.

![alt text][pic6]

2\. On the create page you will be greeted with choices of how you would like to add an API. And on the top you will see option for OpenAPI 2.0 or Open API 3.0.  For this lab we will use the **OpenAPI 2.0**
Go ahead and click Import from existing API Import and  click Next 

![alt text][pic7]

3\. On the Import API page either drag and drop the yaml file from the Saleforce Designer lab or click to upload it.
Click Next.

![alt text][pic8]

4\. The next screen will ask if you want to activate the API. This will automatically create and expose your api however for this lab we will not check that box and click **Next**

5\. You will see the following summary page that shows the definition was successful generated. Click on **Edit API**

![alt text][pic9]

6\. This will populate the fields inside APIC with what was able to be pulled from the document we imported.

You should now land on API Designer page below containing a Design, Source, and Assemble tab.  We are on the API Setup tab.

![alt text][pic10]

7\. The API Designer is a graphical user interface within the developer toolkit and provides functions for the creation and configuration of API definitions, running offline.

Before getting started with securing and setting up our API let’s make a few changes in the API Setup page section.
* Scroll down the page and enable https under the **Schemes** section.
* Under **Host** remove the address (save that for later)
* Make sure the **Base Path** section matches the base path of your API **( /salesforce )**
* Hit **Save** at the top right of the page.


[pic6]: images/6.png
[pic7]: images/7.png
[pic8]: images/8.png
[pic9]: images/9.png
[pic10]: images/10.png

# 2.3 Security Definition <a name="security_definition"></a>

1\. Moving on to Securing the API. On the left-hand side let’s click on **Security Definitions.** 

The click on add and we will start adding the Client ID

![alt text][pic11]

2\. We will first create a client-id filling in the page with the following info.  Once complete click on the Save button in upper right corner. 

![alt text][pic12]

3\. We are going to want to pair this Client Id with a Client Secret so click add to open new Create Security definition page. 

Fill the form as we did with Client Id but now as a Secret.  It should look like the following screen, then hit save. 

![alt text][pic13]

[pic11]: images/11.png
[pic12]: images/12.png
[pic13]: images/13.png


# 2.4 Security <a name="security"></a>

Now that the security definition for client and secret has been established let’s enable it by opening up the next option in the side panel **Security**

1\. Click on the Add button and you will see the Client-Id/Secret here with check boxes next to them. Check both boxes for the Client Secret and ID and then **Save.**

![alt text][pic14]

[pic14]: images/14.png

# 2.5 Paths <a name="paths"></a>

Let’s move on to the Path’s panel by clicking **Paths** on the side panel. We should see the path from our APIs populated in this section for us already.  

1\. Let us start with the accounts path. 

![alt text][pic15]

2\. This page will show the option to add any path parameters or operations. Since the API we created is utilizing a /get request lets scroll down and ensure it exists.

![alt text][pic16]

You can click on the GET operation to open a new page and view its configuration. If the operation requires or is able to take any set parameters this is where you would include those. For this instance, we do not have any parameters that belong to the request so we will leave it blank. 

3\. Now let us look at the AccountID path.  From the edit page click on the GET operation to open a new page and view its configuration.

![alt text][pic17]

4\. Here you see we have a parameter for this GET.	

![alt text][pic18]

Click on the Path in the top to get back to the main Design page.

![alt text][pic19]


[pic15]: images/15.png
[pic16]: images/16.png
[pic17]: images/17.png
[pic18]: images/18.png
[pic19]: images/19.png


# 2.6 Definitions (Optional) <a name="definitions"></a>
In the Definitions section you can create JSON schema definitions. You reference these definitions in an operation to provide developers with information about the JSON request they should make or the JSON response they should expect to receive from the operation. Your schema definitions are made available to developers through the Developer Portal but are not enforced in any calls to the API unless a Validate policy is used.

* Click the Add Definition icon.
* A new definition is created.
* Click the newly created definition to expand its details.
* Complete the Name field for your definition.
* From the Type drop-down list, select the type of your definition.
* Optional: In the Description field for your definition, provide a description of what is defined by the definition.
* Complete the details of your definition’s properties. Each property requires a name and type and can also have a description.
* Optional: To specify that a property is required when the operation is called, select it using the check box in the Required The Required icon column.
* Optional: You can add additional properties by clicking Add Property.
* Optional: You can delete properties or definitions by clicking the Delete icon The Delete icon next to the property or definition.
* If you want to allow the inclusion of properties that are not included in the definition, so that validation will not fail when a validate-rest policy is used on the request, set Allow additional properties to the On position.

# 2.7 Properties <a name="properties"></a>

In the Properties section, define any API properties that you want to use. Your APIs are configured by using properties. Properties are used by the gateway to control behavior of certain policies. Typically, you provide properties, but the policy can also provide properties settings. In API Connect, you can create API properties that consist of Catalog-specific values to eliminate the need for source code modifications. You can then reference the properties elsewhere in your API definition. 

1\. Click on the Properties on the left menu. 

![alt text][pic20]

2\. We should see a **“target-url”** property already created. Let’s click on this property to see how its configured. The default value should match the ACE API url we are targeting. If it does not, please change it now and hit save. This was the url we saved from the API setup page. 

![alt text][pic21]

[pic20]: images/20.png
[pic21]: images/21.png

# 2.8 Target Services <a name="target_services"></a>

If you have an existing REST service that you want to expose through an IBM API Connect API definition, you can create a proxy API and specify the target endpoint by using Target Services in the API Manager at the start or here.

# 2.9 Categories <a name="categories"></a>

You can organize your APIs and Products into categories. The APIs and Products that you categorize in the API Designer or API Manager UI are displayed within the Developer Portal, in their defined categories.

# 3. Assemble View <a name="assemble_view"></a>

The API Designer features an assemble view that you can use to create assemblies. With assemblies, you can readily tailor your APIs to include components such as activity logging and redaction of specific fields.
This view includes a palette, which lists available components, a property sheet, which is used to configure a component, and a canvas, which is used to arrange and visualize the assembly’s components.
We won’t be exploring all these features in this lab but feel free to explore your options elsewhere in your API definition. 

1\. Click on Assemble tab to get to the Assemble view

![alt text][pic22]


2\. We are now on the Assemble view page.

![alt text][pic23]

3\. Click the invoke component to show the property sheet. 

If you noticed the endpoint does not include the path so let’s add that now. Right after the $(target-url) please type $(request.path).  This will append the path we created earlier to our Invoke components URL. Click Save in the upper right corner.

![alt text][pic24]

4\. To activate and test this API we can click on the **Online** button.  Then click **Save**

![alt text][pic25]

You will now see that the API is online and ready to be tested.  It will show the Test tab now is active. 
Click on the Test tab.  

![alt text][pic26]

5\. On the test page you will see all the operators that are in this API. We have the accounts and the AccountID.   We will select the accounts GET and click on the Send button.  

![alt text][pic27]

6\. On the response page you will see the request and the response from the AppConnect Designer API we had created. 

![alt text][pic28]


7\. You can also test the AccountID operator but using one of the ids from the previous call.

![alt text][pic29]

The Response will return just the one AccountID

![alt text][pic30]


[pic22]: images/22.png
[pic23]: images/23.png
[pic24]: images/24.png
[pic25]: images/25.png
[pic26]: images/26.png
[pic27]: images/27.png
[pic28]: images/28.png
[pic29]: images/29.png
[pic30]: images/30.png

# 4. Publishing <a name="publishing"></a>

Now that your API has been activated and tested to work you may want to publish it to a product that can make use of it, or if you’re just starting like us we can create a product for this API to live within. 

1\. There are a few ways to go about this but for this lab let’s go back to the development tab that we first saw when we attempting to create an API.

![alt text][pic31]

2\. Once here you will see the title, version, type, and time last modified of your API. Click the three dots at the end of your API and choose **Publish.**

![alt text][pic32]

3\. Since this is our first product let’s go ahead and give it a title and click next.

![alt text][pic33]

4\. Each organization can create and manage several catalogs containing different combinations of API and products and its own developer portal. For this lab let’s stick with the sandbox catalog and click **Publish.**

![alt text][pic34]

5\. We have now created a consumable product that we can find in our developer portal.

Something to note is we completely skipped the stage portion of the product. Normally you would want to stage the product make changes to visibility, subscribability, API’s, categories to include, and lastly subscription plans and rate limits. An example of what I’ve mentioned can be seen below.

![alt text][pic35]

[pic31]: images/31.png
[pic32]: images/32.png
[pic33]: images/33.png
[pic34]: images/34.png
[pic35]: images/35.png


# 5. Developer Portal <a name="developer_portal"></a>

Application developers discover and use APIs by using the Developer Portal. You can customize the Developer Portal for your application developers.
In addition to allowing application developers to find and use both free and paid APIs, the Developer Portal provides additional features including forums, blogs, comments, and ratings, together with an administrative interface for customizing the Developer Portal. 

Now that your product is published let’s view it in the developer portal. This can be found under the Manage section of APIC. 


1\. Click on the Manage Tab on the left side bar.

![alt text][pic36]

2\. Click the catalog in which you published the API (sandbox).

![alt text][pic37]

3\. Click on Catalog setting

![alt text][pic38]

4\. Copy and paste the Portal URL into your browser in a new tab.

![alt text][pic39]

5\. The portal is setup for self service so we will create a new account as a developer.

![alt text][pic40]

6\. Fill in the form and make sure to use a valid email address since that is where the activation email is sent.  At the bottom when done click on Sign up.

![alt text][pic41]

7\. You will receive an email that you will copy the link and paste in to your browser to complete the registration at which point you can log in. 

![alt text][pic42]

8\. Go now to the Sign in and enter your Username and password you just created.

![alt text][pic43]

9\. Once you are logged in your can explorer varies sections in the developer portal.   For now lets go the Account Product we created and Published to. 

![alt text][pic44]


10\. Now from the Products page we see our API for Salesforce Accounts and below that you see Plans.  This can be configured back in the Products section where you may add plans for Silver and Gold plans.   We have just the default for this one. Click on the API tile.

![alt text][pic45]

11\. Here we select the GET account operation and the try it. You will see that to test this API we need to register an application. Click on that link now. 

![alt text][pic46]


12\. Enter a name for this application and click **Save**.

![alt text][pic47]

13\. You will get the following page.  Save the Key and Secret into notepad and then click OK

![alt text][pic48]

14\. This will take you to the credentials page for the new applications you created. 

![alt text][pic49]

15\. With an app now created let’s travel back to the API Products page of the developer portal (upper left) and click on the product shown that we created and published to. 

![alt text][pic50]

16\. We will also need to subscribe to a plan for this Product.  Since we only have the Default plan we will use that.

![alt text][pic51]


17\. Select the existing application.

![alt text][pic52]


18\. Confirm subscription click next

![alt text][pic53]

19\. Subscription completed.  Click done

![alt text][pic54]

20\. Click on the API that we will now test.

![alt text][pic55]

21\. Here we will select the GET account operation on the and then select Try it.   
The Client ID will have the App name we created earlier.   You will need to copy the secret that we saved and paste it in the Client secret. Then click Send.

![alt text][pic56]

22\. You will see the response on the bottom of the page. 

![alt text][pic57]

23\. Now that we have ran the API several times, click on Apps on the top menu and select the Active app that we are using.  

![alt text][pic58]

24\. This will give you info on the APIs that you are running. 

![alt text][pic59]

The End.

[pic36]: images/36.png
[pic37]: images/37.png
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
[pic53]: images/53.png
[pic54]: images/54.png
[pic55]: images/55.png
[pic56]: images/56.png
[pic57]: images/57.png
[pic58]: images/58.png
[pic59]: images/59.png


**APIC Lab 1 - Create and Secure an API**

In this lab, you will get a chance to use the online APIC Developer
Toolkit and its intuitive interface to create a new API using the
OpenAPI definition (YAML) of the existing product inventory RESTful
web-service.

In this tutorial, you will explore the following key capabilities:

-   Creating an API by importing an OpenAPI definition for an existing
    REST service.

-   Configuring ClientID/Secret Security, endpoints, and proxy to invoke
    endpoint.

-   Testing a REST API in the online developer toolkit.

-   Publish an API for developers.

[Return to main API lab page](../index.md)
----------------------------------------------------------------------------------------------
 Import API to the Developer Workspace
===========================================================================================

First, we will download the OpenApi file for the existing REST service
for Inventory. Then, we will import it to the online workspace.

1.  Open a browser window to the API Manager Portal. If the screen
    displays [[\"Your connection is not
    private\"]] click
    Advanced, and then Accept the to continue. Log in with the username
    ad credentials supplied.

    ![](images/tutorial_html_228c6cdfd6f4d489.png)

    When you login for the first time you will see What's new in API Connect
    10. Click **Done** after reviewing.

    ![](images/tutorial_html_db2469619b74ee90.png)

2.  Click on the [[Develop APIs and
    Products]] tile
    to enter the online development workspace.

    ![](images/tutorial_html_61b4022571d0a4a3.png)  

3.  Now you are in the home screen of the online developer tool. From
    here, you can begin to create APIs and Products.

    ![](images/tutorial_html_333c6b76e2638b45.png)  

4.  Ensure you are on APIs tab. Click [[ADD]]

    ![](images/tutorial_html_993047b3f798317c.png)  

5.  On the next screen, select [[Existing OpenAPI]] under
    Import section, as shown in the image below. Then
    click **[Next.]**

    ![](images/tutorial_html_b219e12b9ba30a1c.png)  

6.  Now download the **Inventory.yaml** 
    Click here and save the yaml file - [inventory.yaml](Inventory.yaml)

    On the Import page select the upload file and select the yaml you just download and Click **[Next.]**

    ![](images/tutorial_html_64514a49c35e90d4.png)  

7.  **[Do not ]**select **[Activate
    API]**.
    Click [[Next]].

    ![](images/tutorial_html_3e51d8ec0929f2b5.png)  

8.  The API should be imported successfully as shown in the image below.
    Click [[Edit
    API]].

    ![](images/tutorial_html_83ece115b799d430.png)

 Configure API
===================================================================

After importing the existing API, the first step is to configure basic
security before exposing it to other developers. By creating a client
key and secret security, you are able to identify the app using the
services. Next, we will define the backend endpoints where the API is
actually running. API Connect supports pointing to multiple backend
endpoints to match your multiple build stage environments. Finally, we
will configure the proxy call to invoke the endpoint.

 Configure API Key security
---------------------------------------------------------------------------------------------------------------------------------------------

1.  Click [[Security
    Definitions]].

2.  In the [[Security
    Definition]] section,
    click
    the [[Add]] button
    on the right. This will open a new view titled [**[API Security
    Definition]**[.]]

3.  In the **[Name]** field,
    type [[client-id]].

4.  Under **[Type]**, choose [[API
    Key]].
    This will reveal additional settings.

5.  For **[Located
    In]** choose [[Header]].
    For **[Key Type]** choose [[Client
    ID]].
    In [[Parameter
    Name]] type [[X-IBM-Client-Id]].
    Your screen should look like the image below. 

    ![](images/tutorial_html_9acabae1c0f045ea.png)

6.  Click
    the [[Save]] button
    to return to the **[Security
    Definitions]** section.

7.  Click [[Add]] again
    to add the client secret definition.

8.  Under **[Name,]** type [[secret]].

9.  For **[Located
    In]** choose [[Header]].
    For **[Key Type]** choose [[Client
    Secret]].
    In [[Parameter
    Name]] type [[X-IBM-Client-Secret]].
    Your screen should look like the image below. 

    ![](images/tutorial_html_c8364653a0d1e2f5.png)

10. Click
    the [[Save]] button
    to return to the **[Security
    Definitions]** section.

    ![](images/tutorial_html_41e66c41b43e89ac.png)

11. Click [[Security]] in
    the left menu.

12. Click [[Add. ]]This will
    populate the **[Security
    Definitions]** table with secret and
    client-id. Select both as shown in the image below. Then
    click [[Save]]. 

13. Add security and enable secret and client-id. Click **Save** to save
    the changes.

    ![](images/tutorial_html_5bd00a842ec2bfff.png)

 Define Target-URL for Sandbox environment
------------------------------------------------------------------------------------------------------------------------------------------------------------

1.  Click
    on [[Properties]] in
    the left menu.

2.  Click on the target-url property. The target-url property is
    automatically inserted to be able to define multiple run-time
    targets for the service.

3.  In the **[Default value]** text field,
    type [https://apic-pot-inventory-api.mybluemix.net](https://apic-pot-inventory-api.mybluemix.net/)

4.  Click **[Add]**

5.  Select the **[Sandbox]** from Catalog and
    for the URL
    type [https://apic-pot-inventory-api.mybluemix.net](https://apic-pot-inventory-api.mybluemix.net/)

![](images/tutorial_html_f977429f6db6091a.png)

6.  Click **[Save]** to complete the
    configuration.

 Configure Proxy Call in Designer
---------------------------------------------------------------------------------------------------------------------------------------------------

1.  On the top Navigation,
    click [[Assemble]].

2.  Click [[Invoke]] in
    the flow
    designer.

3.  This will open a window from the right to configure. In the URL
    field, type **\$(target-url)\$(request.path)\$(request.search)**
    
    ![](images/tutorial_html_eda46641cdf764e6.png)

4.  Click [[Save]].

 Test the API
==================================================================

In the API designer, you have the ability to test the API immediately
after creation in the Assemble view!

1.  Toggle
    [[Offline]]
    to activate API. to publish the API itself to the gateway for
    testing.  

    ![](images/tutorial_html_227e8350d01d16f9.png)

2.  After the API is published, additional tabs appear your screen
    should look like the image below.
    
    ![](images/tutorial_html_a35d4b82b4aa8b10.png)

3.  Choose **[Test]** tab and select **[GET]** operation as shown below.

    ![](images/tutorial_html_5e2c8cff09f77c58.png)

4.  Your client Id  and client secret for the sandbox-test-app is
    prefilled.

5.  Click [[Send]].

6.  You may see a "No response received" pop-up windows if this is the first test of the API, due to a certificate exception raised by the browser. Simply click on the URL to launch a new browser tab and accept the risk to proceed.

    ![](images/tutorial_html_6400dc1e94d34fd8.png)

7.  Go back to the test view and
    click [[Send]] again.

8. Now you will see a Response section with Status code 200 OK and the
    Body displaying all the inventory items.

    ![](images/tutorial_html_d063fb9dba035b70.png)

 Publish API
=================================================================

In this lab, we will make the API available to developers. In order to
do so, the API must be first put into a product and then published to
the sandbox catalog. A product dictates rate limits and API throttling.
When the product is published, the Invoke policy defined in the previous
lab is written to the gateway. 

 Create Inventory Product and Add API
-------------------------------------------------------------------------------------------------------------------------------------------------------

1.  From the vertical navigation menu on the left,
    click **[Develop]** to return to the
    Develop home screen.

    ![](images/tutorial_html_fa935b3ea4222145.png)

2.  Switch to **[Products]** tab. Click **[Add]** and
    select **[Product]**

3.  On the next screen, select **[New Product]**. Then
    click **[Next]**.

4.  For the Title, enter [**[Inventory
    APIs]**. Click **[Next]**.

5.  Select the **[inventory 1.0.0 API]** as
    shown in the image below. Then
    click **[Next]**.  

    ![](images/tutorial_html_536925e23d552bb5.png)

6.  Keep the **[Default Plan]** as is.
    Click **[Next]**.  

    ![](images/tutorial_html_333097bd27fa8fa7.png)

7.  Under **[Publish]**, enable **[Publish Product]** as shown in the image below.
    Then
    click [**[Next]**[.  ]]

    ![](images/tutorial_html_850499fce1003aa7.png)

8.  The Product is now published successfully with the API base URL
    listed and available for developers from the developer portal. Go
    to [APIC Lab 2 - The Developer Portal
    Experience](https://github.ibm.com/americas-integration/cp4i-pot/tree/master/cp4i-labs/APIC-Labs/Lab2) to
    see how to access this API as a developer.

 Summary
=============================================================

You completed the APIC Dev Jam Lab 1 - Create and Secure an
API. Throughout the tutorial, you explored the key takeaways:

-   Create an API by importing an OpenAPI definition for an existing
    REST service.

-   Configure ClientID/Secret Security, endpoints, and proxy to invoke
    endpoint.

-   Test a REST API in the online developer toolkit.

-   Publish an API for developers.

Continue the APIC Labs! Go to [APIC Lab 2 - The Developer Portal
    Experience](https://github.ibm.com/americas-integration/cp4i-pot/tree/master/cp4i-labs/APIC-Labs/Lab2) to
learn how to socialize this API and make it available to developers.

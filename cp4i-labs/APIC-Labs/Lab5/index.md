**APIC Lab 5 - Advanced API Assembly**

In the previous labs, you have been working with an API that acts as a
pass-through to a microservice application.

In this lab, you will expand the product offerings for ThinkIBM. In
addition to the Inventory API, ThinkIBM wishes to provide APIs that
offer financing and shipping logistics to consumer applications. Your
goal is to utilize existing enterprise and public assets to create these
API offerings.

In this tutorial, you will explore the following key capabilities:

-   Create a new API, including object definitions and paths.

-   Configure an API to access an existing SOAP service.

-   Import an existing API from an OpenAPI definition document (a.k.a
    Swagger).

-   Map data retrieved from multiple API calls into an aggregate
    response.

-   Use GatewayScript directly within an API assembly.

[Return to main API lab page](../index.md)

Prerequisites: Labs 1-4

 Create and Define the Financing API (REST to SOAP)
=========================================================================================================

ThinkIBM wants to give its customers the ability to calculate financing
payments. There is already a legacy SOAP-based application which will do
the calculation, but it should be exposed to consumers as a modern
RESTful API. In this section, you will create a new OpenAPI definition
for the financing API.

1. From the left navigation menu,
  click **[Develop]**

2. Click **[Add]** and
  choose **[API]**.

    ![](images/tutorial_html_35bc8347ebf9f3c4.png)

3. Select **[New OpenAPI]** and click [[Next]]

    ![](images/tutorial_html_8027761d9675e244.png)

4. Fill in the form for **Create New OpenAPI** with the following values: 

    **[Title: financing]**

    **Name: financing**

    **Base Path: /financing**

    **Version: 1.0.0**

    Click **Next**.

    ![](images/tutorial_html_6dab5b579d7af76.png)

5. Leave all default values and click [[Next]]. API
    Connect will generate a new OpenAPI definition for the financing API and
    provide a summary with the performed activities.

    ![](images/tutorial_html_fb454c7ee948008d.png)

6.  Click  **[Edit API]** to customize the API

7. Create the model definition for the new API. These definitions are
    used in a few places. Their primary role is to serve as documentation in
    the developer portal on expected input and output parameters. However,
    they can also be used for data mapping actions.
    Click **[Definitions]** from the API
    Designer menu on the left. Then,
    click **[Add]** to create a new definition.

    ![](images/tutorial_html_f584c2696c3ce084.png)

8. Enter **[paymentAmount]** for **[Name]** and
    leave the definition **[Type]** set
    to **[object]**.

9. Click **[Add]** in
    the **[Properties]** section.

    ![](images/tutorial_html_332203efe7e366f5.png)

10. Edit the **property values** using the following values:

    **Property Name: paymentAmount**

    **Type: float**

    **Example: 199.99**

    **Description: Monthly payment amount**

    The page will look like this:

   ![](images/tutorial_html_c600b4bb8ec6adee.png)

    The property will be utilized in the Path you create next. Click [Save] to go back to the main API Editor.

11. Click [[Paths]] in the navigation menu on the left. Then edit the default path (shown as "/" in the picture below).

    ![](images/tutorial_html_f3f04d5e1fde784d.png)

12. The Edit Path screen is loaded. Edit the [[Path name]] to be **[/calculate]**. **[Note:]** [Recall that our Base
    Path for this API is \`financing\`. This new path will be appended to the base, creating a final path of 
    /financing/calculate]

13. Keep the **[[GET]]** operation and remove all other operations by click the three dots to the right of the operatorion
    and select **[[Delete]]** from the menu

    ![](images/tutorial_html_32f5ad5e80b58cd5.png)

14. After removing unsupported operations your API should look like: 

    ![](images/tutorial_html_aae3e2ff9be52791.png)

15. Click **[Save]**. You will be
    redirected to the main API Editor to continue.

16. Click the **[/calculate]** path we just created.

    ![](images/tutorial_html_864cc1225031590a.png)

17. Click the **[GET]** operation to add
    the request parameters. This defines the input to the API request. Since
    this is a GET request, you will add the required request parameters to
    the query component of the URI.

    ![](images/tutorial_html_2cf0c1234fbd4aa3.png)

18. Scroll down to the Parameters section within the operation config.
    Click **[[Add]]** in the **[[Parameters]]** section.
    You are actually going to need three total parameters for this
    operation, so go ahead and click the **[[Add]]** button **two more
    times** to add the parameter templates.

    ![](images/tutorial_html_1e46988677afe0a.png)

19. Edit the **parameters** to set the values:

```
  **Required**   **Name**   **Located In**   **Type**   **Description**
  -------------- ---------- ---------------- ---------- --------------------------
  yes            amount     Query            float      amount to finance
  yes            duration   Query            int 32     length of term in months
  yes            rate       Query            float      interest rate

```
  Once you have entered the values, the screen will look like this:

  ![](images/tutorial_html_2fc0008e5f75928e.png)

20. Set the schema for the response.
    Since we already defined
    the **[paymentAmount]** definition, select
    it from the drop down list
    for [[SCHEMA]], and use it for the [[200]] response code. 
    You will find
    the **[paymentAmount]** definition at the
    bottom of the list.
    For [[DESCRIPTION]] enter [[amount
    calculated
    successfully]]
    ![](images/tutorial_html_f51180a01dc389af.png)

21. Click [[Save]] to
    save the API definition.

 Map the API to a Service WSDL
====================================================================================

Import the legacy Financing SOAP service WSDL and map it to the RESTful
API definition.

 Attach a Service WSDL
-----------------------------------------------------------------------------------------------------------------------------------------

1.  Click the **[Target Services]** option
    in the left column menu palette from the **[financing
    1.0.0]** API Design screen

2.  Click **[Add]** to import the web
    service from the legacy financing service.

    ![](images/tutorial_html_ebb6419fc4fb979a.png)

3.  Download the [calculate.wsdl](https://github.ibm.com/americas-integration/cp4i-pot/blob/master/cp4i-labs/APIC-Labs/resources/calculate.wsdl) and then Click **[Browse]** to
    select [[calculate.wsdl]] located
    in where you downloaded it on your machine.

    ![](images/tutorial_html_e10ec45733dfce99.png)

    You will get a success message and the service included in the WSDL
    will be displayed.

    ![](images/tutorial_html_6a8444e050b87ad3.png)

5. Select **[financingService.]** Then click **[Save]**.

    Build the Financing API Assembly
----------------------------------------------------------------------------------------------------------------------------------------------------

1. Click [[Assemble]] to
    access the assembly editor.

    ![](images/tutorial_html_7ecdd003a7db2e23.png)

2. In the processing pipeline, mouse over
    the [[invoke]] policy
    and click
    the [[trashcan]] icon
    to delete it.

    ![](images/tutorial_html_d05e099dd7e132b4.png)

3. Scroll down to the bottom of the policy menu and drag and drop
    the **[financing]]** web service
    operations to processing pipeline.

    ![](images/tutorial_html_771de22ad92a31fb.png)

4. Now you are going to modify the input and output map policy for
    mapping your REST API into SOAP.

    ![](images/tutorial_html_4a933c8c317bbd97.png)

5. In order to consume a SOAP-based service from your REST-based API,
    you need to map the query parameter inputs that were previously defined
    as part of the GET /calculate operation to a SOAP payload. To do so,
    click the [[financing
    input]] map
    policy on our pipeline to open the map editor.

    [[Tip: Click on the stretch icon to make the editor window fill the
    screen.]]

6. Click on
    the [[pencil icon]] in
    the [[Input column]].

    ![](images/tutorial_html_9d82765fc8e50237.png)

7. Click [[Add parameters for operation\...]] and
    select the **[get /calculate]** operation.

    ![](images/tutorial_html_9dad0a59d5e53a96.png)

    The Map editor will automatically pull in the request parameters
    that you defined earlier.

8. Click **[Done]** to return to the map
    editor.

9. For each of the Input query parameters, map them to their
    respective SOAP Output elements.

    To map from an input field to an output field, click the circle next
    to the source element once, then click the circle next to the target
    element. A line will be drawn between the two, indicating a mapping from
    the source to the target.

![](images/tutorial_html_e18d417ab873efe0.png)
    
10. Click [[\`X\`]] in
    the map editor to return to the policy pipeline.

11. Click
    the [[financing: invoke]] node to
    open its editor.

12. The SOAP service URL has already been set for you during the
    service import when we create the API.

    ![](images/tutorial_html_8d30f4d88ab4c2bf.png)

13. Click [[\`X\`]] to
    return to the policy pipeline.

14. After the Financing Web Service is invoked, you need to map the
    SOAP response into a JSON object.

    You already defined the response object
    called [[paymentAmount]].
    To do the map, click the **[financing
    output]** (Note: this is the **last** node on the assembly line. Do not select financing: output parse node which is the second last node) map policy on the pipeline to
    open the map editor.

15. Click the [[pencil icon]] to set the output object schema.

16. Click the **[Add outputs for
    operation\...]** option and select
    the **[[get /calculate]]** operation.

17. Set the [[Content type]] configuration
    option
    to [[application/json]],
    and then
    click [[Done]] to
    return to the map editor.

    ![](images/tutorial_html_4e9aa0f663bd6c06.png)

18. Click the [[circle next to the paymentAmount source
    element]] once,
    then click the [[circle next to the target
    element]].
    A line will be drawn between the two, indicating a mapping from the
    source to the target.

    ![](images/tutorial_html_f2e452da44248e01.png)

19. Click [[\`X\`]] in
    the map editor to return to the policy pipeline.

20. Click [[Save]] the API definition.

21. Click **[Develop]** in the navigation
    menu to return to the list of APIs and Products in your system.

 Import Logistics API
===========================================================================

In this lab section, we will be adding a new API called logistics which
will provide helper services around calculating shipping rates and
locating nearby stores. Rather than require you to build the entire API
from scratch again, you will see how you can import and modify an
existing OpenAPI definition.

 Import the OpenAPI Definition
-------------------------------------------------------------------------------------------------------------------------------------------------

1.  Click **[Add]** and
    select **[API]**  

    ![](images/tutorial_html_44524c2a518bf56e.png)

2.  From the Create API wizard, select [[Import: Existing
    OpenAPI]].
    Then
    click [[Next]].  ![](images/tutorial_html_5515164592670a5f.png)

3.  You will need logistics.yaml file for this step. Fron another browser window download the file using this link
    [logistics.yaml](https://integrationsuperhero.github.io/techcon2020/APICDevJam/resources/logistics.yaml)

    Click \`**Browse**\` in the [[Import from
    file]] window, and select the downloaded logistics.yaml file.

    ![](images/tutorial_html_2ec43e484c5482b0.png)

4.  Click [[Next]] in
    the confirmation window.

5.  Click [[Next]] one
    more time **[[without selecting the option Activate
    API]]** since
    we still need to make some updates.

6.  Click [[Edit
    API]] in
    the [[Summary]] page
    to go to the API editor.

 Configure payload to be stored in Analytics
---------------------------------------------------------------------------------------------------------------------------------------------------------------

1.  From the API menu, select [[Activity
    Log]].
    In
    the [[Content]] drop-down,
    select [[payload]].
    A pop up window will be displayed, asking to enable buffering.
    Click [[Continue]].

    ![](images/tutorial_html_e8ffcd636704e49b.png)

2.  Set the [[Content on
    error]] drop-down
    to [[activity]].
    Click [[Save]].

    ![](images/tutorial_html_1b4e90745e45c224.png)

 Create an Orchestration Assembly
=======================================================================================

The logistics API provides resources for calculating shipping costs and
locating the nearest store for pickup. In this section, you will
configure the assembly for the shipping calculation resource. Your API
assembly will call out to two separate shipping vendors and provide a
consolidated response back to the consumer.

 Create the Logistics API Assembly
-----------------------------------------------------------------------------------------------------------------------------------------------------

1.  Switch to
    the [[Assemble]] tab
    and remove
    the [[invoke]] policy
    by hovering over it and selecting the [[trashcan
    icon]].

2.  Click and drag
    the [[Operation switch]] policy
    to flow pipeline in the right.

3.  The switch editor will open with a single case with case 0 created
    by default.

4.  Next to case 0, click **[search
    operations\...]** to show the drop-down
    list of available operations.

5.  Select
    the **[shipping.calc]** operation.

6.  Click the **[+ Case]** button to add a
    second case for
    the [[get.stores]] operation.

7.  Click **[X]** to close the operation
    switch configuration editor and then
    click [[Save]].
    You should see two new processing pipelines created on your
    \`operation-switch\` step - one for each case:

    ![](images/tutorial_html_2805ad613d2ba436.png)

 

 Configure the `shipping.calc` Case
--------------------------------------------------------------------------------------------------------------------------------------------------------

This operation will end up invoking two separate back-end services to
acquire shipping rates for the respective companies, then utilize a map
action to combine the two separate responses back into a single,
consolidated message for our consumers.

1.  Add an [[invoke
    policy]] to
    the [[shipping.calc case]].

2.  Edit the **[invoke]** action with the
    following properties:

    -   [[Title:
        invoke_xyz]]

    -   [[URL: $(shipping_svc_url)?company=xyz&from_zip=90210&to_zip=\{zip\}]]

    -   [[Stop on error: unchecked]]

    -   [[Response object variable (scroll to the bottom):
        xyz_response]]  ![](images/tutorial_html_8c4d5816115227c1.png)  
         ![](images/tutorial_html_3a71962c80162408.png)

    -   **[Note: The  parameter provided here is a reference to the
        zip parameter defined as input to the operation. The
        portion of the URL will get replaced by the actual zip code
        provided by the API consumers. ]**

3.  Hover over
    the [[invoke\_xyz policy]] and
    click [[clone]] to
    add another invoke action:  

    ![](images/tutorial_html_c099b7fb4e29d1ef.png)  

4.  Edit the new invoke policy with the following properties:

    -   [[Title:
        invoke\_cek]]

    -   [[URL:
        \$(shipping\_svc\_url)?company=cek&from\_zip=90210&to\_zip=\{zip\}]]
        
    -   [[Stop on error: unchecked]]
    
    -   [[Response object variable:
        cek\_response]]  

        ![](images/tutorial_html_84608c0a3a93f935.png)

        ![](images/tutorial_html_e4fed02337332021.png)

5.  Add
    a [[map policy]] after
    the last invoke and then click it to open the
    editor.  ![](images/tutorial_html_df80d082c629e3eb.png)  

6.  Click
    the [[pencil]] at
    the top of the Input column, then click on the [[Add
    input]] button.
    Enter the following input configuration:

    -   [[Context variable:
        xyz\_response.body]]

    -   [[Name:
        xyz]]

    -   [[Content type:
        application/json]]

    -   [[Definition:
        #/definitions/xyz_shipping_rsp]]

7.  Click the [[Add
    input]] button
    again to add another input. Specify the following input
    configuration:

    -   [[Context variable:
        cek_response.body]]

    -   [[Name:cek]]

    -   [[Content type:
        application/json]]

    -   [[Definition:
        #/definitions/cek_shipping_rsp]]

8.  You now have two inputs assigned to the
    map policy:  ![](images/tutorial_html_1cecd20554b4f15b.png)

9.  Click [[Done]] to
    return to the editor.

10. Click the [[pencil
    icon]] at
    the top of
    the [[Output]] column
    and then click [[Add outputs for
    operation\...]] and
    choose
    the [[shipping.calc]] operation.

11. Set **[Content
    type]** to [[application/json]].

12. Click [[Done]] to
    return to the editor.

13. Complete the mapping. To map from an input field to an output field,
    click the circle next to the source element once, then click the
    circle next to the target element. A line will be drawn between the
    two, indicating a mapping from the source to the
    target. ![](images/tutorial_html_c7529b39125204de.png)

14. Click **X** to close the map editor. Your assembly policy for the
    shipping.calc operation is now complete.

    ![](images/tutorial_html_60e39f1d04c62b0b.png)

15. Click **[[Save]]** button to save your changes.

 Use GatewayScript in an Assembly
=======================================================================================

In this section, you will configure the assembly for the store locator
resource. You will use GatewayScript to modify the response to your
consumers, providing them a maps link to the nearest store location.

 Configure the `get.stores` Case
-----------------------------------------------------------------------------------------------------------------------------------------------------

This operation will call out to the Google Geocode API to obtain
location information about the provided zip code, and will then utilize
a simple gatewayscript to modify the response and provide a formatted
Google Maps link.

1.  Add an invoke policy to
    the **[[get.stores]]** case.  
    
    ![](images/tutorial_html_8fcccda10f7fbc1e.png)

2.  Edit the
    new [[invoke action]] with
    the following properties:

    -   [[Title:
        invoke\_google\_geolocate  ]]

    -   [[URL:
        https://maps.googleapis.com/maps/api/geocode/json?&address=\{zip\}]]

    -   [[Stop on error:
        unchecked ]]

    -   [[Response object variable (scroll to the bottom):
        google\_geocode\_response]]  ![](images/tutorial_html_c230669eaa51ffee.png)  
          ![](images/tutorial_html_bcc946b43e8188.png)

3.  Click [[X]] to
    close the invoke editor.

4.  Add a [[gatewayscript]] policy to the **[[get.stores]]** flow with the following properties:

    -   **[Title:
        gws\_format\_maps\_link]**

    -   Copy the following GatewayScript snippet and paste it into the
        text area:

```
// Save the Google Geocode response body to variable
var mapsApiRsp = apim.getvariable('google_geocode_response.body');

// Get location attributes from geocode response body
var location = mapsApiRsp.results[0].geometry.location;

// Set up the response data object, concat the latitude and longitude
var rspObj = {"google_maps_link": "https://www.google.com/maps?q=" + location.lat + "," + location.lng};

// Save the output     
apim.setvariable('message.body', rspObj)

```

  ![](images/tutorial_html_d005e2f600ea91f1.png)

-   **[Note: Take a quick look at line 5. Notice how our gateway script
    file is reading the body portion of the google\_geocode\_response
    variable which was assigned to the output of the invoke
    action.]**

    Click [[X]] to
    close the gatewayscript editor.

    Your assembly for the \`logistics\` API will now include two separate
    operation policies. 

7.  **Save** your
    changes by clicking the **[[Save]]** button.

8.  Click [[Develop]] in
    the navigation menu to return to the list of APIs and Products in
    your system.

    ![](images/tutorial_html_a810481f55373ff0.png)

 Summary
==============================================================

Congratulations! You have successfully configured two new API's with
advanced assemblies. Throughout the tutorial, you explored the key
takeaways:

-   Create a new API, including object definitions and paths.

-   Configure an API to access an existing SOAP service.

-   Import an existing API from an OpenAPI definition document (a.k.a
    Swagger).

-   Map data retrieved from multiple API calls into an aggregate
    response.

-   Use GatewayScript directly within an API assembly.

Continue with the APIC Labs. Go
to [APIC Lab 6 - Working with API Products](https://github.ibm.com/americas-integration/cp4i-pot/tree/master/cp4i-labs/APIC-Labs/Lab6) to
learn about bundling the API's into a Product and publishing it to the consumer portal.

**APIC Lab 8 -- Creating GraphQL Proxy API**

In this lab, you will explore the how to define GraphQL APIs that proxy
to a backend GraphQL server. GraphQL is a query language for APIs that
gives an application client greater control over what data it retrieves
in an API request when compared with a REST API request.

API Connect GraphQL support also allows rate limiting and other controls
using API Gateway.

In this tutorial, you will explore the following key capabilities:

-   Create a GraphQL Proxy API

-   Learn about GraphQL introspection and Schema Editor

-   Test APIs by using the built-in GraphQL editor

-   Review API Assembly Policies for the cost end point

[Return to main API lab page](../index.md)

Prerequisites: None

 Create a GraphQL Proxy API
=================================================================================

1.  Select Develop API and click Add-\>API

    ![](images/tutorial_html_c0c5acec16e566bb.png)

2.  Enter the following values and click Next. You To create a GraphQL
    proxy definition, select From Existing GraphQL service. When you
    point to an existing GraphQL server, API Connect introspects the
    service and automatically creates a GraphQL proxy service.

    ![](images/tutorial_html_797b2f887d77017c.png)

3.  Enter the following values and click Next. You can use default
    values for the rest.

    Title: accounts

    GraphQL server URL: https://graphql-test-server.us-east.cf.appdomain.cloud/accounts/graphql

    ![](images/tutorial_html_f83e60ae96763438.png)

    ![](images/tutorial_html_90e0cbad29eca5a.png)

4.  The schema validator reports warning and errors if found. There are two
    warnings in the accounts schema imported from the server. You can
    review the schema warning details.

    ![](images/tutorial_html_3cc23a786c4f73c2.png)

5.  A review of the schema shows that no limit is set on the size of the
    two fields. You will fix these warnings in later steps. Click Next to
    continue.

    ![](images/tutorial_html_8104c10fce21e609.png)

6.  Keep both Secure Client ID and CORS checked and click Next

    ![](images/tutorial_html_464f81f24c7d47dd.png)

7.  API Connect successfully created a GraphQL proxy API. You can edit
    the API to view more details on the proxy API just created. Click
    EDIT API to continue.

    ![](images/tutorial_html_e70bb58508f9b662.png)

8.  GraphQL APIs are structured the same as REST APIs with some
    additional options. Just like REST APIs, you will be able to add
    security definitions, properties and Activity logs from the left
    menu bar. You can also view the Source and Assemble tabs similar to
    REST APIs. You will notice a new tab for GraphQL APIs. Click on
    GraphQL Schema tab to view the schema.

    ![](images/tutorial_html_b27d147e1a49276b.png)

9.  GraphQL Schema editor displays Type and Weight information. The
    weighting factor is used when calculating the type cost for a
    request to the GraphQL API. For example, a field that requires
    extensive CPU or memory use on the server to retrieve its value
    would be given a higher cost.

    ![](images/tutorial_html_ab0c11b157a7cd4b.png)

10. Select one of the warning sign to review the warning details. In
    addition to the warning details, the Warning window gives an option
    to fix the warning by apply the limits. Click **[[Apply all]]** and then **[[Apply]]**.

    ![](images/tutorial_html_ed0f88002c9eb816.png)

11. After applyting the recommendation the wanrning message is removed.
    Click Save to save the API definition .

    ![](images/tutorial_html_63ce76efdb0032d7.png)

12. Select Assemble to view the API in Assembly view. The flow is
    automatically created as part of the initial API creation. You may
    apply addition logic by dragging and dropping items from the pallet
    to the canvas. In this tutorial, you are not adding additional
    logic.

    ![](images/tutorial_html_a2cd4daada4f2ca5.png)

13. To publish the API toggle the button from offline to online.

    ![](images/tutorial_html_965b91d211caf432.png)

14. After successfully publishing the API to API Gateway, additional
    tabs appear on the screen. Select Test tab to test the API.

15. Select **[[GET https://apic-min-gw-gateway-cp4i-apic.apps.cody.coc-ibm.com/cody8/sandbox/accounts/graphql]]** from the    drop down list (Note: you URL will be different, but /sandbox/accounts/graphql should be the same)

    ![](images/tutorial_html_ccb982e24326f44f.png)
   
    Click **Send** to test the API.

    A parse error is returned since we have not specified query string yet.

16. API Connect Test feature also includes GraphQL Editor. Enter the
    following in in GraphQL Editor window. You may use Prettify option
    to view formatting string.

```
{
  accounts(limit: 2) {
    name {
      first
      last
    }
  }
}
```

17. Click **[[Run]]** button to send the GraphQL request to the end point. 
    
    ![](images/tutorial_html_98d8f253e934k8j9.png)

18. An exception window may appear when you use test the API for the first
    time.Click accept Exception to continue.

    ![](images/tutorial_html_98d8f253e9342c8b.png)

    You may see an invalid certificate issue page when you continue. This is
    because valid certificates are not applied in this test environment. If
    you are using Chrome browser you can accept the exception by typing
    "thisisunsafe" anywhere in the window. Similar workarounds are available
    for other browsers. For firefox browser, follow the steps from here -
    <https://support.mozilla.org/en-US/kb/error-codes-secure-websites>

    ![](images/tutorial_html_ac0c773416db4db7.png)

19. The results for GraphQL request are displayed on the right panel. In
    the request we limited the values to 2, so only two accounts are
    displayed. Change the value to 5 and submit the request again and
    notice that more accounts are returned in the results window.

    ![](images/tutorial_html_1d05935575c71f8e.png)

20. You can request additional data fields (refer to the schema editor
    for details), GraphQL may reject if certain fields are locked or
    prohibited. To test this, enter CreditCard information in the
    request field and click the **"Play"** button

    The complete request looks as follows:
```
{
  accounts(limit: 2) {
    name {
      first
      last
    }
    shippingAddress {
      building
      street
    }
  }
  creditCard {
    number
    expirationDate
  }
}
```

  You will notice that an error message is displayed in the results window
  instead of the account values as the server restricts the query field
  creditCard.

  (Note: The error message displayed may be different than what is shown
    in the screenshot).

  ![](images/tutorial_html_81c927163c9c11bb.png)

21. Submit another request to get account and shipping address details by adding the **state** and **zip** fields.
    This time the values are turned without errors.

    ![](images/tutorial_html_e37331678c3d02b2.png)

 Create a Product and apply GraphQL RateLimits
====================================================================================================

1.  To create a product Select **[[Develop]]** from left menu bar and click
    Add-\>Product

    ![](images/tutorial_html_4f43bda35452bd65.png)

2.  Select **New Product** and name the product as Accounts Product and click Next

    ![](images/tutorial_html_d0c3992a4bd7bc24.png)

3.  Add Accounts API to the product by selecting accounts. Click Next and accept default values to
    continue to create the accounts-product.

    ![](images/tutorial_html_4ae09f5fddd82bab.png)

4.  Once the accounts-product is created, edit the product accounts-product to review the details. The Default
    Plan contains traditional rate limiting options but you will notice
    another section that list GraphQL Rate Limits.

    ![](images/tutorial_html_15d9c2582155eea8.png)

5.  You will be able to adjust GraphQL cost parameters from this
    section. You can set a limit or make it unlimited. You will not be
    making any changes in this tutorial.

    ![](images/tutorial_html_3c25f5d5dab1988e.png)

6.  Publish the Product to Sandbox Catalog by selecting Publish

    ![](images/tutorial_html_a1f1cf7707e31913.png)

7.  Click Publish to complete publishing the product.

    ![](images/tutorial_html_890ebcd8219b104.png)

 Test GraphQL API from Developer Portal
=============================================================================================

1.  Sign in to API Connect Developer Portal using the Developer Portal
    URL, username and password provided by the instructor.

    ![](images/tutorial_html_540cbe0b9202f4a7.png)

    ![](images/tutorial_html_c34973eb377015ce.png)

2.  Click **API Products**, and select **Accounts Product**.

    ![](images/tutorial_html_2635d049f12d59c6.png)

3.  The selected product lists one API (accounts api) and one plan
    (Default Plan). Click Subscribe button to subscribe to the plan.

    ![](images/tutorial_html_bd0ea34d4f40d756.png)

4.  The Plan subscription requires an application. You can create a new
    application or select the IBM Consumer application that is already
    created.

    ![](images/tutorial_html_2fd3cf48168675e5.png)

5.  Complete application subscription and select accounts API to review and test the API. Click accounts to
    continue

    ![](images/tutorial_html_8a5975dd9780a924.png)

6.  Developer Portal displays the type as GrahQL API. Currently Client
    ID security is enforced. Since there is only on Plan and one
    Consumer Application, the Consumer ID filed is already populated.

    ![](images/tutorial_html_e8892b4b3da410fc.png)

7.  To continue to test the API, click **Try it** and use the GraphQL Editor for your query input. Submit requests
    using the **Play** button with different field names and watch how quickly the results are
    returned in the results window. If this was a REST API multiple end
    points will be needed to achieve the same result.
    
```
{
  accounts(limit: 2) {
    name {
      first
      last
    }
    shippingAddress {
      building
      street
    }
  }
}
```

   ![](images/tutorial_html_9575e27d8184b8fc.png)

Summary
=================================================================================================================

Congratulations! You have successfully created a GraphQL Proxy API,
published the API as part of a Product, applied controls and rate
limits, and tested using Developer Portal.

To learn more about Cloud Pak for Integration and API Life Cycle
Management, visit <https://www.ibm.com/cloud/cloud-pak-for-integration>

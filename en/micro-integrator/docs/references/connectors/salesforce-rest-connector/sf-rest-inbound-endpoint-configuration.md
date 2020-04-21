# Setting up the PushTopic in Salesforce

This documentation explains how to set up the Salesforce environment to connect with WSO2 Salesforce Inbound Endpoint. Please follow up the steps given below

* How to Creating a custom object or object in Salesforce.
* Create a PushTopic.
* Subscribe to the created PushTopic Channel.
* Test the PushTopic Channel.
 
## Creating a custom object/object

As first step you need to, [create a custom object in Salesforce](https://developer.salesforce.com/docs/atlas.en-us.202.0.api_streaming.meta/api_streaming/create_object.htm). In this scenario we simply using `Account` object for store the records.
 
## Create a PushTopic  

The [PushTopic](https://developer.salesforce.com/docs/atlas.en-us.202.0.api_streaming.meta/api_streaming/create_a_pushtopic.htm) record that contains a SOQL query. Event notifications are generated for updates that match the query. Alternatively, you can also use Workbench to create a PushTopic. In this sample we using salesforce Developer Console to create a Push Topic.

1. **Login** to the **Salesforce Account**. Navigate to the top right corner of the **Home page** and click **Setup** icon. Then select **Developer Console**.

   <img src="../../../../assets/img/connectors/open-the-developer-console.png" title="Open the Developer Console." width="800" alt="Open the Developer Console."/>

2. After populate the Developer console click **Debug** -> Open **Execute Anonymous Window**.   
   
   <img src="../../../../assets/img/connectors/salesforce-inboundEP-execute-anonymous-window.png" title="Open the Anonymous Window." width="800" alt="Open the Anonymous Window."/>
   
3. Then, add the following entry in the **Enter Apex Code** window and Click **Execute**.   
   
   <img src="../../../../assets/img/connectors/salesforce-inboundEP-enter-apex-code.png" title="Enter Apex code." width="800" alt="Enter Apex code."/> 
   
   ```
   PushTopic pushTopic = new PushTopic();
   pushTopic.Name = 'Account';
   pushTopic.Query = 'SELECT Id, Name FROM Account';
   pushTopic.ApiVersion = 37.0;
   pushTopic.NotifyForOperationCreate = true;
   pushTopic.NotifyForOperationUpdate = true;
   pushTopic.NotifyForOperationUndelete = true;
   pushTopic.NotifyForOperationDelete = true;
   pushTopic.NotifyForFields = 'Referenced';
   insert pushTopic;
   ```
   We are essentially creating a SOQL query with a few extra parameters the watch for changes in a specified object. If the Push Topic is executed successfully then Salesforce is ready to post notification to WSO2 Salesforce Inbound Endpoint, if any changes made in the Account object in Salesforce, because the below Push Topic has been created for Salesforce's Account object. 
   
## Subscribe to the PushTopic Channel

In this step, we need to [subscribe](https://developer.salesforce.com/docs/atlas.en-us.202.0.api_streaming.meta/api_streaming/subscribe_to_pushtopic_channel.htm) to the channel that we created with the PushTopic record in the previous step. For this can be done through the `Workbench`. Workbench is a free, open source, community-supported tool which helps administrators and developers to interact with Salesforce for Data Insert, Update, Upsert, Delete and Export purposes. 

> **Note**: Salesforce provides a hosted instance of Workbench for demonstration purposes only—Salesforce recommends that you do not use this hosted instance of Workbench to access data in a production database.

1. Using your browser, navigate to the [workbench](https://developer.salesforce.com/page/Workbench).

   <img src="../../../../assets/img/connectors/salesforce-inboundEP-slaesforce-login-workbench.png" title="Login Workbench." width="800" alt="Login Workbench."/> 

2. Select **Environment** as **Production** and **API Version** as **37.0**.
   
   <img src="../../../../assets/img/connectors/salesforce-inboundEP-select-environment.png" title="Select Environment." width="800" alt="Select Environment."/>

3. **Accept the terms of service**, and click **Login with Salesforce**.

4. After login with Salesforce you will be establish a connection to your database, and land on the **Select page**.

   <img src="../../../../assets/img/connectors/salesforce-inboundEP-landing-page.png" title="Select page." width="800" alt="Select page."/>

5. Select **queries** -> **Streaming Push Topics**.

   <img src="../../../../assets/img/connectors/salesforce-inboundEP-streaming-push-topics.png" title="Streaming PushTopic." width="800" alt="Streaming PushTopic."/>
   
6. In the **Push Topic** field, select **Account**.   
  
   <img src="../../../../assets/img/connectors/salesforce-inboundEP-select-pushtopic-Account.png" title="Select created PushTopic." width="800" alt="Select created PushTopic."/>

7. Click **Subscribe**. You’ll see the connection and response information and a response like `Subscribed to /topic/Account`.

   <img src="../../../../assets/img/connectors/salesforce-inboundEP-subscribe.png" title="Subscribe to the PushTopic." width="800" alt="Subscribe to the PushTopic."/>
   
   > **Note**: Keep this browser window open and make sure that the connection does not time out. You’ll be able to see the event notifications triggered by the Account record you create in the testing the PushTopic channel.
   
## Test the PushTopic Channel.

1. Open new browser window and navigate to the [workbench](https://developer.salesforce.com/page/Workbench) using the same username and password. Please follow the steps  given in `Subscribe to the PushTopic Channel` `Step 1`.

2. Select **data** -> **Insert**.

   <img src="../../../../assets/img/connectors/salesforce-inboundEP-data-insert.png" title="Insert data to test the PushTopic." width="800" alt="Insert data to test the PudhTopic."/>

3. For **Object Type**, select *Account*. Ensure that the **Single Record** field is selected, and click **Next**. 
   
   <img src="../../../../assets/img/connectors/salesforce-inboundEP-select-single-record.png" title="Select single record." width="800" alt="Select single record."/>
   
4. Type in a value for the `Name` field.Then click **Confirm Insert**.
  
   <img src="../../../../assets/img/connectors/salesforce-inboundEP-insert-values-to-Name.png" title="Insert value to the object." width="800" alt="Insert value to the object."/>

5. Switch to your **Streaming Push Topics** browser window. You’ll see a notification that the *Account* update was created. The notification returns the `Id` and `Name` fields that we defined in the SELECT statement of our **PushTopic query**. Please find the notification message as shown bellow.
   
   ```
   Message received from: /topic/Account
   {
     "data": {
       "event": {
         "createdDate": "2020-04-21T13:02:56.967Z",
         "replayId": 11,
         "type": "created"
       },
       "sobject": {
         "Id": "0012x0000048qhUAAQ",
         "Name": "Doctor"
       }
     },
     "channel": "/topic/Account"
   }
   ```
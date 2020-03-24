# FHIR Connector Example

Given below is a sample scenario that demonstrates how to work with resources in [FHIR](https://www.hl7.org/fhir/overview.html)(Fast Healthcare Interoperability Resources). FHIR specification is a standard for exchanging health care information electronically.The WSO2 EI FHIR connector uses the FHIR RESTFul API to interact with FHIR.

## What you'll build

Given below is a sample API that illustrates how you can connect to a FHIR with the `init` operation and then use the `create`,`readResource`, `readSpecificResourceById`,`delete` and `update` operation to send messages to the FHIR server.

**init**
````xml
<fhir.init>
    <base>{$ctx:base}</base>
<fhir.init>
````
**Properties**

| Property        | Description |
| ------------- |-------------|
| base    | The [Service Root URL](http://hapi.fhir.org/baseR4). |

**create**
````xml
<fhir.create>
    <base>{$ctx:base}</base>
    <type>{$ctx:type}</type>
    <format>{$ctx:format}</format>
 </fhir.create>
````
**Properties**

| Property        | Description |
| ------------- |-------------|
| base    | The Service Root URL. |
| type    | The name of a resource type (e.g. "Patient").|
| format  | The [Mime Type](http://www.hl7.org/implement/standards/fhir/http.html#mime-type).|

**readResource**
````xml
<fhir.readResource>
     <base>{$ctx:base}</base>
     <type>{$ctx:type}</type>
     <format>{$ctx:format}</format>
</fhir.readResource>
````
**Properties**

| Property        | Description |
| ------------- |-------------|
| base    | The Service Root URL |
| type    | The name of a resource type (e.g. "Patient").|
| format  | The Mime Type.|

**readSpecificResourceById**
````xml
<fhir.readSpecificResourceById>
     <base>{$ctx:base}</base>
     <type>{$ctx:type}</type>
     <id>{$ctx:id}</id>
     <format>{$ctx:format}</format>
     <summary>{$ctx:summary}</summary> 
 </fhir.readSpecificResourceById>
````
**Properties**

| Property        | Description |
| ------------- |-------------|
| base    | The Service Root URL |
| type    | The name of a resource type (e.g. "Patient").|
| format  | The Mime Type.|
| id      | The possible values for the logical Id.|
|summary|The search parameter _summary can be used when reading a resource. It can have the values true, false, text & data.|

**delete**
````xml
<fhir.delete>
    <base>{$ctx:base}</base>
    <type>{$ctx:type}</type>
    <idToDelete>{$ctx:idToDelete}</idToDelete>
 </fhir.delete>
````
**Properties**

| Property        | Description |
| ------------- |-------------|
| base    | The Service Root URL |
| type    | The name of a resource type (e.g. "Patient").|
| idToDelete | The id of the resource.|

**update**
````xml
<fhir.update>
    <base>{$ctx:base}</base>
    <type>{$ctx:type}</type>
    <idToUpdate>{$ctx:idToUpdate}</idToUpdate>
    <format>{$ctx:format}</format>
</fhir.update>
````
**Properties**

| Property        | Description |
| ------------- |-------------|
| base    | The Service Root URL |
| type    | The name of a resource type (e.g. "Patient").|
| idToUpdate | The element of a particular resource.|

> **Note**:If no id element is provided, or the value is wrong, the server SHALL respond with a HTTP 400 error code, and SHOULD provide an operation outcome identifying the issue.

The following diagram illustrates all the required functionality of the FHIR API service that you are going to build.

<img src="/assets/img/connectors/FHIRConnector.png" title="FHIR Connector" width="800" alt="FHIR Connector"/>

## Configure the connector in WSO2 Integration Studio

Follow these steps to set up the ESB Solution Project and the Connector Exporter Project.

{!references/connectors/importing-connector-to-integration-studio.md!}

1. Our project would look similar to the following (source view).

    ```
   <?xml version="1.0" encoding="UTF-8"?>
   <api context="/resources" name="SampleApi" xmlns="http://ws.apache.org/ns/synapse">
       <resource methods="POST" url-mapping="/create">
           <inSequence>
               <property expression="json-eval($.base)" name="base" scope="default" type="STRING"/>
               <property expression="json-eval($.resourceType)" name="type" scope="default" type="STRING"/>
               <property expression="json-eval($.format)" name="format" scope="default" type="STRING"/>
               <fhir.init>
                   <base>{$ctx:base}</base>
               </fhir.init>
               <fhir.create>
                   <type>{$ctx:type}</type>
                   <format>{$ctx:format}</format>
               </fhir.create>
               <log level="full" separator=","/>
               <send/>
           </inSequence>
           <outSequence/>
           <faultSequence/>
       </resource>
       <resource methods="POST" url-mapping="/read">
           <inSequence>
               <property expression="json-eval($.base)" name="base" scope="default" type="STRING"/>
               <property expression="json-eval($.resourceType)" name="type" scope="default" type="STRING"/>
               <property expression="json-eval($.format)" name="format" scope="default" type="STRING"/>
               <fhir.init>
                   <base>{$ctx:base}</base>
               </fhir.init>
               <fhir.readResource>
                   <type>{$ctx:type}</type>
                   <format>{$ctx:format}</format>
               </fhir.readResource>
               <log level="full" separator=","/>
               <send/>
           </inSequence>
           <outSequence/>
           <faultSequence/>
       </resource>
       <resource methods="POST" url-mapping="/readSpecificResourceById">
           <inSequence>
               <property expression="json-eval($.base)" name="base" scope="default" type="STRING"/>
               <property expression="json-eval($.resourceType)" name="type" scope="default" type="STRING"/>
               <property expression="json-eval($.format)" name="format" scope="default" type="STRING"/>
               <property expression="json-eval($.id)" name="id" scope="default" type="STRING"/>
               <property expression="json-eval($.summary)" name="summary" scope="default" type="STRING"/>
               <fhir.init>
                   <base>{$ctx:base}</base>
               </fhir.init>
               <fhir.readSpecificResourceById>
                   <type>{$ctx:type}</type>
                   <id>{$ctx:id}</id>
                   <format>{$ctx:format}</format>
                   <summary>{$ctx:summary}</summary>
               </fhir.readSpecificResourceById>
               <log level="full" separator=","/>
               <send/>
           </inSequence>
           <outSequence/>
           <faultSequence/>
       </resource>
       <resource methods="POST" url-mapping="/delete">
           <inSequence>
               <property expression="json-eval($.base)" name="base" scope="default" type="STRING"/>
               <property expression="json-eval($.resourceType)" name="type" scope="default" type="STRING"/>
               <property expression="json-eval($.format)" name="format" scope="default" type="STRING"/>
               <property expression="json-eval($.idToDelete)" name="idToDelete" scope="default" type="STRING"/>
               <fhir.init>
                   <base>{$ctx:base}</base>
               </fhir.init>
               <fhir.delete>
                   <type>{$ctx:type}</type>
                   <idToDelete>{$ctx:idToDelete}</idToDelete>
               </fhir.delete>
               <log level="full" separator=","/>
               <send/>
           </inSequence>
           <outSequence/>
           <faultSequence/>
       </resource>
       <resource methods="POST" url-mapping="/update">
           <inSequence>
               <property expression="json-eval($.base)" name="base" scope="default" type="STRING"/>
               <property expression="json-eval($.resourceType)" name="type" scope="default" type="STRING"/>
               <property expression="json-eval($.format)" name="format" scope="default" type="STRING"/>
               <property expression="json-eval($.idToUpdate)" name="idToDelete" scope="default" type="STRING"/>
               <fhir.init>
                   <base>{$ctx:base}</base>
               </fhir.init>
               <fhir.update>
                   <type>{$ctx:type}</type>
                   <idToUpdate>{$ctx:idToUpdate}</idToUpdate>
                   <format>{$ctx:format}</format>
               </fhir.update>
               <log level="full" separator=","/>
               <send/>
           </inSequence>
           <outSequence/>
           <faultSequence/>
       </resource>
   </api>

    ```
2. Right-click on the Composite Application Project and click on **Export Project Artifacts and Run**. Select **Run on Micro Integrator**.

3. Micro Integrator will be started and the composite application will be deployed. You can further refer to the application deployed through the CLI tool. Make sure you first export the PATH as below.

    ```
    $ export PATH=/path/to/mi/cli/directory/bin:$PATH\
    ```

{! /references/connectors/exporting-artifacts.md !}

## Deployment
Follow these steps to deploy the exported CApp in the Enterprise Integrator Runtime. 

{!references/connectors/deploy-capp.md!}
    
## Testing

1. Login in to the Micro Integrator CLI tool.

   ```
   ./mi remote login
   ```
2. Provide default credentials admin for both username and password.

3. In order to view the proxy services deployed, execute the following command.

   ```
   ./mi api show
   ```
4. Invoke deployed API resources using a CURL command or sample client.
   
   ### create resource
   
   Sample request for create operation.
   
   ```
   curl -v POST -d 
   '{
      "base": "http://hapi.fhir.org/baseR4",
      "resourceType": "Patient",
      "format": "json",
      "name": [{"family": "Jhone","given": ["Winney","Rodrigo"]}]
   }' "http://localhost:8290/resources/create" -H "Content-Type:application/json" 
       
   ```
   See the following response message content:
      
   ```
   <jsonObject>
       <resourceType>Patient</resourceType>
       <id>698021</id>
        <meta>
          <versionId>1</versionId>
          <lastUpdated>2020-03-24T07:57:14.506+00:00</lastUpdated>
        </meta>
         <text>
           <status>generated</status>
           <div>&lt;div xmlns="http://www.w3.org/1999/xhtml"&gt;&lt;div class="hapiHeaderText"&gt;Winney Rodrigo &lt;b&gt;JHONE &lt;/b&gt;&lt;/div&gt;&lt;table class="hapiPropertyTable"&gt;&lt;tbody/&gt;&lt;/table&gt;&lt;/div&gt;</div>
         </text>
         <name>
            <family>Jhone</family>
            <given>Winney</given>
            <given>Rodrigo</given>
        </name>
   </jsonObject>
   ```  
           
   ### readResource resource
   
   Sample Request for readResource operation :
   
   ```
   curl -v POST -d 
   '{
       "base":"http://hapi.fhir.org/baseR4",
       "resourceType":"Patient",
       "format":"json"
   }' "http://localhost:8290/resources/read" -H "Content-Type:application/json"        
   ```
   It will retrieve all the resources exists in the FHIR server.
  
   ### readSpecificResourceById resource
   
   Sample Request for readSpecificResourceById operation :
      
   ```
   curl -v POST -d 
   '{
       "base":"http://hapi.fhir.org/baseR4",
       "resourceType":"Patient",
       "id":"698022",
       "format":"json"
   }' "http://localhost:8290/resources/readSpecificResourceById" -H "Content-Type:application/json"            
   ```         
   See the following response message content:
      
   ```
   <jsonObject>
          <resourceType>Patient</resourceType>
             <id>698021</id>
              <meta>
              <versionId>1</versionId>
              <lastUpdated>2020-03-24T07:57:14.506+00:00</lastUpdated>
              </meta>
              <text>
                 <status>generated</status>
                 <div>&lt;div xmlns="http://www.w3.org/1999/xhtml"&gt;&lt;div class="hapiHeaderText"&gt;Winney Rodrigo &lt;b&gt;JHONE &lt;/b&gt;&lt;/div&gt;&lt;table class="hapiPropertyTable"&gt;&lt;tbody/&gt;&lt;/table&gt;&lt;/div&gt;</div>
              </text>
               <name>
                  <family>Jhone</family>
                  <given>Winney</given>
                  <given>Rodrigo</given>
               </name>
   </jsonObject>
   ```
   ### delete resource
    
   Sample Request for delete operation :
  
   ```
   curl -v POST -d 
   '{
      "base":"http://hapi.fhir.org/baseR4",
      "resourceType":"Patient",
      "idToDelete":"698022",
      "format":"json"
    }' "http://localhost:8290/resources/delete" -H "Content-Type:application/json" 
   ```
   
   See the following response message content:
   
   ```<jsonObject>
         <resourceType>OperationOutcome</resourceType>
         <text>
            <status>generated</status>
            <div>&lt;div xmlns="http://www.w3.org/1999/xhtml"&gt;&lt;h1&gt;Operation Outcome&lt;/h1&gt;&lt;table border="0"&gt;&lt;tr&gt;&lt;td style="font-weight: bold;"&gt;INFORMATION&lt;/td&gt;&lt;td&gt;[]&lt;/td&gt;&lt;td&gt;&lt;pre&gt;Successfully deleted 1 resource(s) in 46ms&lt;/pre&gt;&lt;/td&gt;
                   					
                   				
                   			&lt;/tr&gt;
                   		&lt;/table&gt;
                   	&lt;/div&gt;</div>
         </text>
         <issue>
            <severity>information</severity>
            <code>informational</code>
            <diagnostics>Successfully deleted 1 resource(s) in 46ms</diagnostics>
         </issue>
      </jsonObject>
      ```
     
   ### update resource
   
   Sample Request for update operation :
   
   ```
      curl -v POST -d 
         '{
             "base":"http://hapi.fhir.org/baseR4",
             "resourceType":"Patient",
             "idToUpdate":"597079",
             "format":"json",
             "name":[
                {
                   "family":"Marry",
                   "given":[
                      "Samsong",
                      "Perera"
                   ]
                }
             ]
          }' "http://localhost:8290/resources/update" -H "Content-Type:application/json"   
   ```
   See the following response message content:  
   
   ```
   <jsonObject>
         <resourceType>Patient</resourceType>
         <id>698021</id>
         <meta>
            <versionId>1</versionId>
            <lastUpdated>2020-03-24T07:57:14.506+00:00</lastUpdated>
         </meta>
         <text>
            <status>generated</status>
            <div>&lt;div xmlns="http://www.w3.org/1999/xhtml"&gt;&lt;div class="hapiHeaderText"&gt;Winney Rodrigo &lt;b&gt;JHONE &lt;/b&gt;&lt;/div&gt;&lt;table class="hapiPropertyTable"&gt;&lt;tbody/&gt;&lt;/table&gt;&lt;/div&gt;</div>
         </text>
         <name>
            <family>Marry</family>
            <given>Samsong</given>
            <given>Perera</given>
         </name>
      </jsonObject>
      ```      
This demonstrates how the WSO2 EI FHIR connector works.
   
## What's next

* You can deploy and run your project on [Docker](../../../setup/installation/run_in_docker.md) or [Kubernetes](../../../setup/installation/run_in_kubernetes.md).
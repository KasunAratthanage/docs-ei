!!! note
    **This page is still a work in progress!**

# Business Rules APIs

## Listing the available business rule instances

### Overview

<table>
<tbody>
<tr class="odd">
<th>Description</th>
<td>Returns the list of business rule instances that are currently available.</td>
</tr>
<tr class="even">
<th>API Context</th>
<td><code>/business-rules/instances</code></td>
</tr>
<tr class="odd">
<th>HTTP Method</th>
<td><code>GET</code></td>
</tr>
<tr class="even">
<th>Request/Response Format</th>
<td><br />
</td>
</tr>
<tr class="odd">
<th>Authentication</th>
<td>Basic</td>
</tr>
<tr class="even">
<th>Username</th>
<td><code>admin</code></td>
</tr>
<tr class="odd">
<th>Password</th>
<td><code>admin</code></td>
</tr>
<tr class="even">
<th>Runtime</th>
<td>tooling</td>
</tr>
</tbody>
</table>

### curl command syntax

``` java
curl -X GET "https://<HOST_NAME>:<PORT>/business-rules/instances" -u admin:admin -k
```

### Sample curl command

``` java
curl -X GET "https://localhost:9643/business-rules/instances" -u admin:admin -k
```

### Sample output

``` java
```

### Response

<table>
<tbody>
<tr class="odd">
<th>HTTP Status Code</th>
<td><p>200 or 404</p>
<p>For descriptions of the HTTP status codes, see <a href="https://ei.docs.wso2.com/en/latest/streaming-integrator/ref/hTTP-Status-Codes/">HTTP Status Codes</a>.</p></td>
</tr>
</tbody>
</table>

## Delete business rule with given UUID

### Overview

<table>
<tbody>
<tr class="odd">
<th>Description</th>
<td>Deletes the business rule with the given UUID. </td>
</tr>
<tr class="even">
<th>API Context</th>
<td><code>/business-rules/instances/{businessRuleInstanceID}?force-delete=false</code></td>
</tr>
<tr class="odd">
<th>HTTP Method</th>
<td><code>DELETE</code></td>
</tr>
<tr class="even">
<th>Request/Response Format</th>
<td>application/json</td>
</tr>
<tr class="odd">
<th>Authentication</th>
<td>Basic</td>
</tr>
<tr class="even">
<th>Username</th>
<td><code>admin</code></td>
</tr>
<tr class="odd">
<th>Password</th>
<td><code>admin</code></td>
</tr>
<tr class="even">
<th>Runtime</th>
<td>tooling</td>
</tr>
</tbody>
</table>

#### Parameter Description

| Parameter                | Description                                                                      |
|--------------------------|----------------------------------------------------------------------------------|
|`{businessRuleInstanceID}`| The UUID (Uniquely Identifiable ID) of the business rules instance to be deleted.|                                                                                     |

### curl command syntax

``` java
curl -X DELETE "https://<HOST_NAME>:<PORT>/business-rules/instances/business-rule-1?force-delete=false" -H "accept: application/json" -u admin:admin
```

### Sample curl command

``` java
curl -X DELETE "https://localhost:9643/business-rules/instances/business-rule-1?force-delete=false" -H "accept: application/json" -u admin:admin
```

### Sample output

``` java

```

### Response

<table>
<tbody>
<tr class="odd">
<th>HTTP Status Code</th>
<td><p>200 or 404</p>
<p>For descriptions of the HTTP status codes, see <a href="https://ei.docs.wso2.com/en/latest/streaming-integrator/ref/hTTP-Status-Codes/">HTTP Status Codes</a> .</p></td>
</tr>
</tbody>
</table>

## Fetch template group with the given UUID

### Overview

<table>
<tbody>
<tr class="odd">
<th>Description</th>
<td>Returns the template group that has the given UUID.</td>
</tr>
<tr class="even">
<th>API Context</th>
<td><code>/business-rules/template-groups/{templateGroupID}</code></td>
</tr>
<tr class="odd">
<th>HTTP Method</th>
<td><code>GET</code></td>
</tr>
<tr class="even">
<td>Request/Response Format</td>
<td>application/json
</td>
</tr>
<tr class="odd">
<td>Authentication</td>
<td>Basic</td>
</tr>
<tr class="even">
<td>Username</td>
<td><code>admin</code></td>
</tr>
<tr class="odd">
<td>Password</td>
<td><code>admin</code></td>
</tr>
<tr class="even">
<td>Runtime</td>
<td>tooling</td>
</tr>
</tbody>
</table>

#### Parameter description

| Parameter           | Description                                   |
|---------------------|-----------------------------------------------|
| `{templateGroupID}` | The UUID of the template group to be fetched. |

### curl command syntax

``` java
curl -X GET "https://<HOST_NAME>:<PORT>/business-rules/template-groups/{templateGroupID}" -u admin:admin -k
```  

### Sample curl command

``` java
curl -X GET "https://localhost:9643/business-rules/template-groups/sweet-factory" -u admin:admin -k
```

### Sample output

``` java
```

### Response

<table>
<tbody>
<tr class="odd">
<th>HTTP Status Code</th>
<td><p>200 or 404</p>
<p>For descriptions of the HTTP status codes, see <a href="https://ei.docs.wso2.com/en/latest/streaming-integrator/ref/hTTP-Status-Codes/">HTTP Status Codes</a> .</p></td>
</tr>
</tbody>
</table>

## Fetch rule templates of the template group with given UUID

### Overview

<table>
<tbody>
<tr class="odd">
<th>Description</th>
<td>Returns the rule templates of the template group with the given UUID.</td>
</tr>
<tr class="even">
<th>API Context</th>
<td><code>/business-rules/template-groups/{templateGroupID}/templates</code></td>
</tr>
<tr class="odd">
<th>HTTP Method</th>
<td><code>GET</code></td>
</tr>
<tr class="even">
<td>Request/Response Format</td>
<td><br />
</td>
</tr>
<tr class="odd">
<td>Authentication</td>
<td>Basic</td>
</tr>
<tr class="even">
<td>Username</td>
<td><code>admin</code></td>
</tr>
<tr class="odd">
<td>Password</td>
<td><code>admin</code></td>
</tr>
<tr class="even">
<td>Runtime</td>
<td>Tooling</td>
</tr>
</tbody>
</table>

#### Parameter description

| Parameter           | Description                                                                    |
|---------------------|--------------------------------------------------------------------------------|
| `{templateGroupID}` | The UUID of the template group of which the rule templates need to be fetched. |

### curl command syntax

``` java
curl -X GET "https://localhost:9643/business-rules/template-groups/{templateGroupID}/templates" -u admin:admin -k
```

### Sample curl command

``` java
curl -X GET "https://localhost:9643/business-rules/template-groups/sweet-factory/templates" -u admin:admin -k
```

### Sample output

``` java
```

### Response

<table>
<tbody>
<tr class="odd">
<th>HTTP Status Code</th>
<td><p>200 or 404</p>
<p>For descriptions of the HTTP status codes, see <a href="https://ei.docs.wso2.com/en/latest/streaming-integrator/ref/hTTP-Status-Codes/">HTTP Status Codes</a> .</p></td>
</tr>
</tbody>
</table>

## Fetch rule template of specific UUID available under a template group with specific UUID

### Overview

<table>
<tbody>
<tr class="odd">
<th>Description</th>
<td>Returns the rule template with the specified UUID that is defined under the template group with the specified UUID.</td>
</tr>
<tr class="even">
<th>API Context</th>
<td><code>/business-rules/template-groups/{templateGroupID}/templates/{ruleTemplateID}</code></td>
</tr>
<tr class="odd">
<th>HTTP Method</th>
<td><code>GET</code></td>
</tr>
<tr class="even">
<th>Request/Response Format</th>
<td><br />
</td>
</tr>
<tr class="odd">
<th>Authentication</th>
<td>Basic</td>
</tr>
<tr class="even">
<th>Username</th>
<td><code>admin</code></td>
</tr>
<tr class="odd">
<th>Password</th>
<td><code>admin</code></td>
</tr>
<tr class="even">
<th>Runtime</th>
<td>Tooling</td>
</tr>
</tbody>
</table>

#### Parameter description

| Parameter                                    | Description                                                                                  |
|----------------------------------------------|----------------------------------------------------------------------------------------------|
| `{templateGroupID}`| The UUID of the template group from which the specified rule template needs to be retrieved. |
| `{ruleTemplateID}` | The UUID of the rule template that needs to be retrieved from the specified template group.  |

### curl command syntax

``` java
curl -X GET "https://localhost:9643/business-rules/template-groups/{templateGroupID}/templates/{ruleTemplateID}" -u admin:admin -k
```

### Sample curl command

``` java
curl -X GET "https://localhost:9643/business-rules/template-groups/sweet-factory/templates/identifying-continuous-production-decrease" -u admin:admin -k
```

### Sample output

``` java
```

### Response

<table>
<tbody>
<tr class="odd">
<th>HTTP Status Code</th>
<td><p>200 or 404</p>
<p>For descriptions of the HTTP status codes, see <a href="https://ei.docs.wso2.com/en/latest/streaming-integrator/ref/hTTP-Status-Codes/">HTTP Status Codes</a> .</p></td>
</tr>
</tbody>
</table>

## Fetch available template groups

### Overview

<table>
<tbody>
<tr class="odd">
<td>Description</td>
<th>Returns all the template groups that are currently available in the SI setup.</th>
</tr>
<tr class="even">
<th>API Context</th>
<td><code>/business-rules/template-groups</code></td>
</tr>
<tr class="odd">
<th>HTTP Method</th>
<td><code>GET</code></td>
</tr>
<tr class="even">
<th>Request/Response Format</th>
<td><br />
</td>
</tr>
<tr class="odd">
<th>Authentication</th>
<td>Basic</td>
</tr>
<tr class="even">
<th>Username</th>
<td><code>admin</code></td>
</tr>
<tr class="odd">
<th>Password</th>
<td><code>admin</code></td>
</tr>
<tr class="even">
<th>Runtime</th>
<td>Tooling</td>
</tr>
</tbody>
</table>

### curl command syntax

``` java
curl -X GET "https://<HOST_NAME>:<PORT>/business-rules/template-groups" -u admin:admin -k
```

### Sample curl command

``` java
curl -X GET "https://localhost:9643/business-rules/template-groups" -u admin:admin -k
```

### Sample output

``` java

```

### Response

<table>
<tbody>
<tr class="odd">
<th>HTTP Status Code</th>
<td><p>200 or 404</p>
<p>For descriptions of the HTTP status codes, see <a href="https://ei.docs.wso2.com/en/latest/streaming-integrator/ref/hTTP-Status-Codes/">HTTP Status Codes</a>.</p></td>
</tr>
</tbody>
</table>

## Fetch business rule instance with given UUID

### Overview

<table>
<tbody>
<tr class="odd">
<td>Description</td>
<th>Returns the business rule instance with the given UUID.</th>
</tr>
<tr class="even">
<th>API Context</th>
<td><code>/business-rules/instances/{businessRuleInstanceID}</code></td>
</tr>
<tr class="odd">
<th>HTTP Method</th>
<td><code>GET</code></td>
</tr>
<tr class="even">
<th>Request/Response Format</th>
<td><code>application/json</code>
</td>
</tr>
<tr class="odd">
<th>Authentication</th>
<td>Basic</td>
</tr>
<tr class="even">
<th>Username</th>
<td><code>admin</code></td>
</tr>
<tr class="odd">
<th>Password</th>
<td><code>admin</code></td>
</tr>
<tr class="even">
<th>Runtime</th>
<td>Tooling</td>
</tr>
</tbody>
</table>


#### Parameter description

| Parameter                  | Description                                            |
|----------------------------|--------------------------------------------------------|
| `{businessRuleInstanceID}` | The UUID of the business rules instance to be fetched. |

### curl command syntax

``` java
curl -X GET "https://<HOST_NAME>:<PORT>/business-rules/instances/{businessRuleInstanceID}" -H "accept: application/json" -u admin:admin -k
```

### Sample curl command

``` java
curl -X GET "https://localhost:9643/business-rules/instances/business-rule-1" -H "accept: application/json" -u admin:admin -k
```

### Sample output

``` java

```

### Response

<table>
<tbody>
<tr class="odd">
<th>HTTP Status Code</th>
<td><p>200 or 404</p>
<p>For descriptions of the HTTP status codes, see <a href="https://ei.docs.wso2.com/en/latest/streaming-integrator/ref/hTTP-Status-Codes/">HTTP Status Codes</a>.</p></td>
</tr>
</tbody>
</table>

  

## Create and save a business rule

### Overview

<table>
<tbody>
<tr class="odd">
<th>Description</th>
<th>Creates and saves a business rule.</th>
</tr>
<tr class="even">
<th>API Context</th>
<td><code>/business-rules/instances?deploy={deploymentStatus}</code></td>
</tr>
<tr class="odd">
<th>HTTP Method</th>
<td><code>POST</code></td>
</tr>
<tr class="even">
<th>Request/Response Format</th>
<td><code>application/json</code>
</td>
</tr>
<tr class="odd">
<th>Authentication</th>
<td>Basic</td>
</tr>
<tr class="even">
<th>Username</th>
<td><code>admin</code></td>
</tr>
<tr class="odd">
<th>Password</th>
<td><code>admin</code></td>
</tr>
<tr class="even">
<th>Runtime</th>
<td>Tooling</td>
</tr>
</tbody>
</table>

#### Parameter description

<table>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>{deploymentStatus}</code></td>
<td><br />
</td>
</tr>
</tbody>
</table>

### curl command syntax

``` java

```

### Sample curl command

``` java
curl -X POST "https://localhost:9643/business-rules/instances?deploy=true" -H "accept: application/json" -H "content-type: multipart/form-data" -F 'businessRule={"name":"Business Rule 5","uuid":"business-rule-5","type":"template","templateGroupUUID":"sweet-factory","ruleTemplateUUID":"identifying-continuous-production-decrease","properties":{"timeInterval":"6","timeRangeInput":"5","email":"example@email.com"}}' -u admin:admin -k
```

### Sample output

``` java
```

### Response

<table>
<tbody>
<tr class="odd">
<th>HTTP Status Code</th>
<td><p>200 or 404</p>
<p>For descriptions of the HTTP status codes, see <a href="https://ei.docs.wso2.com/en/latest/streaming-integrator/ref/hTTP-Status-Codes/">HTTP Status Codes</a> .</p></td>
</tr>
</tbody>
</table>

## Update business rules instance with given UUID

### Overview

<table>
<tbody>
<tr class="odd">
<th>Description</th>
<th>Updates the business rules instance with the given UUID. </th>
</tr>
<tr class="even">
<th>API Context</th>
<td><code>/business-rules/instances/{businessRuleInstanceID}?deploy={deploymentStatus}</code></td>
</tr>
<tr class="odd">
<th>HTTP Method</th>
<td><code>PUT</code></td>
</tr>
<tr class="even">
<th>Request/Response Format</th>
<td><code>application/json</code>
</td>
</tr>
<tr class="odd">
<th>Authentication</th>
<td>Basic</td>
</tr>
<tr class="even">
<th>Username</th>
<td><code>admin</code></td>
</tr>
<tr class="odd">
<th>Password</th>
<td><code>admin</code></td>
</tr>
<tr class="even">
<th>Runtime</th>
<td>Tooling</td>
</tr>
</tbody>
</table>


#### Parameter description

<table>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>{businessRuleInstanceID}</code></td>
<td>The UUID of the business rules instance to be updated.</td>
</tr>
<tr class="even">
<td><code>{deploymentStatus}</code></td>
<td><br />
</td>
</tr>
</tbody>
</table>

### curl command syntax

``` java

```

  

### Sample curl command

``` java
curl -X PUT "https://localhost:9643/business-rules/instances/business-rule-5?deploy=true" -H "accept: application/json" -H "content-type: application/json" -d '{"name":"Business Rule 5","uuid":"business-rule-5","type":"template","templateGroupUUID":"sweet-factory","ruleTemplateUUID":"identifying-continuous-production-decrease","properties":{"timeInterval":"9","timeRangeInput":"8","email":"newexample@email.com"}}' -u admin:admin -k
```

### Sample output

``` java

```

### Response

<table>
<tbody>
<tr class="odd">
<th>HTTP Status Code</th>
<td><p>200 or 404</p>
<p>For descriptions of the HTTP status codes, see <a href="https://ei.docs.wso2.com/en/latest/streaming-integrator/ref/hTTP-Status-Codes/">HTTP Status Codes</a>.</p></td>
</tr>
</tbody>
</table>

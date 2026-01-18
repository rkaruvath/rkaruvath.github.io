<div style="text-align: right">
<a href="https://rkaruvath.github.io/WorkSamples/index.html">Home</a><br><a href="https://rkaruvath.github.io/WorkSamples/WritingSample.html">Documentation sample</a><br><a href="https://rkaruvath.github.io/WorkSamples/InfographicSample.html">Infographics sample</a><br><a href="https://rkaruvath.github.io/WorkSamples/VideoSample.html">Video sample</a>
</div>

# REST API documentation sample
This page contains REST API documentation sample.

___

## Change Management REST API
Use the Change Management module in the ITSM application to plan, schedule, implement, and manage changes to the technology environment in your organization. For example, migrate data to a new database system. 

Alternatively, you can use the following REST API endpoints to perform the change operations: 

|Operation|HTTP method|Endpoint|Description
|---|---|---|---|
| [Create a change request](#create-a-change-request)|POST|/change|Creates a new change request.|
|[Show a change request](#show-a-change-request)|GET|/change/{id}|Shows the details of a change request by ID.|
|[Update a change request](#update-a-change-request)|PATCH|/change/{id}|Updates a change request by ID.|

---

## Create a change request
`POST` /change

Creates a new change request.

### Request URL
&lt;baseurl&gt;/change

### Request

#### Header parameters

|Name|Description|
|---|---|
|Authorization|Authorization: Bearer &lt;token&gt;|
|Content-Type|application/json|

#### Request body parameters

|Name|Description|Type|
|---|---|---|
|summary|Summary for the change request.|string|
|impact (optional)|Impact of the change on the service level of the affected business processes.<br><br>The following are the supported values:<br>- 1000: Extensive/Widespread<br>- 2000: Significant/Large<br>- 3000: Moderate/Limited<br>- (Default) 4000: Minor/Localized|integer|
urgency (optional)|Urgency measures how soon the change will significantly impact the business.<br><br>For example, a high-impact change may have low urgency if the impact is not expected to affect the business in the near future.<br><br>The following are the supported values:<br>- 1000: Critical<br>- 2000: High<br>- 3000: Medium<br>- (Default) 4000: Low|integer|
|priority (optional)|Priority is the relative importance of the change. Priority is based on the impact and urgency of the change.<br><br>The following are the supported values:<br>- 1: Critical<br>- 2: High<br>- 3: Medium<br>- (Default) 4: Low|integer|
|risk level (optional)|The anticipated risk for the change.<br><br>For example, if a critical security update needs to be installed on all computers during business hours, the risk level can be 4 or 5. However, if it can be installed during non-business hours, the risk level can be 2.<br><br>The following are the supported values:<br>- 1: Minimal (lowest risk)<br>- 2: Low<br>- 3: Medium<br>- 4: High<br>- 5: Extreme (highest risk)|integer|
|status (optional)|The current state of the change request.<br><br>The following are the supported values:<br>- (Default) 0: Draft<br>- 1: Request For Authorization<br>- 2: Planning In Progress<br>- 3: Scheduled For Review<br>- 4: Scheduled For Approval<br>- 5: Scheduled<br>- 6: Implementation In Progress<br>- 7: Pending<br>- 8: Rejected<br>- 9: Completed<br>- 10: Closed<br>- 11: Cancelled|integer|
|locationCompany|The location where the change needs to be implemented.|string|
|requestedFor.loginId|The login ID of the user initiating the change request.|string|
|coordinator.loginId|The login ID of the change coordinator to be assigned the change request.|string|
|changeManager.loginId|The login ID of the change manager  monitoring the change request.|string|

#### Example request schema
![Create change schema](/Images/Create_Change_API_Request_Schema.png)

#### Example request
![Create change request sample](/Images/Create_Change_API_Request_Sample_cURL.png)

### Response

#### Response attributes
After a change request is successfully created, the API returns an HTTP 201 Created status code with a JSON response body that includes the following attributes:

|Attribute name|Child attribute name|Description|Type|
|---|---|---|---|
|status||A message indicating that the change request is successfully created.|string|
|details||An object containing specific identifiers associated with the new change request.|object|
||requestId|A unique identifier of the specific API request. Use this ID when searching through logs to track this transaction.|string|
||guid|A Globally Unique Identifier (GUID) of the new change request. This is a system-generated, immutable string used for internal database mapping.|string|
||id|A business-facing identifier of the new change request. Use this ID for subsequent GET, PATCH, or DELETE operations on this specific change request.|string|

#### Status codes

|Status code|Description|Example response|
|---|---|---|
|201 Created|The resource is created successfully.|![201_Created_Status](/Images/POST_201_Created_Status.png)|
|400 Bad request|One or more fields contain invalid values.|![400_Invalid_Values](/Images/POST_400_Invalid_Values.png)|
|403 Unauthorized|The authentication credentials are incorrect or missing.|![403_Unauthorized](/Images/POST_403_Unauthorized.png)|
|500 Internal server error|The server encountered an unexpected error and couldn't complete the request.|![500_Internal_Server_Error](/Images/POST_500_Internal_Server_Error.png)|

---

## Show a change request
`GET` /change/{id}

Shows a change request by ID.

### Request URL
&lt;baseurl&gt;/change/{id}

### Request

#### Header parameters

|Name|Description|
|---|---|
|Authorization|Authorization: Bearer &lt;token&gt;|
|Accept|application/json|

#### Path parameters

|Name|Description|
|---|---|
|id|Unique identifier of the change request to be retrieved.<br>For example: CRQ000000000001.|

#### Example request
![Get change request by ID](/Images/Get_Change_API_Request_Sample_cURL.png)

### Response

#### Status code

|Status code|Description|Example response|
|---|---|---|
|200 OK|The resource is retrieved successfully.|![Get_200](/Images/Get_200_Retrieved.png)|
|403 Unauthorized|The authentication credentials are incorrect or missing.|![GET_403_Unauthorized](/Images/Get_403_Unauthorized.png)|
|404 Not found|The requested resource does not exist.|![404_Not_Found](/Images/404_Not_Found.png)|
|500 Internal server error|The server encountered an unexpected error and couldn't complete the request.|![500_Internal_Server_Error](/Images/POST_500_Internal_Server_Error.png)|

---

## Update a change request
`PATCH` /change/{id}

Updates a change request by ID.

### Request URL
&lt;baseurl&gt;/change/{id}

### Request

#### Header parameters

|Name|Description|
|---|---|
|Authorization|Authorization: Bearer &lt;token&gt;|
|Content-Type|application/json|

#### Path parameters

|Name|Description|
|---|---|
|id|Unique identifier of the change request to be updated.<br>For example: CRQ000000000001.|

#### Request body parameters

|Name|Description|Type|
|---|---|---|
status (Optional)|The current state of the change request.<br><br>The following are the supported values:<br>- (Default) 0: Draft<br>- 1: Request For Authorization<br>- 2: Planning In Progress<br>- 3: Scheduled For Review<br>- 4: Scheduled For Approval<br>- 5: Scheduled<br>- 6: Implementation In Progress<br>- 7: Pending<br>- 8: Rejected<br>- 9: Completed<br>- 10: Closed<br>- 11: Cancelled|integer|
|statusReason (Optional)|Reason for the current status change.|string|
|summary (Optional)|Summary of the change request.|string|

#### Example request schema
![Update change schema](/Images/Update_Change_API_Request_Schema.png)

#### Example request
![Update change request sample](/Images/Update_Change_API_Request_Sample_cURL.png)

### Response

#### Status codes

|Status code|Description|Example response|
|---|---|---|
|200 OK|Successfully updated the resource.|![200_OK_Updated](/Images/Patch_200_OK.png)|
|400 Bad request|One or more fields contain invalid values.|![400_Bad_Request](/Images/Patch_400_Bad_Request.png)|
|403 Unauthorized|The authentication credentials are incorrect or missing.|![403_Unauthorized](/Images/POST_403_Unauthorized.png)|
|500 Internal server error|The server encountered an unexpected error and couldn't complete the request.|![500_Internal_Server_Error](/Images/POST_500_Internal_Server_Error.png)|







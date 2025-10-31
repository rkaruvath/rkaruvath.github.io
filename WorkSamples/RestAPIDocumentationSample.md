# REST API documentation sample
This page contains REST API documentation sample.

## Change management REST API
Use the Change Management module to plan, schedule, implement, and manage changes to the technology environment in your organization. For example, migrate data to a new database system. 

Alternatively, you can use the following REST API endpoints to perform the change operations: 

|Operation|HTTP method|Endpoint|Description
|---|---|---|---|
| [Create a change request](#create-a-change-request)|POST|/change|Creates a new change request.|
|[Show a change request](#show-a-change-request)|GET|/change/{id}|Shows the details of a change request, by ID.|
|[Update a change request](#update-a-change-request)|PATCH|/change/{id}|Updates a change request, by ID.

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
|impact (optional)|Impact of the change on the service level of the affected business processes.<br><br>The following are the supported values:<br>- 1000: "1-Extensive/Widespread"<br>- 2000: "2-Significant/Large"<br>- 3000: "3-Moderate/Limited"<br>- (Default) 4000: "4-Minor/Localized"</p>|integer|
urgency (optional)|Urgency measures how soon the change will significantly impact the business.<br><br>For example, a high-impact change may have low urgency if the impact is not expected to affect the business in the near future.<br><br>The following are the supported values:<br>- 1000: "1-Critical"<br>- 2000: "2-High"<br>- 3000: "3-Medium"<br>- (Default) 4000: "4-Low"|integer|
|priority (optional)|Priority is the relative importance of the change. Priority is based on the impact and urgency of the change.<br><br>The following are the supported values:<br>- 0: "1-Critical"<br>- 1: "2-High"<br>- 2: "3-Medium"<br>- (Default) 3: "4-Low"|integer|
|risk level (optional)|Risk level is the anticipated risk for the change.<br><br>For example, if a critical security update needs to be installed on all computers during business hours, the risk level can be 4 or 5. If it can be installed during non-business hours, the risk level can be 2.<br><br>The following are the supported values:<br>- 1: Minimal (lowest risk)<br>- 2: Low<br>- 3: Medium<br>- 4: High<br>- 5: Extreme (highest risk)|integer|
|status (optional)|Status is the current state of the change request.<br><br>The following are the supported values:<br>- (Default) 0: "Draft"<br>- 1: "Request For Authorization"<br>- 2: "Request For Change"<br>- 3: "Planning In Progress"<br>- 4: "Scheduled For Review"<br>- 5: "Scheduled For Approval"<br>- 6: "Scheduled"<br>- 7: "Implementation In Progress"<br>- 8: "Pending"<br>- 9: "Rejected"<br>- 10: "Completed"<br>- 11: "Closed"<br>- 12: "Cancelled"|integer|
|locationCompany|The location where the change needs to be implemented.|string|
|requestedFor.loginId|The login ID of the user initiating the change request.|string|
|coordinator.loginId|The login ID of the change coordinator to be assigned the change request.|string|
|changeManager.loginId|The login ID of the change manager  monitoring the change request.|string|

#### Example schema
![Create change schema](/Images/Create_Change_API_Request_Schema.png)

#### Request sample
![Create change request sample](/Images/Create_Change_API_Request_Sample_cURL.png)

### Response

#### Status codes

|Status code|Description|
|---|---|
|201 Created|The resource is created successfully.|
|400 Bad request|One or more fields contain invalid values.|
|403 Unauthorized|Authentication credentials are incorrect or missing.|
|500 Internal server error|The server encountered an unexpected error and couldn't complete the request.|

## Show a change request
`GET` /change/{id}

Shows a change request by its ID.

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

#### Request sample
![Get change request by ID](/Images/Get_Change_API_Request_Sample_cURL.png)

### Response

#### Status code

|Status code|Description|
|---|---|
|200 OK|The resource is retrieved successfully.|
|403 Unauthorized|The authentication credentials are incorrect or missing.|
|404|The requested resource does not exist.|
|500 Internal server error|The server encountered an unexpected error and couldn't complete the request.|

## Update a change request
`PATCH` /change/{id}

Updates a change request by its ID.

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
status (Optional)|Status is the current state of the change request.<br><br>The following are the supported values:<br>- (Default) 0: "Draft"<br>- 1: "Request For Authorization"<br>- 2: "Request For Change"<br>- 3: "Planning In Progress"<br>- 4: "Scheduled For Review"<br>- 5: "Scheduled For Approval"<br>- 6: "Scheduled"<br>- 7: "Implementation In Progress"<br>- 8: "Pending"<br>- 9: "Rejected"<br>- 10: "Completed"<br>- 11: "Closed"<br>- 12: "Cancelled"|integer|
|statusReason (Optional)|Reason for the current status change.|string|
|summary (Optional)|Summary of the change request.|string|
|impact (Optional)|Impact of the change on the service level of the affected business processes.<br><br>The following are the supported values:<br>- 1000: "1-Extensive/Widespread"<br>- 2000: "2-Significant/Large"<br>- 3000: "3-Moderate/Limited"<br>- (Default) 4000: "4-Minor/Localized"|integer|
urgency (optional)|Urgency measures how soon a change will significantly impact the business.<br><br>For example, a high-impact change may have low urgency if the impact is not expected to affect the business in the near future.<br><br>The following are the supported values for urgency:<br>- 1000: "1-Critical"<br>- 2000: "2-High"<br>- 3000: "3-Medium"<br>- (Default) 4000: "4-Low"|integer|
|priority (optional)|Priority is the relative importance of the change. Priority is based on the impact and urgency of the change.<br><br>The following are the supported values:<br>- 0: "1-Critical"<br>- 1: "2-High"<br>- 2: "3-Medium"<br>- (Default) 3: "4-Low"|integer|
|risk level (optional)|Risk level is the anticipated risk for the change.<br><br>For example, if a critical security update needs to be installed on all computers during business hours, the risk level can be 4 or 5. If it can be installed during non-business hours, the risk level can be 2.<br><br>The following are the supported values for risk level:<br>- 1 : Minimal (lowest risk)<br>- 2 : Low<br>- 3 : Medium<br>- 4 : High<br>- 5 : Extreme (highest risk)|integer|

#### Example schema
![Update change schema](/Images/Update_Change_API_Request_Schema.png)

#### Request sample
![Update change request sample](/Images/Update_Change_API_Request_Sample_cURL.png)

### Response

#### Status codes

|Status code|Description|
|---|---|
|200 OK|Successfully updated the resource.|
|400 Bad request|One or more fields contain invalid values.|
|403 Unauthorized|The authentication credentials are incorrect or missing.|
|500 Internal server error|The server encountered an unexpected error and couldn't complete the request.|







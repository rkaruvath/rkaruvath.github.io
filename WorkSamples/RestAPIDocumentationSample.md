# REST API documentation sample
This page contains REST API sample documentation.

## Change management REST API
Use the Change Management module to plan, schedule, implement, and manage changes to the technology environment in your organization. For example, change passwords or hard disks. 

Alternately, you can use the following REST API endpoints to perform the change operations: 

|Operation|HTTP method|Endpoint|Description
|---|---|---|---|
| [Create a change request](#create-a-change-request)|POST|/change|Creates a new change request.|
|[Show a change request](#show-a-change-request)|GET|/change/{id}|Shows the details of a change request, by ID.|
|[Update a change request](#update-a-change-request)|PATCH|/change/{id}|Updates a change request, by ID.

## Create a change request
Creates a new change request.

`POST /change`

### URL format
{baseurl}/change

### Request

#### Header parameters

|Name|Description|
|---|---|
|Authorization|Contains the authentication credentials for HTTP authentication.<br>Example: AR-JWT={{token}}|
|X-Requested-By|Example: XMLHttpRequest|
|Content-Type|Data format of the request body.<br>The supported format is application/json.|

#### Request body parameters
|Name|Description|Type|
|---|---|---|
|summary|Summary of the change request.|string|
|impact (optional)|Impact of a change on the service level of the affected business processes.<br>The following are the supported values for impact:<br>- 1000: "1-Extensive/Widespread"<br>- 2000: "2-Significant/Large"<br>- 3000: "3-Moderate/Limited"<br>- (Default) 4000: "4-Minor/Localized"</p>|integer|
urgency (optional)|Urgency measures how soon a change will significantly impact the business.<br>For example, a high impact change may have low urgency if the impact does not affect the business until the end of the financial year.<br>The following are the supported values for urgency:<br>- 1000: "1-Critical"<br>- 2000: "2-High"<br>- 3000: "3-Medium"<br>- (Default) 4000: "4-Low"|integer|
|status (optional)|Status is the current state of a change request.<br>The following are the supported values for status:<br>- (Default) 0: "Draft"<br>- 1: "Request For Authorization"<br>- 2: "Request For Change"<br>- 3: "Planning In Progress"<br>- 4: "Scheduled For Review"<br>- 5: "Scheduled For Approval"<br>- 6: "Scheduled"<br>- 7: "Implementation In Progress"<br>- 8: "Pending"<br>- 9: "Rejected"<br>- 10: "Completed"<br>- 11: "Closed"<br>- 12: "Cancelled"|integer|
|priority (optional)|Priority identifies the relative importance of a change. Priority is based on impact and urgency of a change, and it identifies required times for actions to be taken. <br>The following are the supported values for priority:<br>- 0: "1-Critical"<br>- 1: "2-High"<br>- 2: "3-Medium"<br>- (Default) 3: "4-Low"|integer|
|risk level (optional)|Risk level is the anticipated risk for the change.<br>For example, if the support team needs to install a critical security update on all the computers in the sales department during working hours, the risk level can be 4 or 5. If the critical security update can be installed during non-working hours, the risk level can be 2.<br>The following are the supported values for risk level:<br>- 1 : Minimal (lowest risk)<br>- 2 : Low<br>- 3 : Medium<br>- 4 : High<br>- 5 : Extreme (highest risk)|integer|
|locationCompany|The location where the change needs to be implemented.|string|
|requestedFor.loginId|The login ID of the user who initiated the change request.|string|
|coordinatorGroupId (optional)|The ID of the change coordinator group that is assigned the change request.|string|
|coordinatorGroup (optional)|The name of change coordinator group that is assigned the change request.|string|
|coordinatorGroupOrganization (optional)|The organization of the change coordinator group that is assigned the change request.|string|
|coordinator.loginId|The login ID of the change coordinator who is assigned the change request.|string|
|changeManager.loginId|The login ID of the change manager monitoring the change request.|string|

### Response

#### Status codes
|Status code|Description|
|---|---|
|201 Created|Request is successful.|
|400 Bad request|One or more fields contain invalid values.|
|403 Unauthorized|Authentication credentials are incorrect or missing.|
|500 Internal server error|The server encountered an unexpected condition, which prevented it from fulfilling the request.|

### Sample usage

---screenshot>

## Show a change request
Shows a change request by its ID.

`GET /change/{id}`

### URL format
{baseurl}/change/{id}

### Request

#### Header parameters
|Name|Description|
|---|---|
|Authorization|Contains the authentication credentials for HTTP authentication.Example: AR-JWT={{token}}|
|X-Requested-By|Example: XMLHttpRequest|
|Accept|Data format of the response body. Supported types: application/json or application/xml.|

#### Path parameters
|Name|Description|
|---|---|
|id|Unique identifier of the change request.<br>For example: CRQ000000000001|

### Response

#### Status code
|Status code|Description|
|---|---|
|200 OK|Request is successful.|
|400 Bad request|The request:<br>- is missing required fields.<br>- contains invalid field values.<br>- is by a user who does not have the necessary permission to view the change request.|
|403 Unauthorized|The authentication credentials are incorrect or missing.|
|404|The requested resource doesn’t exist.|
|500 Internal server error|The server encountered an unexpected condition, which prevented it from fulfilling the request.|

### Sample usage

---screenshot>

## Update a change request
Updates a change request by its ID.

`PATCH /change/{id}`

### URL format
{baseurl}/change/{id}

### Request

#### Header parameters
|Name|Description|
|---|---|
|Authorization|Contains the authentication credentials for HTTP authentication.Example: AR-JWT={{token}}|
|X-Requested-By|Example: XMLHttpRequest|
|Accept|Data format of the response body. Supported types: application/json or application/xml.|
|

#### Path parameters
|Name|Description|
|---|---|
|id|Unique identifier of the change request.<br>For example: CRQ000000000001|

#### Request body parameters
|Name|Description|Type|
|---|---|---|
status (Optional)|Status is the state of change request in its control process flow and transitions as it follows the process through its lifecycle. The following are the supported values for status:<br>- (Default) 0: "Draft"<br>- 1: "Request For Authorization"<br>- 2: "Request For Change"<br>- 3: "Planning In Progress"<br>- 4: "Scheduled For Review"<br>- 5: "Scheduled For Approval"<br>- 6: "Scheduled"<br>- 7: "Implementation In Progress"<br>- 8: "Pending"<br>- 9: "Rejected"<br>- 10: "Completed"<br>- 11: "Closed"<br>- 12: "Cancelled"|integer|
|statusReason (Optional)|Reason of the current status change.|string|
|summary (Optional)|Summary of the change request.|string|
|impact (Optional)|Impact is a measure of the effect of an incident, problem, or change on business processes. Impact is often based on how service levels will be affected. Following are the supported values for impact:<br>- 1000: "1-Extensive/Widespread"<br>- 2000: "2-Significant/Large"<br>- 3000: "3-Moderate/Limited"<br>- (Default) 4000: "4-Minor/Localized"|integer|
|priority (optional)|Priority is a category that identifies the relative importance of an incident, problem, or change. Priority is based on impact and urgency, and it identifies required times for actions to be taken. Impact and urgency are used to assign priority. Following are the supported values for priority:<br>- 0: "1-Critical"<br>- 1: "2-High"<br>- 2: "3-Medium"<br>- (Default) 3: "4-Low"|integer|


### Response

#### Status codes
|Status code|Description|
|---|---|
|200 OK|The request is successful.|
|400 Bad request|The request: <br>- is missing required fields.<br>- contains invalid field values.<br>- contains fields that cannot be set for the issue type.<br>- is by a user who does not have the necessary permission to update the change request.|
|403 Unauthorized|The authentication credentials are incorrect or missing.|
|500 Internal server error|The server encountered an unexpected condition, which prevented it from fulfilling the request.|

### Sample usage

---screenshot>







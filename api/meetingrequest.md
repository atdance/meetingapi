
# MeetingRequest
Suggest meeting times based on employee time constraints specified as parameters.


## HTTP request

```http
POST /calendar/MeetingRequest
```

## Request body
All the supported parameters are listed below. Depending on your scenario, specify a JSON object for each of the necessary parameters in the request body.


| Parameter	   | Type	|Description|
|:---------------|:--------|:----------|
|employees|[employee](../resources/employee.md) collection|A collection of employeess for the meeting.  Required.|
|meetingDuration|Edm.Duration|The length of the meeting, denoted in [ISO8601](https://www.iso.org/iso/iso8601) format. 

 
 If no meeting duration is specified, **MeetingRequest** uses the default of 30 minutes. Optional.|
 
 
|timeSlot|[timeSlot](../resources/timeslot.md)| Target meeting time periods (**timeSlots** property).|

## Response

If successful, this method returns `200 OK` response code and a [meetingReply](../resources/meetingreply.md) in the response body.

By default, each meeting time suggestion is returned in UTC.

If **MeetingRequest** cannot return any meeting suggestions, the response would indicate
this setting the property **approved** to false.


## Example

The following example shows how to find time to meet by specifying the following parameters in the request body:

- **employees** , participants (employee ids), one or multiple
- **timeSlot** earliest and latest requested meeting date and time
- **meetingDuration** , desired meeting length (minutes) 
- **office hours** (e.g. 08-17)


##### Request
Here is the example request.

# [HTTP](#tab/http)

```http
POST https://api.mysite.com/v1.0/me/MeetingRequest
Content-Type: application/json

{
  "employees": [
    {
      "id": "162783",  
      "emailAddress": {
        "name": "Alex Wilbur",
        "address": "alf.red@myaacount.com"
      }
    }
  ],  
    "timeslots": [
      {
        "start": "2019-04-16T09:00:00",  
        "end": "2019-04-18T17:00:00",  
       }
    ],  
  "meetingDuration": "PT1H"
}
```
---

##### Response
Here is an example response.

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "approved": "true",
    "timeslots": [
		{            
			"meetingTimeSlot": {
                "start": "2019-04-18T16:00:00.0000000",
                "end": "2019-04-18T17:00:00.0000000"
            }
        },
		{
            "meetingTimeSlot": {
                "start": "2019-04-18T08:00:00.0000000",
                "end": "2019-04-18T09:00:00.0000000"
            }
        }        
    ]
}
```

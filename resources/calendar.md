
# calendar resource type

A calendar is a container for meetings.


## Properties
| Property	   | Type	|Description|
|:---------------|:--------|:----------|
|name|String|The calendar name.|
|owner |[emailAddress](emailaddress.md) | This represents the user who created or added the calendar.  

## JSON representation

Here is a JSON representation of the resource


```json
{
  "name": "string",
  "owner": {"@odata.type": ".emailAddress"}
}

```

# meetingReply resource type

A collection of meeting suggestions if there is any, and if the meeting is possible.

## JSON representation

Here is a JSON representation of the resource

```json
{
  "approved": "Boolean",
  "timeSLot": [{"@odata.type": "timeSLot"}]
}

```
## Properties
| Property	   | Type	|Description|
|:---------------|:--------|:----------|
|approved|Boolean|If the meeting can be set up.|
|timeSlot|[timeSlot](timeslot.md) collection|An array of meeting time suggestions.|

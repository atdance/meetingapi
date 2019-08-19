# MeetingAPI
Suggest meeting times based on employee time constraints.


## Architecture

A calender database is the core.
A REST based application 
- sends the incoming meeting requests to the calender 
- updates the calender with the incoming messages from the emmployees that update their availability

### Schema

All API access is over HTTPS, and accessed from https://api.mysite.com. All data is sent and received as JSON.

### Rate limiting

For API requests using Basic Authentication or OAuth, you can make up to 5000 requests per hour. Authenticated requests are associated with the authenticated user, regardless of whether Basic Authentication or an OAuth token was used. This means that all OAuth applications authorized by a user share the same quota of 5000 requests per hour when they authenticate with different tokens owned by the same user.

For unauthenticated requests, the rate limit allows for up to 60 requests per hour. Unauthenticated requests are associated with the originating IP address, and not the user making requests.

Note that the Search API has custom rate limit rules.

The returned HTTP headers of any API request show your current rate limit status:

|Header Name|Description|
|X-RateLimit-Limit|The maximum number of requests you're permitted to make per hour.|
|X-RateLimit-Remaining|The number of requests remaining in the current rate limit window.|
|X-RateLimit-Reset|The time at which the current rate limit window resets in UTC epoch seconds.|


## Resources

- [**Calendar**](resources/calendar.md )
- [**Employee**](resources/employee.md)
- [**MeetingReply**](resources/meetingreply.md)
- [**Timeslot**](resources/timeslot.md)


## API

- [**meetingRequest**](api/meetingrequest.md)
- [**employeeAvailability**](api/employeeavailability.md)

 
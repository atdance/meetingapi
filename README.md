# MeetingAPI
Suggest meeting times based on employee time constraints.


## Architecture

A calender database is the core.
A REST based application
- sends the incoming meeting requests to the calender
- updates the calender with the incoming messages from the employees that update their availability

## Resources

- [**Calendar**](resources/calendar.md )
- [**Employee**](resources/employee.md)
- [**MeetingReply**](resources/meetingreply.md)
- [**Timeslot**](resources/timeslot.md)


## API

- [**meetingRequest**](api/meetingrequest.md)
- [**employeeAvailability**](api/employeeavailability.md)

### Schema

All API access is over HTTPS, and accessed from https://api.mysite.com. All data is sent and received as JSON.

### Rate limiting

For API requests using Basic Authentication or OAuth, you can make up to 5000 requests per hour. Authenticated requests are associated with the authenticated user, regardless of whether Basic Authentication or an OAuth token was used. This means that all OAuth applications authorized by a user share the same quota of 5000 requests per hour when they authenticate with different tokens owned by the same user.

For unauthenticated requests, the rate limit allows for up to 60 requests per hour. Unauthenticated requests are associated with the originating IP address, and not the user making requests.

Note that the Search API has custom rate limit rules.

The returned HTTP headers of any API request show your current rate limit status:

|Header Name|Description|
|:---------------|:--------|
|X-RateLimit-Limit|The maximum number of requests you're permitted to make per hour.|
|X-RateLimit-Remaining|The number of requests remaining in the current rate limit window.|
|X-RateLimit-Reset|The time at which the current rate limit window resets in UTC epoch seconds.|

### User agent required

All API requests MUST include a valid User-Agent header. Requests with no User-Agent header will be rejected.

If you provide an invalid User-Agent header, you will receive a 403 Forbidden response.

### Client errors

These are the possible types of client errors on API calls that receive request bodies:

- Sending invalid JSON will result in a 400 Bad Request response.

```http
  HTTP/1.1 400 Bad Request
  Content-Length: 40

  {
	"message":"Problems parsing JSON"
  }
```	

- Sending the wrong type of JSON values will result in a 400 Bad Request response.

```http
  HTTP/1.1 400 Bad Request
  Content-Length: 35

  {
	"message":"Body should be a JSON object"
  }
```


### Timezones

Some requests that create new data allow you to provide time zone information when specifying or generating timestamps. We apply the following rules, in order of priority, to determine timezone information for API calls.

    - Explicitly providing an ISO 8601 timestamp with timezone information
    - Defaulting to UTC without other timezone information

#### Explicitly providing an ISO 8601 timestamp with timezone information

For API calls that allow for a timestamp to be specified, we use that exact timestamp.

These timestamps look something like 2019-09-27T15:05:09+01:00. Also see this example for how these timestamps can be specified.

#### Defaulting to UTC without other timezone information

If the steps above don't result in any information, we use UTC as the timezone to create or update the resource.

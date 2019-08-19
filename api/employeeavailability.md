# employeeAvailability

The availability of an employee.
A collection of times when the employee is available.

## Request body
All the supported parameters are listed below.
|ID| Int32 | A unique identifier for the employee.|
|emailAddress|emailAddress|Includes the name and SMTP address of the employee.|
|timeSlot|[timeSlot](timeslot.md) collection|An array of meeting time suggestions.|

## HTTP request

```http
POST /calendar/{id|userPrincipalName}/employeeAvailability
```
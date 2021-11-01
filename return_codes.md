# Return codes
Return codes should be limited to the following status codes and may combined with return-messages.

Status codes may be extended with error-response

    {
      err_code:'BAD_SHIPPING',
      err_msg:'Error in cleartext that may listen to LANG argument'
    }

**2xx Succeess**
- 200 OK (request completed)
- 201 Created (after successfull POST create record)
- 202 Accepted (request (intent) started or in que)

**3xx Moved** 
- 301 Moved permanently (rare use)

**4xx Client (request) error**
- 401 Unauthorized (I don't know who you are so I'm saying noting)
- 403 Forbidden (I know who you are and I'm not gonna let you do that)
- 404 Not found (You requested a resource, id or PAGE that does not exist)

**5xx Server error**
- 500 Internal Server Error (The backend hit an unexpected error)
- 503 Service Unavailable (A 3rd part service could not be reached)

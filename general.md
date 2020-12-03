# General
The goal of REST-x is to make REST-API's more fun, easy and stable to work with.

That's it. Here it is:

## Naming conventions

### Casing
The API should use the __camel_casing__ for resources its attribues.

For API arguments, such as COUNT or PAGE, UPPER_CAMEL_CASE should be used.
    
      /customers?PAGE=4&COUNT=50

* API-arguments may be sent in URI or HEADER
* No risk for collision with standard- or non-standard HTTP-HEADERS.
* No need to use (or not use) X-prefix in HEADER-arguments.

### Resources- and field names
* Resources should be named in pluralis, since:
  * Resources are collections
  * Provides a difference towards the resources attribues which are in singular
  * Irregular pluralis resources (mouce/mice) are rare
* Resouces should be limited to a two-level structure
* Field names are normally singularis

      /customers/53/orders?year=2018&status=shipped

### Versioning
Versioning should be provided in hostname, (hence the project name REST-x)
* It provides easier mapping (to machines or containers) of different verisons.
* Current version could be mapped to standard api.example.com

      api-2.example.com/customers?PAGE=5

## API-arguments
REST-x does not use header-arguments. API-arguments are sent in UPPER_CAMEL_CASE in request.
* Exception: file_name of binary file uploads (PUT).
* OAUTH/JWT etc are not a part of REST-x guidelines.

Current list of optional API arguments are:
* COUNT - number of records to be returned in collection
* PAGE - page of collection
* LANG - perefered language of error messages and hints.
* TZ - GMT time-zone
* DATE_FMT - YYYY-MM-DD
* TIME_FMT - H:i:s
* HINT - get data entry guidance for resource.

## Verbs
To comply with HTTP-standrds, the REST-verbs should be used as follows:

### GET
Reading data, either:
* collections (/customers),
* a collection with filter (/customers?city=Lund)
* a single resource (/customers/53), 
* custom view, (/customers/nearby?gps=53.25,25.25)

### POST
* Creating a record (/customers)
* Executing a method/intent (/customers/53/doClearBalance)
* NOT for replacing existing records.

### PUT
* Uploading binary content (/customers/53/customer_logo)
* NOT for replacing existing records.

### PATCH
* Updating PROVDED FIELDS on resource (/customers/53)

### DELETE
* Delete single resource (/customers/53)

## Return codes
Return codes should be limited to the following status codes and may combined with return-messages.

Status codes may be extended with error-response

    {
      err_code:'BAD_SHIPPING',
      err_msg:'Error in cleartext that may listen to LANG argument'
    }

__2xx Succeess__
* 200 OK (request completed)
* 201 Created (after successfull POST create record)
* 202 Accepted (request (intent) started or in que)

__3xx Moved__ 
* 301 Moved permanently (rare use)

__4xx Client (request) error__
* 401 Unauthorized (I don't know who you are so I'm saying noting)
* 403 Forbidden (I know who you are and I'm not gonna let you do that)
* 404 Not found (You requested a resource, id or PAGE that does not exist)

__5xx Server error__
* 500 Internal Server Error (The API is to be blamed)
* 503 Service Unavailable (3rd part API to be blamed)

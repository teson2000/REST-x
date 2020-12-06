# REST-x

## GOAL
- Define best praxises for REST
- For the better, bend some rules.

## End-point types
Each API-endpoint should be of one of the types below, with standard endpoint-location.

| Type        | Description                                                                                                                 | Methods allowed     |
| ----------- | --------------------------------------------------------------------------------------------------------------------------- | ------------------- |
| Collection  | List with filter- and sort-options. With support of POST to create record<br>/customers and /customers/{id}/orders          | GET, POST           |
| View        | Alternate view of collection with calulated result<br> /customers/nearby and /customers/{id}/orders/may_be_delayed          | GET                 |
| Resource    | View, update & delete record<br>customers/{id} and /customers/{id}/orders/{id}                                              | GET, PATCH, DELETE  |
| Intent      | Request action on resource, syncronous or async<br>/customers/{id}/doResetPassword, /customers/{id}/order/{id}/doRelease    | POST                |
| Upload      | Binary upload to resource field<br>/customers/{id}/field or /customers/{id}/orders/{id}/field                               | PUT                 |

## End-point parsing
Resource ID is identified as integer or string in parentheses.

    /groups/(72e8b54c-37ce-11eb-adc1-0242ac120002)/posts/634

**Parsing overview**

| Method | Path        | Description                                  | Sub-resource           |
| ------ | ----------- | -------------------------------------------- | ---------------------- |
| GET    | /S          | List collection of resources                 | /S/R/S                 |
| POST   | /S          | Create new resource                          | /S/R/S +               |
| GET    | /S/S        | List view                                    | /S/R/S/S               |
| POST   | /S/S        | Send intent on collection                    | /S/R/S/S               |
| GET    | /S/R+       | View resource                                | /S/R/S/R               |
| PATCH  | /S/R        | Update resource                              | /S/R/S/R               |
| DELETE | /S/R        | Delete resource                              | /S/R/S/R               |
| POST   | /S/R        | Update resource with html-form-data          | /S/R/S/R               |
| POST	 | /S/R/S	   | Sent intent on resource +                    | /S/R/S/R/S             |
| PUT    | /S/R/S      | Binary upload                                | /S/R/S/R/S             |

+ Note risk for collision between for POST /S/R/S. Intent /S/R/S has precedence over New sub-resource /S/R/S
+ If R=HINT on /S/R, resource-field sizes may be retured. (?)

## Naming conventions

### Casing
The API should use the **camel_casing** for resources its attribues. Period.
* More universal than PascalCasing
* Allows for API-arguments using UPPERCASE-arguments
* Improved readability (i_max vs IMax)

For intents (verbs) on resources or collections, camelCasing shoud be used to accentuate the action.

     /customers/346/doConvertToPartner

For API arguments, such as COUNT or PAGE, UPPER_CAMEL_CASE should be used.
    
     /customers?PAGE=4&COUNT=50

- API-arguments should be sent in URI
- No risk for field-name collision since UPPER_CASE
- No risk for collision with standard- or non-standard upper-kebab-case HTTP-HEADERS.
- No need to use (or not use) X-prefix in HEADER-arguments.

### Resources- and field names
- Resources should be named in pluralis, since:
  - Resources are collections
  - Provides a difference towards the resources attribues which are in singular
  - Irregular pluralis resources (mouce/mice) are rare
- Resouces should be limited to a two-level structure

      /customers/53/orders?year=2018&status=shipped

### Versioning
Versioning should be provided in **hostname**, (hence the project name REST-x)
- It provides easier machine/container-mapping of different verisons.
- Current version could be mapped to standard api.example.com
- **Both versioning in URI or HEADER are discouraged**

      api-2.example.com/customers?PAGE=5

## API-arguments
REST-x does not use header-arguments. API-arguments are sent in UPPER_CAMEL_CASE in request.
- Exception: file_name of binary file uploads (PUT).
- OAUTH/JWT etc are not a part of REST-x guidelines.

Current list of optional API arguments are:
- COUNT - number of records to be returned in collection
- PAGE - page of collection
- LANG - perefered language of error messages and hints.
- TZ - GMT time-zone
- DATE_FMT - YYYY-MM-DD
- TIME_FMT - H:i:s
- HINT - get data entry guidance for resource.

..this list is incomplete

## HATEOAS
- On single resource, allowed actions should be listed in a links section.
- On collection, allowed action on collection (next/prev) should be listed.
- On collection, allowed actions on collection-item **could** be listed.

## Return codes
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
- 500 Internal Server Error (The API is to be blamed)
- 503 Service Unavailable (3rd part API to be blamed)

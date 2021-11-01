# REST-x
Extended application-protocol for REST-API services.

[Version: 0.4](changelog.md)

## WHY
- Avoid hitting the wall as API gets bigger
- Guide myself and possibly others.

## Summary
 - [parsing]
 - [name_conventions]
 - [versioning]
 - [hateoas]
 - [api_arguments]
 - [return_codes]

[parsing]: parsing.md
[name_conventions]: name_conventions.md
[versioning]: versioning.md
[hateoas]: hateoas.md
[api_arguments]: api_arguments.md
[return_codes]: return_codes.md

## End-point types
Each API-endpoint should be of one of the types below, with standard endpoint-location.

| Type          | Description                                                                                | Methods allowed          |
| ------------- | ------------------------------------------------------------------------------------------ | ------------------------ |
| [Collection]  | List with filter-, sorting- and field arguments on resource fields.<br>POST create resouce | GET, POST                |
| [View]        | Alternate view of collection with non-resource arguments                                   | GET                      |
| [Resource]    | View, update & delete record and extended support for form-based deletion/upload           | GET, PATCH, DELETE, POST |
| [Intent]      | Request action on resource, syncronous or asyncronous                                      | POST                     |
| [Upload]      | Binary upload to resource field with support for chuncks                                   | PUT                      |

[Collection]: collection.md
[View]: view.md
[Resource]: resource.md
[Intent]: intent.md
[Upload]: upload.md

## End-point parsing
Resource ID is identified as integer or string in parentheses.

    /groups/(72e8b54c-37ce-11eb-adc1-0242ac120002)/posts/634
    
Composite keys should be avoided but may be used if JSON- and uri-encoded, inside parentheses. (Below not url-encoded for visibility)

    /order/({order_no:"522-532",order_part="4"})/items

**Parsing overview**
__S__ String value
__R__ Resource ID

| Method | Path        | Description                                  | Sub-resource           |
| ------ | ----------- | -------------------------------------------- | ---------------------- |
| GET    | /S          | List collection of resources                 | /S/R/S                 |
| POST   | /S          | Create new resource                          | /S/R/S +               |
| GET    | /S/S        | List view                                    | /S/R/S/S               |
| POST   | /S/S        | Send intent on collection                    | /S/R/S/S               |
| GET    | /S/R        | View resource                                | /S/R/S/R               |
| PATCH  | /S/R        | Update resource                              | /S/R/S/R               |
| DELETE | /S/R        | Delete resource                              | /S/R/S/R               |
| POST   | /S/R        | Update resource with html-form-data          | /S/R/S/R               |
| POST	 | /S/R/S +	   | Sent intent on resource                      | /S/R/S/R/S             |
| PUT    | /S/R/S      | Binary upload                                | /S/R/S/R/S             |

+ Note risk for collision between for POST /S/R/S. Intent /S/R/S has precedence over New sub-resource /S/R/S

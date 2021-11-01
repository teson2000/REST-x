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

# REST-x
Extended application-protocol for REST-API services.

[Version: 0.4](changelog.md)

## WHY
- Avoid hitting the wall as API gets bigger
- Guide myself and possibly others.

## Summary
| Topic              | Summary                                                                                |
| ------------------ | -------------------------------------------------------------------------------------- |
| [versioning]       | Versioning should be defined in host name, not in header or url.                       |
| [mame_conventions] | Resources in snake_case, intents in pascalCase, api-arguments in UPPER_SNAKE_CASE      |
| [api_arguments]    | In url (not header) PAGE, COUNT, OP_(field)), LANG, etc..                              |
| [parsing]          | Routing of request to resource / collection / intent                                   |
| [hateoas]          | Embedded in (\_links) and with label declaration                                       |
| [return_codes]     | Code and msg.                                                                          |

[versioning]: versioning.md
[name_conventions]: name_conventions.md
[api_arguments]: api_arguments.md
[parsing]: parsing.md
[hateoas]: hateoas.md
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

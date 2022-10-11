## End-point parsing
Resource ID is identified as integer or UUID.

    /groups/5325/posts/634
    /groups/72e8b54c-37ce-11eb-adc1-0242ac120002/posts/634

Single natural should be provided in parentheses.

    /groups/(rest-freaks/enthuiasts)/posts/634

Composite keys should be avoided but may be used if JSON- and uri-encoded, inside parentheses. (Below not url-encoded for visibility)

    /order/({order_no:"522-532",order_part="4"})/items

**Parsing overview**
- __S__ String value. Resource or intent based on context.
- __I__ Resource ID. Integer, GUID or composit according to above.

| Path       | GET                       | POST                       | PATCH                       | PUT                       |
| ---------- | ------------------------- | -------------------------- | --------------------------- | ------------------------- |
| /S         | Collection of resources   | Create new resource        | Update resource             | Write blob on resource    |
| /S/I       | Get resource              | Web update                 | N/A                         | N/A                       |
| /S/S       | Custom view on collection | N/A                        |                             |                           |


| Path       | Method | Description                                  | Sub-resource           |
| ---------- | ------ | -------------------------------------------- | ---------------------- |
| /S         | GET    | List collection of resources                 | /S /R/S                |
| /S         | POST   | Create new resource                          | /S /R/S (1)            |
| /S/S       | GET    | Custom view with custom arguments            | /S/S /R/S              |
| /S/S       | POST   | Request intent on collection(!)              | /S/S /R/S              |
| /S/R       | GET    | View resource                                | /S/R /S/R              |
| /S/R       | PATCH  | Update resource                              | /S/R/S/R               |
| /S/R       | DELETE | Delete resource                              | /S/R/S/R               |
| /S/R       | POST   | Update/create resource with html-form (2)    | /S/R/S/R               |
| /S/R/S (1) | POST	  | Request intent on resource                   | /S/R/S /R/S            |
| /S/R/S     | PUT    | Binary upload of field S on resource R       | /S/R/S /R/S            |

**Sub resources**
Sub-resources has the following paths.
**TO BE WRITTEN*

1) Note risk for collision between for POST /S/R/S. Intent /S/R/S has precedence over New sub-resource /S/R/S
2) Html-form data may be accepted for create/update record. Create record by providing null as key.

## End-point parsing
Resource ID is identified as integer or string in parentheses.

    /groups/(72e8b54c-37ce-11eb-adc1-0242ac120002)/posts/634
    
Composite keys should be avoided but may be used if JSON- and uri-encoded, inside parentheses. (Below not url-encoded for visibility)

    /order/({order_no:"522-532",order_part="4"})/items

**Parsing overview**
__S__ String value. Resource or intent
__R__ Resource ID. Integer, GUID or composit according to above.

| Path       | Method | Description                                  | Sub-resource           |
| ---------- | ------ | -------------------------------------------- | ---------------------- |
| /S         | GET    | List collection of resources                 | /S /R/S                |
| /S         | POST   | Create new resource                          | /S /R/S +              |
| /S/S       | GET    | List view                                    | /S/S /R/S              |
| /S/S       | POST   | Send intent on collection                    | /S/S /R/S              |
| /S/R       | GET    | View resource                                | /S/R /S/R              |
| /S/R       | PATCH  | Update resource                              | /S/R/S/R               |
| /S/R       | DELETE | Delete resource                              | /S/R/S/R               |
| /S/R       | POST   | Update resource with html-form-data          | /S/R/S/R               |
| /S/R/S +	 | POST	  | Sent intent on resource                      | /S/R/S /R/S            |
| /S/R/S     | PUT    | Binary upload                                | /S/R/S /R/S            |

**Sub resources**
Sub-resources has the following paths.
**TO BE WRITTEN*

+ Note risk for collision between for POST /S/R/S. Intent /S/R/S has precedence over New sub-resource /S/R/S

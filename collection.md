# Collection (GET)
For POST-action, see resource.

     /customers
     /customers/limited_view
     /customers/{id}/orders
     
## Arguments
Arguments in request are designed to be easy to interact with web forms.

- Filter-operators have their own arguments
- Search-operators may have their own arguments

### Filtering (y-axis)
Filtering may be applied to to fields in collection

     /customers?city=Lund

Filter-operators may be provided by adding the API-parameter OPER_(field_name) (operator).

    /customers?city=Lund&registration_year=2010&OPER_registration_year=GTE

The filter type BETWEEN uses the additional OPERTO_(field_name) to pass max-value

    /customers?city=Lund&registration_date=2001-01-01&OPER_registration_date=BETWEEN&TO_registration_date=2014-12-12
    
Valid operators are:

| \_OP       | Meaning | Comment                            |
| ---------- | ------- | ---------------------------------- |
| EQU        | =       | default                            |
| NOT        | <>      | Not equal to                       |
| GT         | >       | Greater than                       |
| GTE        | >=      | Greater or equal                   |
| LT         | <       | Less than                          |
| LTE        | <=      | Less or equal than                 |
| LIKE       | *       | Limits set by API                  |
| IN         | a,b,c   | Comma-separated list of values     |
| BETWEEN    | range   | (field) sets from value            |
| (BETWEEN)  | range   | TO_(field) sets to value           |

### Sorting
Sorting may be applied to collection in two ways, either on field by using api-suffix \_SORT

**Option 1, individual sort-arguments**
This option is designed to directly interact with web forms:

     /customers?SORT_city=asc

May be combined with additional sort-fields

    /customers?SORT_city=asc&SORT_registration_year=desc
    
Sorting priority is by default in argument-order but may be overridden with

    /customers?SORT_city=asc&SORT_registration_year=desc&SORT_BY=registration_year,city
    
**Option 2, combined sort-arguments**
Designed to interact with designed API-request

    /customers?SORT_BY=+city,-registration_year
    
### Field-filtering (X-axis)
To minimize used bandwidth, fields may be limited

    /customers?FIELDS=customer_id,city

### Pagination
Pagination may be used by using the API-parameters COUNT and PAGE

    /customers?COUNT=50&PAGE=10

## Return format
Returning the collection does not have to include all fields of the individual record.
Links (HATEOAS) should be provided to collection and to collection-items **when requested**

The point of HATEOAS is for debate since each endpoint is so flexible it's not realistic to make links for all.

- The return-format are inspired by the JSON:API standard, but simplified.
- The 'links' are returned by default, with the types of
  - first, prev, next, last for page-navigation
  - HINT for new-record entry.
- The 'LINKS' on item could be requested with LINKS=1

Calculating the appropriate grants is disabled by default since it may require CPU to be trustworthy.

    {
      'meta':
        "count": 5325
      },
      'links': {
        "link_type": "URI",
        "new": "/customers?HINT=1"
      }
      'data': [
        {
          'id' : 1,
          'city' : 'Lund',
          'registration_year': '2015',
          'LINKS' : {
            'delete' : "URI",
            ...
          },
        },
        {},
        ...
      ]
    }


[back](README.md)

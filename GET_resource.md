# GET resource
- Data and HATEOAS-links are provided.
- Enums are provided for option-boxes.
- Enums should adhere LANG in header
- Intents could be added as HATEOAS-links

     {
       'links': {},
       'data': {},
       'enums': {
         'status_code': {
           'shipped': 'Is shipped',
           'open': 'Open for modification'
         }
       }
     }

## Hinting
Hinting provides information to the client about field-type, field-size and recommended labels and placehoders.

Hinting of creating new record

     GET /customers/53/orders?HINT=1

Hinting of editing existing record

     GET /customers/53/orders/324?HINT=1


    'fields': {
      'name': {
        'type': varchar,
        'size': 50,
        'required':true,
        'label': 'Company name',
        'placeholder':'Enter company name'
      },
      'city': {
        'type': varchar,
        'size': 30,
        'required':no,
        ...

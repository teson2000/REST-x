# Resource (GET/PATCH/DELETE/POST)
- Data and HATEOAS-links are provided.
- Enums are provided for option-boxes.
- Enums should adhere LANG in header
- Intents could be added as HATEOAS-links
- Only authorized HATEOAS/intents should be provided.
    
      {
        'links': {
          'self': 'https://api2v4.example.com/orders/(535-535)'
          'ship': './doShip'
          'delete': '.'
        },
        'data': {
          'order_id': '535-535',
          'adress': '221B Baker Street',
          'status_code': 'open'
        },
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
        'required': true,
        'label': 'Company name',
        'placeholder':'Enter company name'
      },
      'city': {
        'type': varchar,
        'size': 30,
        'required': false,
        ...


## PATCH and binary data
- PATCH may remove binary data by setting field_name to null.

## POST and binary data
- POST (form-data) may update binary data and also delete binary field using field_name_DELETE = 1

[Back](README.md)

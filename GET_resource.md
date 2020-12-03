# GET resource
- Data and HATEOAS-links are provided.
- 

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
    'size': 50,
    'required':no,
  }
  ..
}

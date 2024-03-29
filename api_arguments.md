## API-arguments
REST-x does not endorse header-arguments. API-arguments are preferably sent as UPPER_CAMEL_CASE in request URI.

- Exception: file_name of binary file uploads (PUT).
- OAUTH/JWT etc are not a part of REST-x guidelines.

Current list of optional API arguments are:

**Collection arguments (final)**
- COUNT - number of records to be returned in collection
- FIELDS - limits collection fields (FIELDS=first_name,last_name)
- PAGE - page of collection
- OPER_(field_name) - GT/LT/NEQU etc on filter collection
- SORT_(field_name) - = ASC or DESC
- SORT_BY - collection of fields for nested sort order (=last_name,first_name) or (=+lastname,-first_name)


**General arguments (draft)**
- LANG - perefered language of error messages, HATEOAS-labels and field-labels / placeholder / hints.
- TZ - GMT time-zone
- FMT_DATE - YYYY-MM-DD
- FMT_TIME - H:i:s
- HINT - get data entry guidance for resource.

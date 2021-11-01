## API-arguments
REST-x does not use header-arguments. API-arguments are sent in UPPER_CAMEL_CASE in request.
- Exception: file_name of binary file uploads (PUT).
- OAUTH/JWT etc are not a part of REST-x guidelines.

Current list of optional API arguments are:
- COUNT - number of records to be returned in collection
- PAGE - page of collection
- LANG - perefered language of error messages and hints.
- TZ - GMT time-zone
- FMT_DATE - YYYY-MM-DD
- FMT_TIME - H:i:s
- HINT - get data entry guidance for resource.

..this list is incomplete

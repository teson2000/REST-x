## Naming conventions

### Casing
The API should use the **camel_casing** for resources its attribues. Period.
* More universal (java, python etc) than camelCasing or PascalCasing
* Allows for safe API-arguments using UPPERCASE-arguments
* Improved readability (i_max vs IMax)

For intents (verbs) on resources or collections, camelCasing *should* be used to accentuate the method/intent.

     POST /customers/346/convertToPartner

For API arguments, such as COUNT or PAGE, UPPER_SNAKE_CASE should be used.
    
     /customers?PAGE=4&COUNT=50

- API-arguments may be sent in URI or HEADER
- No risk for field-name collision since UPPER_CASE
- No risk for collision with standard- or non-standard upper-kebab-case HTTP-HEADERS.
- No need to use (or not use) X-prefix in HEADER-arguments.
- Arguments in HEADER *may* be prefixed with API_

### Resources- and field names
- Resources should normally be named in pluralis, since:
  - Resources are collections
  - Provides a difference towards the resources attribues which are in singular
  - Irregular pluralis resources (mouce/mice) are rare
  - Exception when surronding systems use singular standards
- Resouces should be limited to a two-level structure

      GET /customers/53/orders?year=2018&status=shipped

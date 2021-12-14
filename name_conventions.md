# Naming conventions / casing

## Resources
Resources and their fields should use **snake_casing**. Period.

- More universal (java, python etc) than camelCasing or PascalCasing
- Allows for safe API-arguments using UPPERCASE-arguments
- Improved readability (i_max over IMax)

### Pluralis for resources

 - Resources should use pluralis unless non collection resources (SESSION)
 - Resources should be limited to a two-level structure

      GET /customers/53/orders?year=2018&status=shipped

## Intents
For intents (RPC like actions) on resources or collections, camelCasing *should* be used to accentuate the method/intent.

     POST /customers/346/convertToPartner
     
## API-arguments
For API arguments, such as COUNT or PAGE, UPPER_SNAKE_CASE should be used.
    
     GET /customers?PAGE=4&COUNT=50

- API-arguments may be sent in URI or HEADER
- No risk for field-name collision since UPPER_CASE
- No risk for collision with standard- or non-standard upper-kebab-case HTTP-HEADERS.
- No need to use (or not use) X-prefix in HEADER-arguments.
- Arguments in HEADER *may* be prefixed with API_



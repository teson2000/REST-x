# PUT (binary upload)
The PUT method is by the original standard used to replace a resource. This might be a bad idea.
- The resource may hold data that is not exposed of the API that would be lost.
- If only the fields of the resource should be replaced it could be regarded as a PATCH.
- PUT is by design idempotent which is may be hard to design at API-design time.

PUT however, fits perfectly to support uploads of binary content.
- Content shoud be sent RAW (not FORM-ENCODED since this is related to HTML and not HTTP).
- Original file_name may be sent in header.

The method is applied NOT to the resource, but to the resource-field:

    PUT /customers/53/customer_logo
    
The original filename may be supplied

    PUT /customers/53/customer_logo?FILE_NAME=myLogo.png
    
## Partial upload
Upload may be split into sections to allow progress feedback.

    PUT /customers/53/customer_logo?PART=1/10

Partial upload may be cancelled (allowing for deletion of incomplete upload at server)

    PUT /customers/53/customer_logo?PART=cancel
    
- Partial content (3/10) could be uploaded multiple times
- Partial content could be uploaded unordered
- Partial content response code is 202.

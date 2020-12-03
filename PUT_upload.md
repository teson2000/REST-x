# PUT (binary upload)
The PUT method is by the original standard used to replace a resource. This might be a bad idea.
- The resource may hold data that is not exposed of the API that would be lost.
- If only the fields of the resource should be replaced it could be regarded as a PATCH.
- PUT is by design idempotent which may not fit underlying systems of the API.

PUT however, fits perfectly to support uploads of binary content.
- Content shoud be sent RAW (not FORM-ENCODED since this is related to HTML and not HTTP).
- Original file_name may be sent in URI using FILE_NAME.

The method is applied NOT to the resource, but to the resource-field:

    PUT /customers/53/logo_file
    
The original filename may be supplied

    PUT /customers/53/logo_file?FILE_NAME=myLogo.png
    
The file-name should be url-encoded and in same char-set as API (normally UTF-8)
    
## Partial upload
Upload may be split into sections to allow progress feedback.

    PUT /customers/53/logo_file?PART=1/10

Partial upload may be cancelled (allowing for deletion of incomplete upload at server)

    PUT /customers/53/logo_file?PART=cancel
    
- The same partial content could be uploaded multiple times
- Partial content could be uploaded unordered
- Until completion (PART=X/X), content response code is 202. On complete, 201

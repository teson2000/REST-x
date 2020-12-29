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
    
The original filename may be supplied.

    PUT /customers/53/logo_file?FILE_NAME=myLogo.png
    
The file-name should be url-encoded and in same char-set as API (normally UTF-8)
    
## Partial upload
Upload may be split into sections to allow progress feedback. Chunks may be 10 or 100.

    PUT /customers/53/logo_file?PART=1/10
    
On final part, file-name and md5-checksum may be provided to validate upload

    PUT /customers/53/logo_file?PART=10/10&MD5=d41d8cd98f00b204e9800998ecf8427e

Partial upload may be cancelled (allowing for deletion of incomplete upload at server)

    PUT /customers/53/logo_file?PART=cancel
    
Partial upload does __not__ have to support idempotency.
- The same partial content should __not__ be uploaded multiple times
- Partial content shoul be uploaded in order.
- Server may sequentially append each chunk to tempororary file.
- Until completion (PART=X/X), content response code is 202. On complete, 201
- At final part, we may send original file-name and md5 for integrity check
- Previous version of file should be replaced upon successfull final chunk.
- Upon cancel, response code is 200, even if temporary file was never created. 

[Back](README.md)

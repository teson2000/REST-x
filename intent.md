# POST-intents
- Intents are **verbs** to extend the limitations or resource-based API design.
- Intents may/should be self-describing by allowing GET-method on intent-URI
- Intents may use camelCase and start with "do" to accentuate that it's a verb.

    /customer/53/doBlockForSales
    
    /rockets/apollo11/doLaunch
    
    /imports/53/doCommit
    
## Transactions
By using intents transcation-like behaviours may be provided to API

Arguments to intent should be as few as possible due to documentation.

    POST /imports (create new import job)
    
    PUT /imports/53/log_file (upload log file to be imported)
    
    GET /imports/53 (view preliminary, status='not checked')
    
    GET /imports/53/integrityCheck (check integrity of log file)
    
    POST /imports/53/doImport > 202
    
    GET /imports/53 (status='running', 'error' or 'complete')
    
    now either
    
    POST /imports/53/doRollback or /imports/53/doCommit

[Back](README.md)

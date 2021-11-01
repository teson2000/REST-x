# Petstore errata
According to specifications in REST-x, petstore should be re-arranged according to:

    -- **PET**
    POST /pet/{petId}/uploadImage > PUT /pet/{petId}/image (put used for binary raw transfer)
    POST /pet > ok
    PUT /pet > PATCH /pet (patch is less destructive than put)
    GET /pet/findByStatus > GET /pet/find_by_status (view)
    GET /pet/{petId} > ok
    POST /pet/{petID} > ok (form-data)
    (missing) > PATCH /pet/{petID} update with json
    DELETE /pet/{petId} > ok
    -- ** STORE **
    Store rewritten see as:
    GET /store/inventory > /stores/{store_id}/pets
    -- ** ORDERS **
    Odd B2B endpoints?
    POST /store/order > expanded to:
      POST /orders > create (prepare) order
      POST /orders/{order_id}/items (add item to order)
      POST /orders/{order_id}/doRelease (intent on order for further processing)
    -- ** USER(s) **
    Confusion around the collection USERS and the state resource SESSION
    POST /user/createWhiteList > POST /users/createUsersFromJSON
    GET /user/{username} > (numeric PK) GET /users/({username})
    POST /user > POST /users
    -- ** SESSION ** 
    GET /user/login > POST /session/doLogin
    GET /user/logout > POST /session/doLogout
    
    

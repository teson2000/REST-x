# Custom views
Custom views allow arguments not present as fields.

Return format of custom views may be different from the standard resource-collection format.
The HATEOAS-link "self" should point to the **standard** resource URI.

Example of view-endpoint accepting non-resource argument and returning calculated (non-resource) value.

     /customers/nearby?my_gps=53.25,25.25

May return:

    {
      'data': [
        {
          'id' : 3030,
           'name': 'bob',
           'distance_km': 40,
           'LINKS': {
             'self' : '/customers/3030'
           }
         },
         {
           'id : 5050,
           ..
         }
       }
     }

[Back](README.md)

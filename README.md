# A web-based intelligent editor for security modeling

## Description
  A computer science bachelor thesis. Time alloted: 9 weeks (Individual study).

## Features
  * Data models
  
    An example to demonstrate data models:  Consider a simple domain, where there are only cars and persons. The persons can own cars (they are their owners), and, logically, the cars can be owned by persons (they are their ownedCars). No restriction is imposed regarding ownership: a person can own many different cars (or none), and a car can be owned by many different persons (or by none). Finally, each car can have a color, and each person can have a name. This domain can be model (using our JSON-format) as follows:
    
    ```json
     [
      {"class" : "Car",
       "attributes" : [
          {"name" : "color", "type" : "String"},
          {"name" : "model", "type" : "String"}
          ]
      },
      {"class" : "Person",
       "attributes" : [
          {"name" : "name", "type" : "String"},
          {"name" : "age", "type" : "String"}
          ]
      },
      {"association" : "Ownership",
       "ends" : ["owners", "ownedCars"],
       "classes" : ["Car", "Person"]
      }
     ]
    ```

  * Security models
  
      An example to demonstrate security models: Consider the following (fine-grained) access-control policy, where Person is the user-class.
    
    * Any user can read the name of any other user.
    * Any user can read its own age.
    * Any user with role “Police” can read the age of the cars’ owners.
    * Any user with role “Police” can read the cars’ owners.
    * Any user with role “Police” can read the owners’ cars.
    
    ```json
     [
      {
        "class" : "Car",
        "permissions" : [
          {
            "actions" : ["read"],
            "resources" : ["owners"],
            "roles" : ["Police"],
            "auth" : "true"
          }
        ]
      },
      {
        "class" : "Person",
        "permissions" : [
          {
            "actions" : ["read"],
            "resources" : ["name"],
            "default" : "true"
          },
          {
            "actions" : ["read"],
            "resources" : ["age"],
            "default" : "self = caller"
          },
          {
            "actions" : ["read"],
            "resources" : ["age"],
            "roles" : ["Police"],
            "auth" : "self.ownedCars->notEmpty()"
          },
          {
            "actions" : ["read"],
            "resources" : ["ownedCars"],
            "roles" : ["Police"],
            "auth" : "true"
          }
        ]
      }
    ]
    ```
  
  
  
  
## Author
     Duong Thai Hoang
